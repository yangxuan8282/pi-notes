aria2-1.32.0
===

```
mkdir -p ~/src/aria2/1.32.0/src ~/.config/aria2 &&
wget -O ~/src/aria2/1.32.0/aria2.tar.bz2 https://github.com/q3aql/aria2-static-builds/releases/download/v1.32.0/aria2-1.32.0-linux-gnu-arm-rbpi-build1.tar.bz2 &&
tar -jxvf ~/src/aria2/aria2.tar.bz2 --strip 1 -C ~/src/aria2/1.32.0/src &&
pushd ~/src/aria2/1.32.0/src &&
sudo make install &&
popd 
```

```
echo "continue=true
dir=$HOME/dl
input-file=$HOME/.config/aria2/session.lock
#max-concurrent-downloads=3
max-connection-per-server=5
bt-enable-lpd=true
bt-require-crypto=true
listen-port=65298
dht-listen-port=65298
seed-time=120
enable-rpc=true
rpc-allow-origin-all=true
rpc-listen-all=true
rpc-listen-port=6800
disable-ipv6=true
file-allocation=none
save-session=$HOME/.config/aria2/session.lock
save-session-interval=300" | tee ~/.config/aria2/aria2.conf 
```

```
touch ~/.config/aria2/session.lock
```

`systemd` template:

```
echo "[Unit]
Description=Aria2 Service
After=network.target

[Service]
User=$(whoami)
ExecStart=/usr/bin/aria2c --enable-rpc --rpc-listen-all --rpc-allow-origin-all --conf-path=$HOME/.config/aria2/aria2.conf
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/aria2.service
```
