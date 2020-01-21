# AWS - DATALAKE - SYSTEM
Create DATALAKE with Apache Hadoop and Ecosystem - Instalation, configuration on 3 AWS machines


# Installation of Hadoop in AWS
This guide describes to do manually setup one DATALAKE cluster with Hadoop on AWS 3 Red Hat Linux 8 machines new big data environment Apache Hadoop ecosystem for the purpose learn mains concepts from begin 


## Create 3 Isntance (t2.Xlarge) with the options
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
  
## Step: Install HUE
  * Install PostgreSql ----------------- NOT FINISHED
  * Install Hive------------------------ NOT FINISHED
 

