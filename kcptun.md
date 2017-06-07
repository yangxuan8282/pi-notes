kcptun
===

server:

```
mkdir -p ~/src/kcptun ~/.config/kcp &&
wget -O ~/src/kcptun/kcptun.tar.gz https://github.com/xtaci/kcptun/releases/download/v20170525/kcptun-linux-amd64-20170525.tar.gz &&
sudo tar --transform='s,server_linux_amd64,kcp,' --extract --file=$HOME/src/kcptun/kcptun.tar.gz -C /usr/local/bin/ server_linux_amd64
```

```
kcp -t "127.0.0.1:$TARGET_PORT" -l ":$KCP_PORT"
```

```
cat >> ~/.config/kcp/kcp.ini << "EOF"
    {
        "listen":":$KCP_PORT",
        "target":"127.0.0.1:$TARGET_PORT"
    }
EOF
```

```
echo "[Unit]
Description=kcptun server
After=network.target

[Service]
User=$(whoami)
ExecStart=/usr/local/bin/kcp -c $HOME/.config/kcp/kcp.ini
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/kcp.service
```

client:

```
mkdir -p ~/src/kcptun ~/.config/kcp &&
wget -O ~/src/kcptun/kcptun.tar.gz https://github.com/xtaci/kcptun/releases/download/v20170525/kcptun-linux-arm-20170525.tar.gz &&
sudo tar --transform='s,client_linux_arm7,kcp,' --extract --file=$HOME/src/kcptun/kcptun.tar.gz -C /usr/local/bin/ client_linux_arm7
```

```
kcp -r "$KCP_SERVER_IP:$KCP_PORT" -l ":$TARGET_PORT"
```

```
cat >> ~/.config/kcp/kcp.ini << "EOF"
    {
        "remoteaddr":"$KCP_SERVER_IP:$KCP_PORT",
        "localaddr":":$TARGET_PORT"
    }
EOF
```

```
echo "[Unit]
Description=kcptun client
After=network.target

[Service]
User=$(whoami)
ExecStart=/usr/local/bin/kcp -c $HOME/.config/kcp/kcp.ini
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/kcp.service
```
