ghost.md
===

```
curl -sL https://deb.nodesource.com/setup | sudo bash -
```

for China user:

```
sudo sh -c 'cat > /etc/apt/sources.list.d/nodesource.list <<"EOF"
deb https://mirrors.tuna.tsinghua.edu.cn/nodesource/deb_6.x/ jessie main
deb-src https://mirrors.tuna.tsinghua.edu.cn/nodesource/deb_6.x/ jessie main
EOF'
```

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 1655A0AB68576280 &&
sudo apt-get update &&
sudo apt-get install nodejs 
```

```
curl -L https://ghost.org/zip/ghost-latest.zip -o ghost.zip
```

```
sudo mkdir -p /var/www &&
unzip -uo ghost.zip -d /var/www/ghost
```

```
mv npm-shrinkwrap.json npm-shrinkwrap.json.orig &&
npm install --production --registry=https://registry.npm.taobao.org
```

> replace `$URL` with your url

```
sudo sh -c 'sed -i "s|my-ghost-blog.com|$URL|1" /var/www/ghost/config.js' &&
sudo sh -c 'sed -i "s/127.0.0.1/0.0.0.0/1" /var/www/ghost/config.js'
```

```
npm start --production
```

then visit: `raspberrypi:2368` or your url

**/etc/systemd/system/ghost.service**

```
[Unit]
Description=Ghost blog
After=network.target

[Service]
Type=simple
PIDFile=/run/ghost.pid
WorkingDirectory=/var/www/ghost
User=pi
ExecStart=/usr/bin/npm start --production /var/www/ghost
ExecStop=/usr/bin/npm stop /var/www/ghost
StandardOutput=null
StandardError=null

[Install]
WantedBy=multi-user.target
```

