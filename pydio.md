Pydio-8.0.0
===


### Dependencies

[MariaDB](http://www.linuxfromscratch.org/blfs/view/stable/server/mariadb.html)/MySQL
[PHP](http://www.linuxfromscratch.org/blfs/view/stable/general/php.html)

### RUN

```
mkdir -p ~/src/pydio ~/work/run/pydio &&
wget -O ~/src/pydio/pydio.tar.gz https://download.pydio.com/pub/core/archives/pydio-core-8.0.0.tar.gz &&
tar --extract --file=$HOME/src/pydio/pydio.tar.gz -C $HOME/work/run/pydio --strip 1
```

