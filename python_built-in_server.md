python built-in server
---

follow [BLFS](http://www.linuxfromscratch.org/blfs/view/stable/general/python2.html) to install python2 first

then cd to dir and simple run:

```
python -m SimpleHTTPServer
```

there is a version from github user [@ksmith97](https://github.com/ksmith97), which support gzip

download the script with:

```
sudo wget -O /usr/local/bin/gzsimpleserver https://raw.githubusercontent.com/ksmith97/GzipSimpleHTTPServer/master/GzipSimpleHTTPServer.py 
```

then you can run it with:

```
gzsimpleserver
```

> make sure `/usr/local/bin` is in your $PATH

`systemd` template:

**/etc/systemd/system/$APP.service**

```
[Unit]
Description=$APP_NAME
After=network.target

[Service]
WorkingDirectory=$WORKDIR
ExecStart=/usr/local/bin/gzsimpleserver --port $PORT
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target
```

> change `$APP_NAME` to your service name \
>        `$WORKDIR` to correct working directory (absolute path) \
>        `$PORT` to the port you want to use

> [TIPS] create compressed file like this: `gzip --keep index.html`, and keep the original file
