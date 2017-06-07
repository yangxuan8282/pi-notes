Minio
===

```
mkdir -p ~/src/minio ~/files &&
wget -O ~/src/minio/minio https://dl.minio.io/server/minio/release/linux-arm/minio &&
sudo install -Dm755 ~/src/minio/minio /usr/local/bin/minio
```

```
minio server --address :2000 ~/files
```

`systemd` template:

```
echo "[Unit]
Description=Minio
After=network.target

[Service]
User=$(whoami)
ExecStart=/usr/local/bin/minio server --address :2000 $HOME/files
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target " | sudo tee /etc/systemd/system/minio.service
``` 

```
cat ~/.minio/config.json | grep "accessKey\|secretKey"
```

> the default config file locate in `~/.minio/config.json`
