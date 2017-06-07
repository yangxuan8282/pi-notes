Caddy
===

```
curl https://getcaddy.com | bash
```

for more plugins, go to offical [download page](https://caddyserver.com/download)

`systemd` template:

**/etc/systemd/system/$APP.service**

```
[Unit]
Description=$APP_NAME
After=network.target

[Service]
WorkingDirectory=$WORKDIR
ExecStart=/usr/local/bin/caddy -port $PORT
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target
```
