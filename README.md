# AWS - DATALAKE - SYSTEM
Create DATALAKE with Apache Hadoop and Ecosystem - Instalation, configuration on 3 AWS machines


# Hadoop Installation on AWS
This guide describes to do manually setup one DATALAKE cluster with Hadoop on AWS 3 Red Hat Linux 8 machines new big data environment Apache Hadoop ecosystem for the purpose learn mains concepts from begin 


## Create 3 Instance (t2.Xlarge) with the options
* AMI: Amazon Linux 2 AMI (HVM), SSD Volume Type 64 bit
* Network: vpc by default + No precense subnet + Public IP Use subnet  setting (enable)
* Storage: Root disk 40 GB + Add Volume 100GB Magnetic (delete on termination)
* Use security group created (ClsChongNameNodeGroup)
* Create or use new .pem key (copy this file in a secure place)

## Security

### Create a Security Group

* Create new security group with the name: ClsChongNameNodeGroup
```bash
Type              Protocol        Port        Source

All Traffic       All             0 - 65535   Anywhere   

SSH               TCP             22          Anywhere
```

## 1. Step: Install some tools
  * Install wget
  * Install nano
  * Install gedit
  * Install Anaconda
  * Install SSH
  * Install Java

## 2. Step: Hadoop Installation and Configuration
  * Install and Configure Hadoop NameNode and DataNode 
  
### 2.1 Step: Working with HDFS
  * List files 
  * Create directory
  * copy files 
  
## 3. Step: Sqoop Installation and Configuration
  * Install and Configure Sqoop

### 3.1. Step: Import data from PostgreSql to HDFS
  * Download connector JDBC for PostgreSql        
  * Copy .jar to lib sqoop folder  
  * Connect to PostgreSql and list tables from Database 
  * Connect to PostgreSql and import Data to HDFS 
  
## 4. Step: Flume Installation and Configuration
  * Install and Configure Flume

### 4.1. Step: Import data from Twitter to HDFS
  *  Configure Agent(Source - Channel - Sink)
  *  Create Twitter App
  *  Starting agent and capture twitts real time and store in HDFS
 
## 5. Step: HIVE Installation and Configuration
  * Install and Configure HIVE
  
### 5.1. Step: Working with Hive
  *  Create table from HFDS files -------- NOT FINISHED YET
  *  
  *  
  
## 6. Step: HBASE Installation and Configuration
  * Install and Configure HBASE
  
### 6.1. Step: Working with HBASE
  *  
  *  
  *  
  
## 7. Step: KAFKA Installation and Configuration
  * Install and Configure KAFKA
  
### 7.1. Step: Working with KAFKA
  *  
  *  
  *  
  
## 8. Step: TEZ Installation and Configuration
  * Install and Configure TEZ
  
  
## Step: Install HUE
  * Install PostgreSql ----------------- NOT FINISHED
  * Install Hive------------------------ NOT FINISHED
  
## Step: Install AMBARI ----------------- NOT FINISHED
  * 
  
 

