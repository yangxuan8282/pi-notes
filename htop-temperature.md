htop-2.0.2
===

raspberry pi:

```
mkdir -p ~/src/htop &&
wget -O ~/src/htop/htop_2.0.2-2_armhf.deb.zip https://github.com/wbenny/htop/files/573914/htop_2.0.2-2_armhf.deb.zip &&
unzip ~/src/htop/htop_2.0.2-2_armhf.deb.zip -d ~/src/htop &&
pushd ~/src/htop &&
    ar vx htop_2.0.2-2_armhf.deb && 
popd &&
sudo tar --extract --file=$HOME/src/htop/data.tar.xz -C /usr/local/bin/ --strip 3 ./usr/bin/htop
```