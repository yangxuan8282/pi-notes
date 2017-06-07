mdwiki
===

```
mkdir -p ~/work/run/mdwiki &&
wget -O ~/work/run/mdwiki/index.html https://raw.githubusercontent.com/Dynalon/mdwiki/gh-pages/index.html
```

create and edit `index.md`

then install a web server, and start the service

```
echo "[Unit]
Description=mdwiki
After=network.target

[Service]
WorkingDirectory=$HOME/work/run/mdwiki
ExecStart=/usr/local/bin/caddy -port 1998
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target " | sudo tee /etc/systemd/system/mdwiki.service
```
