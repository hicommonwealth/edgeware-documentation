# Set Up a Full Node

This guide covers how to set up an Edgeware node. There are two ways you can proceed:

* Setting up a private node, e.g. if you would like to run a validator
* Setting up a public node, e.g. if you want to run connect services or dapps to Edgeware

{% hint style="info" %}
To quickly run node from **Docker** image: [https://hub.docker.com/repository/docker/hicommonwealth/edgeware](https://hub.docker.com/repository/docker/hicommonwealth/edgeware)
{% endhint %}

If you are running a private node, you will only need to follow **steps 0 and 1** of this guide. Otherwise, we will guide you through setting up an SSL certificate in **steps 2 and 3**, so any browser can securely connect to your node. (Most people, including validators, only need to set up a private node.)

## 0. Provisioning a server

Provision an appropriately sized server from a reputable VPS provider, e.g.:

* [Vultr](https://www.vultr.com)
* [DigitalOcean](https://www.digitalocean.com)
* [Linode](https://www.linode.com)
* [OVH](https://www.ovh.com.au)
* [Contabo](https://contabo.com)
* [Scaleway](https://www.scaleway.com/en/)
* [Amazon AWS](https://aws.amazon.com), etc.

We recommend a node with at least 2GB of RAM, and Ubuntu 18.04 x64. Other operating systems will require adjustments to these instructions.

If you are running a public node, set up DNS from a domain name that you own to point to the server. The DNS target needs to be type A and not Redirect type. We will use `testnet1.edgewa.re`. (You don't need to do this if you are setting up a private node.)

SSH into the server.

## 1. Installing Edgeware and setting it up as a system service

First, clone the `edgeware-node` repo, install any dependencies, and run the required build scripts.

```
apt update
apt install -y gcc libc6-dev
apt install -y cmake pkg-config libssl-dev git clang libclang-dev

# Prefetch SSH publickeys
ssh-keyscan -H github.com >> ~/.ssh/known_hosts

# Install rustup
curl https://sh.rustup.rs -sSf | sh -s -- -y
source /root/.cargo/env
export PATH=/root/.cargo/bin:$PATH

# Get packages
git clone https://github.com/hicommonwealth/edgeware-node.git
cd edgeware-node

# Build packages
./setup.sh
```

Set up the node as a system service. To do this, navigate into the root directory of the `edgeware-node` repo and execute the following to create the service configuration file:

```
{
    echo '[Unit]'
    echo 'Description=Edgeware'
    echo '[Service]'
    echo 'Type=exec'
    echo 'WorkingDirectory='`pwd`
    echo 'ExecStart='`pwd`'/target/release/edgeware --chain=edgeware --ws-external --rpc-cors "*"'
    echo '[Install]'
    echo 'WantedBy=multi-user.target'
} > /etc/systemd/system/edgeware.service
```

**Note: This will create an Edgeware server that accepts incoming connections from anyone on the internet. If you are using the node as a validator, you should instead remove the `ws-external` flag, so Edgeware does not accept outside connections.**

Double check that the config has been written to `/etc/systemd/system/edgeware.service` correctly. If so, enable the service so it runs on startup, and then try to start it now:

```
systemctl enable edgeware
systemctl start edgeware
```

Check the status of the service:

```
systemctl status edgeware
```

You should see the node connecting to the network and syncing the latest blocks. If you need to tail the latest output, you can use:

```
journalctl -u edgeware.service -f
```

## 2. Configuring an SSL certificate (public nodes only)

We will use Certbot to talk to Let's Encrypt. Install Certbot dependencies:

```
apt -y install software-properties-common
add-apt-repository universe
snap install --classic certbot
apt update
```

Install Certbot:

```
apt -y install certbot python-certbot-nginx
```

It will guide you through getting a certificate from Let's Encrypt:

```
certbot certonly --standalone
```

If you already have a web server running (e.g. nginx, Apache, etc.) you will need to stop it, by running e.g. `service nginx stop`, for this to work.

Certbot will ask you some questions, start its own web server, and talk to Let's Encrypt to issue a certificate. In the end, you should see output that looks like this:

```
root:~/edgeware-node# certbot certonly --standalone
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator standalone, Installer None
Please enter in your domain name(s) (comma and/or space separated)  (Enter 'c'
to cancel): testnet1.edgewa.re
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for testnet1.edgewa.re
Waiting for verification...
Cleaning up challenges

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/testnet1.edgewa.re/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/testnet1.edgewa.re/privkey.pem
   Your cert will expire on 2019-10-08. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
```

## 3. Configuring a Websockets proxy (public nodes only)

First, install nginx:

```
apt -y install nginx
```

Set the intended public address of the server, e.g. `testnet1.edgewa.re`, as an environment variable:

```
export name=testnet1.edgewa.re
```

Set up an nginx configuration. This will inject the public address you have just defined.

```
{
    echo 'user       www-data;  ## Default: nobody'
    echo 'worker_processes  5;  ## Default: 1'
    echo 'error_log  /var/log/nginx/error.log;'
    echo 'pid        /var/run/nginx.pid;'
    echo 'worker_rlimit_nofile 8192;'
    echo ''
    echo 'events {'
    echo '  worker_connections  4096;  ## Default: 1024'
    echo '}'
    echo ''
    echo 'http {'
    echo '    map $http_upgrade $connection_upgrade {'
    echo '      default upgrade;'
    echo "      \'\' close;"
    echo '    }'
    echo '    server {'
    echo '      listen       443 ssl;'
    echo '      server_name  '$name';'
    echo ''
    echo '      ssl_certificate /etc/letsencrypt/live/'$name'/cert.pem;'
    echo '      ssl_certificate_key /etc/letsencrypt/live/'$name'/privkey.pem;'
    echo '      ssl_session_timeout 5m;'
    echo '      ssl_protocols  SSLv2 SSLv3 TLSv1 TLSv1.1 TLSv1.2 TLSv1.3;'
    echo '      ssl_ciphers  HIGH:!aNULL:!MD5;'
    echo '      ssl_prefer_server_ciphers   on;'
    echo ''
    echo '      location / {'
    echo '          proxy_pass http://127.0.0.1:9944 ;'
    echo '          proxy_http_version 1.1;'
    echo '          proxy_set_header Upgrade $http_upgrade;'
    echo '          proxy_set_header Connection $connection_upgrade;'
    echo '      }'
    echo '    }'
    echo '}'
} > /etc/nginx/nginx.conf
```

Make sure that the paths of `ssl_certificate` and `ssl_certificate_key` match what Let's Encrypt produced earlier. Check that the configuration file has been created correctly.

```
cat /etc/nginx/nginx.conf
nginx -t
```

Make sure that Nginx's OpenSSL version >1.0.2 You will have to Rebuild Nginx if the OpenSSL version is lower. Otherwise, modern TLS protocols created in letsencrypt certificates won't work, and Nginx will throw an error.

If there is an error, `nginx -t` should tell you where it is. **Note that there may be subtle variations in how different systems are configured, e.g. some boxes may have different login users or locations for log files. It is up to you to reconcile these differences.**

Start the server:

```
service nginx restart
```

You can now try to connect to your new node from [polkadot.js/apps](https://polkadot.js.org/apps/#/settings), or by making a curl request that emulates opening a secure WebSockets connection:

```
curl --include --no-buffer --header "Connection: Upgrade" --header "Upgrade: websocket" --header "Host: $name:80" --header "Origin: http://$name:80" --header "Sec-WebSocket-Key: SGVsbG8sIHdvcmxkIQ==" --header "Sec-WebSocket-Version: 13" http://$name:9944/
```

## 4. Connecting to your node

Congratulations on your new node! If you set up public DNS and a SSL certificate in steps 2 and 3, you should be able to connect to it now from [polkadot-js/apps](https://polkadot.js.org/apps/#/settings):

![](https://user-images.githubusercontent.com/1273926/66156368-631b3400-e5d6-11e9-8254-33040f87ee4f.png)

Otherwise, you should be able to use [edgeware-cli](https://github.com/hicommonwealth/edgeware-cli) to connect to it:

```
git clone https://github.com/hicommonwealth/edgeware-cli.git
cd edgeware-cli
yarn
bin/edge -r ws://testnet1.edgewa.re:9944 balances freeBalance 5G8jA2TLTQqnofx2jCE1MAtaZNqnJf1ujv7LdZBv2LGznJE2
```

In general, you should use these URLs to connect to your node:

* `ws://testnet1.edgewa.re:9944` if you set it up as a public node with `--ws-external` in step 1
* `wss://testnet1.edgewa.re` if you set it up as a public node and also followed steps 2 and 3

## 5. Next steps

Your node will automatically restart when the system reboots, but it may not be able to recover from other failures. To handle those, consider following our guide to [Setting up monitoring](../advanced/setting-up-monitoring.md).

You may also wish to proceed to [Validating on Edgeware](set-up-a-validator.md).
