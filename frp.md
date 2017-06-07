frp-0.11.0
===

### HOME

https://github.com/fatedier/frp

### RUN

server:

```
mkdir -p ~/src/frp ~/.config/frp &&
wget -O ~/src/frp/frp.tar.gz https://github.com/fatedier/frp/releases/download/v0.11.0/frp_0.11.0_linux_amd64.tar.gz &&
sudo tar --extract --file=$HOME/src/frp/frp.tar.gz -C /usr/local/bin/ --strip=1 frp_0.11.0_linux_amd64/frps
```

> replace `$TOKEN` and `$DOMAIN_NAME` with yours

```
cat >> ~/.config/frp/frps.ini << "EOF"
# frps.ini
[common]
bind_port = 7000
vhost_http_port = 80
privilege_token = $TOKEN
subdomain_host = $DOMAIN_NAME
EOF
```

```
echo "[Unit]
Description=frp server
After=network.target

[Service]
User=$(whoami)
ExecStart=/usr/local/bin/frps -c $HOME/.config/frp/frps.ini
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/frps.service
```

client:

```
mkdir -p ~/src/frp ~/.config/frp &&
wget -O ~/src/frp/frp.tar.gz https://github.com/fatedier/frp/releases/download/v0.11.0/frp_0.11.0_linux_arm.tar.gz &&
sudo tar --extract --file=$HOME/src/frp/frp.tar.gz -C /usr/local/bin/ --strip=1 frp_0.11.0_linux_arm/frpc
```

> replace `$SERVER_IP`, `$TOKEN`, `$PORT`, `$PREFIX` with yours

```
cat >> ~/.config/frp/frpc.ini << "EOF"
# frpc.ini
[common]
server_addr = $SERVER_IP
server_port = 7000
privilege_token = $TOKEN

[$APP1_NAME]
type = http
local_port = $PORT1
use_gzip = true
subdomain = $PREFIX1

[$APP2_NAME]
type = http
local_port = $PORT2
use_gzip = true
subdomain = $PREFIX2
EOF
```

```
echo "[Unit]
Description=frp client
After=network.target

[Service]
User=$(whoami)
ExecStart=/usr/local/bin/frpc -c $HOME/.config/frp/frpc.ini
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/frpc.service
```

