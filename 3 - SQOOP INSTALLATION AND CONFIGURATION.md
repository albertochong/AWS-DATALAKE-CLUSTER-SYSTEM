# SQOOP Installation and Configuration
System for bulk data transfer between HDFS and structured datastores as RDBMS. Like Flume but from HDFS to RDBMS.

### Run in terminal(NameNode or another server) with user hadoop

* Download Sqoop under home/user directory
```bash
cd /opt
sudo wget https://www-eu.apache.org/dist/sqoop/1.4.7/sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz
```

* unpack files
```bash
sudo tar -xzf sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz 
```

* move to folder opt/sqoop and change owner to group and user hadoop
```bash
sudo mv sqoop-1.4.7.bin__hadoop-2.6.0/ /opt/sqoop
sudo chown -R hadoop:hadoop sqoop/
```

*  add sqoop envirnoment variables under home/user
```bash
nano .bash_profile
# SQOOP
export SQOOP_HOME=/opt/sqoop
export HCAT_HOME=/opt/sqoop/hcatalog
export ACCUMULO_HOME=/opt/sqoop/accumulo
export PATH=$PATH:$SQOOP_HOME/bin
```

* renitialize/Activate
```bash
source .bash_profile
```

* Inside folder sqoop create directoryr accumulo and hcatalog because sqoop need them
```bash
mkdir accumulo
mkdir hcatalog
```

* Go to /sqoop/conf to edit sqoop-env.sh
```bash
nano sqoop-env.sh
#Set path to where bin/hadoop is available
export HADOOP_COMMON_HOME=/opt/hadoop

#Set path to where hadoop-*-core.jar is available
export HADOOP_MAPRED_HOME=/opt/hadoop

#set the path to where bin/hbase is available
#export HBASE_HOME=/opt/hbase

#Set the path to where bin/hive is available
export HIVE_HOME=/opt/hive

#Set the path for where zookeper config dir is
#export ZOOCFGDIR=/opt/zookeeper/conf
```

* checking sqoop installation running
```bash
sqoop version 
```

