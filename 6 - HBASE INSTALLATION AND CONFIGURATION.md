
# Hbase Non Relational Database Installation and Configuration
Use Apache HBase™ when you need random, realtime read/write access to your Big Data. This project's goal is the hosting of very large tables -- billions of rows X millions of columns -- atop clusters of commodity hardware. Apache HBase is an open-source, distributed, versioned, non-relational database modeled after Google's Bigtable

### Run in terminal in NODE MASTER

* Connect to NameNode and Download Hbase under home/hadoop directory
```bash
wget https://www-us.apache.org/dist/hbase/2.1.8/hbase-2.1.8-bin.tar.gz
```

* unpack files
```bash
tar -xvf hbase-2.1.8-bin.tar.gz 
```

* move to folder opt/Hbase and change ownner
```bash
sudo mv hbase-2.1.8/ /opt/hbase 
sudo chown -R hadoop:hadoop /opt/hbase/
```

* Add hbase envirnoment variables under home/hadoop
```bash  
nano .bash_profile
 
# HBASE
export HBASE_HOME=/opt/hbase
export PATH=$PATH:$HBASE_HOME/bin
export CLASSPATH=$CLASSPATH:/opt/hbase/lib/*:.
   
```     

* Renitialize/Activate
```bash   
source .bash_profile
``` 

* Create directory to HBASE in HDFS
```bash   
hdfs dfs -mkdir /hbase
``` 

* Create directory zookepper if no exists
```bash   
mkdir /opt/zookepper
``` 

* Go to /hbase/conf to edit hbase-env.sh
```bash
nano /opt/hbase/confhbase-env.sh 
-------------- let´s uncommnet JAVA_HOME line and set our directory
export JAVA_HOME=/opt/jdk
# Tell HBase whether it should manage it's own instance of ZooKeeper or not.
export HBASE_MANAGES_ZK=true
``` 
 
* Go to /hbase/conf to edit hbase-site.xml
```bash
nano /opt/hbase/conf/hbase-site.xml -------------- let´s add some configurations

<configuration>

  <property>
    <name>hbase.rootdir</name>
    <value>hdfs://ip-172-31-8-80.us-east-2.compute.internal:19000/hbase</value>><!-- NameNode dns -->
    <description>The directory on NameNode shared  by RegionServers.
    </description>
  </property>

  <property>
    <name>hbase.cluster.distributed</name>
    <value>true</value>
    <description>The mode the cluster will be in. Possible values are false:
      standalone and pseudo-distributed setups with managed ZooKeeper , true: fully-distributed with unmanaged ZooKeeper Quorum (see
      hbase-env.sh)
    </description>
  </property>


  <property>
     <name>hbase.zookeeper.property.dataDir</name>
     <value>/home/hadoop/zookeeper</value>
  </property>

  <property>
     <name>hbase.zookeeper.quorum</name>
     <value>ip-172-31-8-80.us-east-2.compute.internal</value><!-- NameNode dns -->
  </property>

  <property>
    <name>hbase.zookeeper.property.clientPort</name>
    <value>2181</value>
  </property>

</configuration>

```


* edit file regionservers and add yours RegionServes.It will be the DataNodes 1 and 2
```bash
nano /opt/hbase/conf/regionservers
dns_dataNode1
dns_Datanode2
```







* Inside folder hbase create directoryr hfiles(directory to database files)
```bash
mkdir hfiles
```




* checking if hdfs,zookeeper and yarn services are online. If not, you must start
```bash
jps
```

* starting hbase
```bash
start-hbase.sh
```

* starting shell
```bash
hbase shell
```
