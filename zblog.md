zblog
===

install zblog on raspberry pi
---

follow [BLFS](http://www.linuxfromscratch.org/blfs/view/stable/general/php.html) compile && install php, or use [oneinstack](https://oneinstack.com/install/) to install it

```
mkdir -p ~/src/zblog ~/work/run/zblog &&
wget -O ~/src/zblog/zblog.zip https://www.zblogcn.com/program/zblogphp15/ &&
unzip ~/src/zblog/zblog.zip -d ~/work/run/zblog
```

```
php -S 0000:1997 -t .
```

```
echo "[Unit]
Description=zblog
After=network.target

[Service]
ExecStart=/usr/bin/php -S 0000:1997 -t /home/pi/work/run/zblog
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target " | sudo tee /etc/systemd/system/zblog.service
```

