Shadowsocks Go-1.2.1
===

```
mkdir -p ~/src/ss-go ~/.config/ss &&
wget -O ~/src/ss-go/ss.tar.gz https://github.com/shadowsocks/shadowsocks-go/releases/download/1.2.1/shadowsocks-server.tar.gz &&
sudo tar -xvf $HOME/src/ss-go/ss.tar.gz -C /usr/local/bin/
```

```
cat >> ~/.config/ss/config.json << "EOF"
    {
        "server":"127.0.0.1",
        "server_port":8388,
        "local_port":1080,
        "password":"xxxx",
        "method": "aes-128-cfb-auth",
        "timeout":600
    }
EOF
```

```
shadowsocks-server -c ~/.config/ss/config.json
```
