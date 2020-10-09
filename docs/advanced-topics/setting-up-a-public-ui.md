# Setting Up a Public UI

This page explains how to set up a [polkadot-js/apps UI](https://polkadot.js.org/apps/) for Edgeware, using the Edgeware branch of `apps`. The main difference is that the Edgeware branch supports the types defined in Edgeware's voting and governance modules.

## 0. Provisioning a server

Provision an appropriately sized server from one of the recommended VPS providers.

We assume you are using Ubuntu 18.04 x64; other versions or operating systems will require adjustments to these instructions.

Set up DNS pointing to the server, from e.g. apps.edgewa.re. It is strongly recommended that you do this now.

SSH into the server.

## 1. Installing `apps` and setting it up as a system service

Clone the `apps` repo:

```text
git clone https://github.com/hicommonwealth/apps.git
cd apps
```

Install nodejs 11.x and yarn. You will need to add new package repositories:

```text
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
apt update
apt install -y nodejs yarn
```

Install dependencies:

```text
yarn
```

Create the apps service:

```text
{
    echo '[Unit]'
    echo 'Description=EdgewareApps'
    echo '[Service]'
    echo 'Type=exec'
    echo 'WorkingDirectory='`pwd`
    echo 'Environment=ENV=production'
    echo 'ExecStart=yarn run start'
    echo '[Install]'
    echo 'WantedBy=multi-user.target'
} > /etc/systemd/system/apps.service
```

Start and check the service is running:

```text
systemctl start apps
systemctl status apps
curl localhost:3000
```

## 2. Configuring an SSL certificate

To make `apps` available in a secure manner, we will use Let's Encrypt and certbot to make the server available via SSL.

Install Certbot:

```text
apt -y install software-properties-common
add-apt-repository universe
add-apt-repository ppa:certbot/certbot
apt update
apt -y install certbot python-certbot-nginx
```

Run certbot to get a certificate from Let's Encrypt:

```text
certbot --nginx
```

Certbot will ask you some questions, start its own web server, and talk to Let's Encrypt to issue a certificate.

When it asks you whether to redirect traffic from port 80 to SSL, you should respond **yes**.

## 3. Updating the nginx configuration

Set the intended public address of the server, e.g. apps.edgewa.re, as an environment variable:

```text
export name=apps.edgewa.re
```

Set up an nginx configuration. This will inject the public address you have just defined.

```text
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
    echo '      ssl_protocols  SSLv2 SSLv3 TLSv1;'
    echo '      ssl_ciphers  HIGH:!aNULL:!MD5;'
    echo '      ssl_prefer_server_ciphers   on;'
    echo ''
    echo '      location / {'
    echo '          proxy_pass http://127.0.0.1:3000 ;'
    echo '      }'
    echo '    }'
    echo '}'
} > /etc/nginx/nginx.conf
```

Start nginx, and ensure it is run on system startup:

```text
systemctl daemon-reload
systemctl start nginx
systemctl enable nginx
```

Check your server is running from your local browser.

