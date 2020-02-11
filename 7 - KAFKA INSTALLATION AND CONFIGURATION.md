# KAFKA Installation and Configuration

### Run in terminal in NODE MASTER

* Connect to NameNode and Download Kafka under home/hadoop directory
```bash
wget https://archive.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz
```

* unpack files
```bash
tar -xvf kafka_2.11-1.1.0.tgz
```

* move to folder opt/kafka and change ownner
```bash
sudo mv kafka_2.11-1.1.0/ /opt/kafka 
sudo chown -R hadoop:hadoop /opt/kafka/
```

* Add kafka envirnoment variables under home/hadoop
```bash  
nano .bash_profile
 
# KAFKA
export KAFKA_HOME=/opt/kafka
export PATH=$PATH:$KAFKA_HOME/bin
```     

* Renitialize/Activate
```bash   
source .bash_profile
``` 

* Check if folder zookeeper is there means zookeeper is already installed
```bash   
cd /opt/kafka/libs
``` 
