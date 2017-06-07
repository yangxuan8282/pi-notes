h5ai
===

### FROM

https://github.com/lrsjng/h5ai/issues/571

### RUN

follow [BLFS](http://www.linuxfromscratch.org/blfs/view/stable/general/php.html) compile && install php, or use [oneinstack](https://oneinstack.com/install/) to install it

```
mkdir -p ~/src/h5ai ~/work/run/h5ai &&
wget -O ~/src/h5ai/h5ai.zip https://release.larsjung.de/h5ai/h5ai-0.29.0.zip &&
unzip ~/src/h5ai/h5ai.zip -d ~/work/run/h5ai
```

```
cat >> ~/work/run/h5ai/_h5ai/router.php << "EOF"
<?php
// full path of requested file
$path = dirname(__DIR__) . preg_replace('/\?(.*)/', '', $_SERVER['REQUEST_URI']);

// h5ai is required when user request a directory
if(file_exists($path) && is_dir($path))
{
    // directory must not contain index.php or index.html
    if(file_exists("$path/index.php") == false && file_exists("$path/index.html") == false)
    {
        // script name must be "tweaked" to detect path
        $_SERVER['SCRIPT_NAME'] = '/_h5ai/public/index.php';

        include __DIR__ . "/public/index.php";
        exit;
    }
}

// CSS is sent with text/html content type, so we need to fix it
if($path == __DIR__ . '/public/css/styles.css')
{
    header('Content-Type: text/css');
}

// return resource "as-is"
return false;
EOF
```

```
php -S 0000:1995 ~/work/run/h5ai/_h5ai/router.php
```

```
echo "[Unit]
Description=h5ai
After=network.target

[Service]
WorkingDirectory=$HOME/work/run/h5ai
ExecStart=/usr/bin/php -S 0000:1995 _h5ai/router.php
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target " | sudo tee /etc/systemd/system/h5ai.service
```
