php built-in server
===

follow [BLFS](http://www.linuxfromscratch.org/blfs/view/stable/general/php.html) compile && install php, or use [oneinstack](https://oneinstack.com/install/) to install it

cd to dir and run with:

```
php -S 0000:$PORT -t .
```

> change `$PORT` to the port you want to use

`systemd` template:

**/etc/systemd/system/$APP.service**

```
[Unit]
Description=$APP_NAME
After=network.target

[Service]
ExecStart=/usr/bin/php -S 0000:$PORT -t $PATH
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target
``` 
