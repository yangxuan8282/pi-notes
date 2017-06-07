Syncthing-0.14.29
===

```
mkdir -p ~/src/syncthing &&
wget -O ~/src/syncthing/syncthing.tar.gz https://github.com/syncthing/syncthing/releases/download/v0.14.29/syncthing-linux-arm-v0.14.29.tar.gz &&
sudo tar --extract --file=$HOME/src/syncthing/syncthing.tar.gz -C /usr/local/bin/ --strip=1 syncthing-linux-arm-v0.14.29/syncthing
```

```
syncthing
```

```
sed -i "s/127.0.0.1/0.0.0.0/g" ~/.config/syncthing/config.xml
```

then visit: $SERVER_IP:8384

`systemd` template:

```
echo "[Unit]
Description=Syncthing - Open Source Continuous File Synchronization 
After=network.target

[Service]
User=$(whoami)
ExecStart=/usr/local/bin/syncthing -no-browser -no-restart -logflags=0
Restart=on-failure
SuccessExitStatus=3 4
RestartForceExitStatus=3 4

[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/syncthing.service
```
