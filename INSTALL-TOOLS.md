# Installing Tools 
### Tools
* unzip
* gedit
* wget
* nano
* Anaconda
 
## Run in terminal
* Install bzip2
```bash
sudo yum install bzip2
```
* Install unzip
```bash
sudo yum install unzip
```
* Install wget
```bash
sudo yum install rsync wget net-tools
```
* Install nano
```bash
sudo yum install nano
```

## Install SSH(Secure Shell) We need SSH protocol to enable comunication between servers in the cluster 
### Run in terminal
* Install SSH
```bash
 sudo yum install openssh-server openssh-clients  
``` 
* Enable SSH
```bash 
sudo systemctl enable sshd
``` 
* Start SSH
```bash 
sudo systemctl start sshd
``` 
* Check status SSH
```bash 
sudo systemctl status sshd
``` 
* Change SSH configuration file ssh_config under home/user directory.Uncommnet this properties
```bash
sudo nano /etc/ssh/sshd_config
Uncomment Port 22
ListenAddress 0.0.0.0
 ``` 
* Restart SSH service          
```bas
sudo systemctl restart sshd           
``` 
    
## Install Java Virtual machine.Hadoop needs jdk to work 
### Run in terminal
* Check if java is installed
```bash 
java -version 
or
sudo yum list java*
``` 
* Remove all openjdk packages
```bash 
sudo yum remove java*
``` 
* (Download Java) under home/user directory
```bash 
wget -c --content-disposition "https://javadl.oracle.com/webapps/download/AutoDL?BundleId=239835_230deb18db3e4014bb8e3e8324f81b43"
```
* Unpack 
```bash 
sudo tar xzf java_package_name
```
*  Move folder jdk1.8.0_221 to opt/jdk
```bash 
sudo mv jdk1.8.0_221/ /opt/jdk
```
*  Edit .bashrc Under home/user directory to create envirnoment variable for java and add
```bash 
nano .bashrc
  export JAVA_HOME=/opt/jdk
  export PATH=$PATH:$JAVA_HOME/bin
```
* Reactive and update and read news environment variable
```bash 
source .bashrc
```
* To confirm java installation
```bash 
java -version 
```    
* Install Anaconda
  * Download Anaconda
   ```bash
   wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
   ```
  * Install Anaconda 
   ```bash 
   bash Anaconda3-2019.10-Linux-x86_64.sh
   ```
  *  Edit .bashrc Under home/user directory to create envirnoment variable and inform spark to work with jupyter notebook
   ```bash 
   nano .bashrc
   export PYSPARK_DRIVER_PYTHON=jupyter
   export PYSPARK_DRIVER_PYTHON_OPTS=notebook
   export PYSPARK_PYTHON=python3
   ```
  * Reactive and update and read news environment variable
   ```bash 
   source .bashrc
   ```
