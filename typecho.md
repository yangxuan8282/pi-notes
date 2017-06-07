typecho
===

follow [BLFS](http://www.linuxfromscratch.org/blfs/view/stable/general/php.html) compile && install php, or use [oneinstack](https://oneinstack.com/install/) to install it

```
mkdir -p ~/src/typecho ~/work/run/typecho &&
wget -O ~/src/typecho/typecho.zip https://github.com/typecho/typecho/archive/master.zip &&
unzip ~/src/typecho/typecho.zip -d ~/work/run/typecho
```

```
cd ~/work/run/typecho/typecho-master &&
php -S php -S 0000:1994 -t .
```

```
echo "[Unit]
Description=Typecho blog
After=network.target

[Service]
ExecStart=/usr/bin/php -S 0000:1994 -t /home/pi/work/run/typecho/typecho-master
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target " | sudo tee /etc/systemd/system/typecho.service
```

