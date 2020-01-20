
# Hadoop Installation and Configuration in Cluster Mode 

## Run in terminal
* Create new user for hadoop installation on 3 instances
```bash
sudo useradd -m hadoop
sudo passwd hadoop 
```

* Add user hadoop on file /etc/sudoers
```bash
sudo nano /etc/sudoers
hadoop ALL=(ALL)  ALL
```

* reboot server
```bash
sudo reboot
```

* Download Hadoop under home/use directory
```bash
wget https://www-eu.apache.org/dist/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz
```
* unpack files
```bash
tar -xzf hadoop-3.2.1.tar.gz
```
* Move to folder opt/hadoop
```bash
sudo mv hadoop-3.2.1/ /opt/hadoop
```   
* Add some envirnoment variables under home/user
```bash
nano .bashrc
# HADOOP
     export HADOOP_HOME=/opt/hadoop
     export HADOOP_INSTALL=$HADOOP_HOME
     export HADOOP_COMMON_HOME=$HADOOP_HOME
     export HADOOP_MAPRED_HOME=$HADOOP_HOME
     export HADOOP_HDFS_HOME=$HADOOP_HOME
     export YARN_HOME=$HADOOP_HOME
     export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
``` 
*  renitialize to activate new variables
```bash
source .bashrc
``` 
*  Check hadoop version if installed sucessfully
```bash
hadoop version
``` 

* Create 3 folder to change hadoop behavior 
```bash
mkdir /opt/hadoop/dfs
mkdir /opt/hadoop/dfs/data ---------------> to save data
mkdir /opt/hadoop/dfs/namespace_logs------> to save metadata on namenodes.All folders is on same machine because this is pseudo mode, if we have cluster we created /opt/hadoop/dfs/data on datanodes machine and                                                                         /opt/hadoop/dfs/namespace_logs in namenode and secondaryname nodes machines
``` 

* Let´s go to hadoop folder /opt/hadoop/etc/hadoop.Edit core-site.xml and add this configuration.Run Terninal:
```bash 
cd /opt/hadoop/etc/hadoop
nano core-site.xml
   <configuration>
    <!-- HDFS PATH -->
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
   </configuration>
```
* Edit hdfs-site.xml and add this configuration.Run Terninal: 
```bash
nano hdfs-site.xml
   <configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value> <!-- if we have more machines in cluster we can put value 3 to replicate at least 3 blocks of data , one each machines. Fault tolerance-->
    </property>
    <property>
      <name>dfs.namenode.name.dir</name>
      <value>/opt/hadoop/dfs/namespace_logs</value>
    </property>
    <property>
      <name>dfs.datanode.data.dir</name>
      <value>/opt/hadoop/dfs/data</value>
    </property>
    <property>
      <name>dfs.namenode.checkpoint.dir</name>
      <value>/opt/hadoop/dfs/namesecondary</value>
    </property>
   </configuration>
```
* Let´s Setup passphraseless ssh (ssh without credentials)
  Note: Suppose we have cluster with 300 machines, 1 namenodes, 1 secondnamenodes and 298 datanodes.
        We don´t neeed configure 300 user and password, so we use ssh to make comunication between master and datanodes
        SSH is an security protocol encrypted, we configure key pairs, private and public.
        The private key is stored in masternode and we copy public keys to all existing datanodes.
```bash
     1 - Go to home/user and run:
     ssh-keygen -t rsa -----> to generate key with RSA crytography and will stored in /home/ec2-user/.ssh/id_rsa if you accepted
     
     2 - Moving generated content key public to authorized_keys file
     cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
     
     3 - Testing SSH connection. Run terminal
     ssh localhost
     
     4 - If the system ask for password something is wrong because we Setup passphraseless above. By default SSH give previleges only to
          root account, so if you are logged with another user you should add this user to ssh config file.
          Run terminal:
     sudo nano etc/ssh/sshd_config
      - add this property : AllowUsers xxxx
      
     5 -  After reinitialize service ssh in terminal
      sudo systemctl restart sshd
 ```   
 * Preparing system files
 ```bash
 hdfs namenode -format 
 Check for message like Storage directory /tmp/hadoop-ec2-user/dfs/name has been successfully formatted.
 ---
 
* Starting hdfs
```bash
 start-dfs.sh
 stop-dfs.sh -----------------> stop hdfs if you want
--- 

* YARN configurion(Resource Manager).Let´s go to hadoop folder /opt/hadoop/etc/hadoop
```bash
   1- edit mapred-site.xml and add this configuration.Run Terninal : 
      cd /opt/hadoop/etc/hadoop
      nano mapred-site.xml
      <configuration>
         <property>
            <name>mapreduce.framework.name</name>
            <value>yarn</value>
         </property>
         <property>
            <name>mapreduce.application.classpath</name>
            <value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value>
         </property>
      </configuration>
 
   2- edit yarn-site.xml and add this configuration.Run Terninal : 
      nano yarn-site.xml
      <configuration>
         <property>
            <name>yarn.nodemanager.aux-services</name>
            <value>mapreduce_shuffle</value>
         </property>
         <property>
            <name>yarn.nodemanager.env-whitelist</name>
     <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
         </property>
      </configuration>

   3 - jps ------------> checking services.If hadoop services is not running you must start
   
   4 - start-yarn.sh ----- > starting yarn
       stop-yarn.sh ----- > stop yarn if you want
 ---      
 
 NOTE: 
       1 - if you doesn't change hadoop parameter cnfiguration it´s will assume default configuration and save on temporary folder tmp
           Hadoop Oficial doc : https://hadoop.apache.org/docs/stable/index.html
           
       2 - Check hadoop logs in opt/hadoop/logs if any error come up. If you want to remove some logs files in terminal run
           rm -rf * ------> run inside logs folder
           
       3 - you can format namenode again or drop all content inside folder tmp/hadoop-xxxxxx if any problem occurs but not 
           in production environment

       4 - Check my namenode on : http://3.227.30.97:9870/
