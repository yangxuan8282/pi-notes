kodexplorer
===

follow [BLFS](http://www.linuxfromscratch.org/blfs/view/stable/general/php.html) compile && install php, or use [oneinstack](https://oneinstack.com/install/) to install it

```
mkdir -p ~/src/kodexplorer ~/work/run/kodexplorer &&
wget -O ~/src/kodexplorer/kodexplorer.zip http://static.kalcaddle.com/update/download/kodexplorer3.46.zip &&
unzip ~/src/kodexplorer/kodexplorer.zip -d ~/work/run/kodexplorer
cd ~/work/run/kodexplorer &&
chmod -Rf 777 ./*
```

```
php -S 0000:1996 -t .
```

> [WARNING] `admin` user permissions are too open, when you login in with `admin` you can edit any files on your machine, so you should set `open_basedir`

```
echo "[Unit]
Description=kodexplorer
After=network.target

[Service]
ExecStart=/usr/bin/php -S 0000:1996 -t /home/pi/work/run/kodexplorer
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target " | sudo tee /etc/systemd/system/kodexplorer.service
```
