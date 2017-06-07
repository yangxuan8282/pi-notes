leanote
===

### FROM

https://github.com/leanote/leanote/wiki/Leanote%E5%BC%80%E5%8F%91%E7%89%88%E5%9C%A8Cubieboard%E4%B8%8A%E8%AF%A6%E7%BB%86%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B

https://github.com/leanote/leanote/wiki/leanote-binary-installation-on-Mac-and-Linux-(En)

### RUN

```
sudo apt install git mongodb golang
```

```
mkdir ~/work/leanote &&
cd ~/work/leanote
```

```
wget -O ~/work/leanote/leanote-linux-arm-v2.4.bin.tar.gz https://sourceforge.net/projects/leanote-bin/files/2.4/leanote-linux-arm-v2.4.bin.tar.gz/download
```

```
tar xf leanote-linux-arm-v2.4.bin.tar.gz &&
rm -rf *.tar.gz 
```

```
mongorestore -h localhost -d leanote --dir ~/work/leanote/leanote/mongodb_backup/leanote_install_data/
```

type:

```
mongo
```

then:

```
use leanote 
```

```
exit
```

edit `/home/pi/work/leanote/leanote/conf/app.conf`

change url to yours

**/etc/systemd/system/leanote.service**

```
[Unit]
Description=Leanote
After=network.target

[Service]
ExecStart=/bin/bash /home/pi/work/leanote/leanote/bin/run.sh
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target
```

```
sudo systemctl start leanote.service &&
sudo systemctl enable leanote.service
```


