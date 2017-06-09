jdk-1.8.0.131
===

```
mkdir -p ~/src/jdk/8-jdk &&
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" -O ~/src/jdk/8-jdk/jdk.tar.gz http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-arm32-vfp-hflt.tar.gz &&
sudo tar --extract --file=$HOME/src/jdk/jdk-8u131-linux-arm32-vfp-hflt.tar.gz -C /opt/
```

```
echo "
# Set JAVA_HOME directory
export JAVA_HOME=/opt/jdk1.8.0_131

# Set JRE_HOME directory
export JRE_HOME=\$JAVA_HOME/jre

# Adjust PATH
export PATH=$PATH:\$JAVA_HOME:\$JRE_HOME" | tee --append ~/.bashrc
```