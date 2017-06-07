Node-6.10.3
===

armv7l:

```
mkdir -p ~/src/node/6.10 &&
wget -O ~/src/node/6.10/node.tar.xz https://nodejs.org/dist/v6.10.3/node-v6.10.3-linux-armv7l.tar.xz &&
sudo tar --extract --file=$HOME/src/node/6.10/node.tar.xz -C /usr/ --strip 1
```

amd64:

```
mkdir -p ~/src/node/6.10 &&
wget -O ~/src/node/6.10/node.tar.xz https://nodejs.org/dist/v6.10.3/node-v6.10.3-linux-x64.tar.xz &&
sudo tar --extract --file=$HOME/src/node/6.10/node.tar.xz -C /usr/ --strip 1  
```
