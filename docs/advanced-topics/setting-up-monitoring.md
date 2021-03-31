# Setting Up Monitoring

If you are running a validator or a public node, you should set up system monitoring to be aware if your node goes offline, and restart it automatically if possible.

This tutorial explains how to set up **monit** and **mmonit** to accomplish this:

* Monit is a process monitoring tool, which can restart your node if it stalls.
* Mmonit is a dashboard that shows the performance \(CPU, memory, alerts, etc.\)

  of monit nodes.

\(If you don't need a dashboard, you can skip directly to the section for setting up `monit` on an individual node.\)

The tutorial assumes you are running Ubuntu 18.04.

## Setting up an `mmonit` monitoring server

For the monitoring server, a small server should be enough \(e.g. 1GB memory\). The default setup will use SQLite as a database. This means if you remove the monit directory, all logged events will be lost!

```text
apt install -y monit
wget https://mmonit.com/dist/mmonit-3.7.3-linux-x64.tar.gz
tar -vxzf mmonit-3.7.3-linux-x64.tar.gz
mv mmonit-3.7.3 mmonit
```

Use monit to keep mmonit up:

```text
{
    echo 'check process mmonit with pidfile '`pwd`'/mmonit/logs/mmonit.pid'
    echo '  start program = "'`pwd`'/mmonit/bin/mmonit"'
    echo '  stop program = "'`pwd`'/mmonit/bin/mmonit stop"'
    echo 'set httpd port 2812 and use address localhost'
    echo '  allow localhost'
} > /etc/monit/monitrc

monit reload
monit validate
```

To start the mmonit dashboard manually, you can use the command `mmonit/bin/mmonit`. To stop, use `mmonit/bin/mmonit stop`.

Now, go to the node in your browser, e.g `http://monitor.edgewa.re:8080/`. Log in with username `admin` and password `swordfish` and change the default username and password.

You should end up with two users; admin is what you'll use to log in, and the other user is what you'll provide to nodes that push data to the monitoring server.

## Setting up `monit` on an individual node

SSH into your node.

Before proceeding, set an appropriate hostname for the node, e.g.

```text
hostnamectl set-hostname validator1
```

Install monit.

```text
apt install -y monit
```

Set up a Slack webhook \(optional\):

```text
export WEBHOOK=[slack webhook url]
{
    echo 'URL="'$WEBHOOK'"'
    echo "PAYLOAD='{\"text\": \"`hostname` restarted edgeware.service\"}'"
    echo 'curl -s -X POST --data-urlencode "payload=$PAYLOAD" $URL'
} > /root/slack_notify.sh

chmod 755 /root/slack_notify.sh
```

Set up a Monit config to check the Edgeware service at 10-second intervals, restart if CPU &gt; 90% for five checks \(~50sec\), and post events to mmonit.

If you are using mmonit, include the username and password you have set for mmonit above. Otherwise, you should remove the sections that use the username and password below:

```text
export USER=edgeware
export PASSWORD=[password]
export TARGET=[domain]
{
    echo 'set daemon 10'
    echo 'set log /var/log/monit.log'
    echo 'set idfile /var/lib/monit/id'
    echo 'set statefile /var/lib/monit/state'
    echo 'set eventqueue'
    echo '  basedir /var/lib/monit/events'
    echo '  slots 100                    '
    echo ''
    echo 'check process edgeware matching target/release/edgeware'
    echo '  start program = "/bin/systemctl restart edgeware"'
    echo '  stop program = "/bin/systemctl kill edgeware"'
    echo '  if cpu > 90% for 20 cycles then exec "/bin/systemctl stop edgeware" and repeat every 10 cycles'
    echo '  if cpu > 90% for 64 cycles then exec "/bin/systemctl kill edgeware" and repeat every 10 cycles'
    echo '  if cpu > 90% for 64 cycles then alert'
    echo '  if does not exist for 1 cycles then start'
    echo '  if does not exist for 1 cycles then exec "/bin/bash -c /root/slack_notify.sh"'
    echo ''
    echo 'set mmonit http://'$USER:$PASSWORD@$TARGET':8080/collector'
    echo 'set httpd port 2812 and use address localhost'
    echo '  allow localhost'
    echo '  allow '$USER:$PASSWORD
} > /etc/monit/monitrc

chmod 600 /etc/monit/monitrc

monit reload
monit validate
```

Refer to the [monit documentation](https://mmonit.com/monit/documentation/monit.html) if you would like to set up email alerts or other additional checks on your node.

## Monitoring API health

So far, monit will only check to ensure that the node does not remain at 100% CPU for extended periods of time. We can now add another check that uses the API to ensure the node is accepting connections and syncing properly.

This will catch some failure scenarios where the node appears to keep operating but stops recognizing new blocks. We provide `nodeup` for this purpose.

Clone [nodeup](https://github.com/hicommonwealth/nodeup) into the `/root` directory. Follow its installation instructions:

```text
git clone https://github.com/hicommonwealth/nodeup.git
cd nodeup
apt install -y nodejs npm
npm install -g yarn
yarn
```

Make sure your node is running with the `--rpc-cors="*"` flag, so WebSocket connections are accepted. Note that by default, this will not make the node accept connections from outside the local machine \(`--ws-external` is required for that\).

Test nodeup:

```text
node index.js
```

If it is working, you can now add these lines to your monit configuration at `/etc/monit/monitrc` \(they assume that nodeup is installed in the `/root/nodeup` directory, adjust accordingly if not\):

```text
check program nodeup with path "/root/nodeup/index.js -u ws://localhost:9944"
  if status > 0 for 10 cycles then exec "/bin/systemctl stop edgeware" and repeat every 10 cycles
```

Restart monit, and check that the new script is working:

```text
monit reload
monit status
```

