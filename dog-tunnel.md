Dog Tunnel lite-1.30
===

server:

```
sudo wget -O /usr/local/bin/dog-tunnel https://raw.githubusercontent.com/yangxuan8282/docker-image/master/dog-tunnel/lite_v1.30/amd64/dog-tunnel &&
sudo chmod a+x /usr/local/bin/dog-tunnel
```

`systemd` template:

```
echo "[Unit]
Description=Dog tunnel for http
After=network.target
[Service]
ExecStart=/usr/local/bin/dog-tunnel -service :$DTUNNEL_PORT -v -xor $XOR
Restart=always
RestartSec=60
[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/dtunnel-server.service
```

client:

```
sudo wget -O /usr/local/bin/dog-tunnel https://raw.githubusercontent.com/yangxuan8282/docker-image/master/dog-tunnel/lite_v1.30/arm/dog-tunnel &&
sudo chmod a+x /usr/local/bin/dog-tunnel
```

`systemd` template:

```
echo "#!/bin/bash
ssh -f -i $SSH_KEY $SERVER_SSH_USER@$SERVER_IP -p $SERVER_SSH_PORT "sudo systemctl restart dtunnel-server"
/usr/local/bin/dog-tunnel -service $SERVER_IP:$DTUNNEL_PORT -v -action 127.0.0.1:$LOCAL_PORT -encrypt -xor $XOR -local :$REMOTE_PORT -pipe 5 -r
" | sudo tee /usr/local/bin/dtunnel-up.sh
```

```
echo "#!/bin/bash
ssh -f -i $SSH_KEY $SERVER_SSH_USER@$SERVER_IP -p $SERVER_SSH_PORT "sudo systemctl stop dtunnel-server"
" | sudo tee /usr/local/bin/dtunnel-down.sh
```

```
sudo chmod +x /usr/local/bin/dtunnel-up.sh &&
sudo chmod +x /usr/local/bin/dtunnel-down.sh
```

```
echo "[Unit]
Description=Dog tunnel for http
After=network.target
[Service]
ExecStart=/usr/local/bin/dtunnel-up.sh
ExecStop=/usr/local/bin/dtunnel-down.sh
Restart=always
RestartSec=60
[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/http-dtunnel.service
```

