Go-1.8.3
===

```
mkdir -p ~/src/golang/1.8 ~/go/{src,pkg,bin} &&
wget -O ~/src/golang/1.8/golang.tar.gz https://storage.googleapis.com/golang/go1.8.3.linux-armv6l.tar.gz &&
sudo tar -C /usr/local -xzf ~/src/golang/1.8/golang.tar.gz
```

```
echo "
export PATH=$PATH:/usr/local/go/bin" | sudo tee --append /etc/profile
```

```
echo "
export GOPATH="$HOME"/go
export PATH="$PATH":"$GOROOT"/bin:"$GOPATH"/bin" | tee --append ~/.bashrc 
```

```
source /etc/profile
``` 

```
source ~/.bashrc
```
