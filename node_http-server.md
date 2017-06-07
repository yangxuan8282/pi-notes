node http-server
===

install node via [package manager](https://nodejs.org/en/download/package-manager/), or [binary file](node.md):

```
sudo npm install http-server -g
```

`systemd` template:

**/etc/systemd/system/$APP.service**

```
[Unit]
Description=$APP_NAME
After=network.target

[Service]
WorkingDirectory=$WORKDIR
ExecStart=/usr/bin/http-server -p $PORT
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target
```

