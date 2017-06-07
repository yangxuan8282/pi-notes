Ran-0.1.3
---

```
mkdir -p ~/src/ran/src
```

```
cat >> ~/src/ran/make.sh << "EOF"
#!/bin/bash
#
# This script will build the executable and leave it in `./src`


IMAGE=yangxuan8282/golang:alpine
SRCDIR=/go/src/github.com/m3ng9i/ran

mkdir -p ~/src/ran/src 
wget -O ~/src/ran/v0.1.3.tar.gz https://github.com/m3ng9i/ran/archive/v0.1.3.tar.gz 
tar -xvf ~/src/ran/v0.1.3.tar.gz --strip 1 -C ~/src/ran/src 
docker $DOCKER_OPTIONS run -t --rm -v "$PWD"/src:$SRCDIR -v "$PWD"/build.sh:/build.sh -e SRCDIR=${SRCDIR} -e GOOS=${GOOS:-linux} -e GOARCH=${GOARCH:-arm} -e CGO_ENABLED=${CGO_ENABLED:-0} -w $SRCDIR $IMAGE sh /build.sh 
EOF
```

```
cat >> ~/src/ran/build.sh << "EOF"
#!/bin/sh

apk add --no-cache bash build-base git
go get github.com/m3ng9i/ran
cd ${SRCDIR}
go build .
EOF
```

```
pushd ~/src/ran &&
bash ~/src/ran/make.sh &&
popd 
```
