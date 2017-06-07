seafile
===

```
mkdir -p ~/work/seafile &&
cd ~/work/seafile &&
wget https://github.com/haiwen/seafile-rpi/releases/download/v6.1.0/seafile-server_6.1.0_beta_pi.tar.gz &&
tar xf *.tar.gz &&
rm -rf *.tar.gz &&
cd ~/work/seafile/seafile-server-6.1.0 &&
./setup-seafile.sh auto -n pi-seafile -i $URL -p 8082 -d 
```

```
./seafile.sh start 
```

```
./seahub.sh start
```

**/etc/systemd/system/seafile.service**

```
[Unit]
Description=Seafile
After=network.target

[Service]
Type=oneshot
ExecStart=/home/pi/work/seafile/seafile-server-6.1.0/seafile.sh start
ExecStop=/home/pi/work/seafile/seafile-server-6.1.0/seafile.sh stop
RemainAfterExit=yes
User=pi

[Install]
WantedBy=multi-user.target
```

**/etc/systemd/system/seahub.service**

```
[Unit]
Description=Seafile hub
After=network.target seafile.service

[Service]
Type=oneshot
ExecStart=/home/pi/work/seafile/seafile-server-6.1.0/seahub.sh start
ExecStop=/home/pi/work/seafile/seafile-server-6.1.0/seahub.sh stop
RemainAfterExit=yes
User=pi

[Install]
WantedBy=multi-user.target
```

```
sudo systemctl start seafile &&
sudo systemctl start seahub &&
sudo systemctl enable seafile seahub 
```

frpc template config

```
[seafile]
type = http
local_port = 8082
use_gzip = true
subdomain = fileserver

[seahub]
type = http
local_port = 8000
use_gzip = true
subdomain = file
```

then change `SERVICE_URL` && `FILE_SERVER_ROOT` in seahub

if use same subdomain as the frpc config above, change them to `file.mydomain.com` and `fileserver.mydomain.com`

