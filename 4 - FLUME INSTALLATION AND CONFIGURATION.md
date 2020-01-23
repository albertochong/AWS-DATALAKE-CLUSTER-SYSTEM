
# FLUME Installation and Configuration
According Apache Flume is a distributed, reliable, and available service for efficiently collecting, aggregating, and moving large amounts of log data. It has a simple and flexible architecture based on streaming data flows. It is robust and fault tolerant with tunable reliability mechanisms and many failover and recovery mechanisms. It uses a simple extensible data model that allows for online analytic application.

### Run in terminal(NameNode or another server) with user hadoop

* Download Flume under home/hadoop directory
```bash
cd /opt
sudo wget https://www-us.apache.org/dist/flume/1.9.0/apache-flume-1.9.0-bin.tar.gz
```

* unpack files
```bash
 sudo tar -xvf apache-flume-1.9.0-bin.tar.gz 
```

* rename folder apache-flume-1.9.0-bin to flume and change owner to group and user hadoop
```bash
sudo mv apache-flume-1.9.0-bin/ flume
sudo chown -R hadoop:hadoop flume/
```

*  add flume envirnoment variables under home/hadoop
```bash
nano cd ~/.bash_profile
# FLUME
export FLUME_HOME=/opt/flume
export PATH=$PATH:$FLUME_HOME/bin
```

* renitialize/Activate
```bash
source .bash_profile
```

* Go to /$FLUME_HONE/conf to edit flume-env.sh and uncomment and set correct path
```bash
cp flume-env.sh.template flume-env.sh
nano $FLUME_HONE/conf/sqoop-env.sh
export JAVA_HOME=/opt/jdk
FLUME_CLASSPATH="opt/flume/lib/*"
```

 



