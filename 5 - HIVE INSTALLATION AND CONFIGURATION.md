
# HIVE Installation and Configuration
The Apache Hive ™ data warehouse software facilitates reading, writing, and managing large datasets residing in distributed storage using SQL. Structure can be projected onto data already in storage. A command line tool and JDBC driver are provided to connect users to Hive.

## Run in terminal(NameNode or another server) with user hadoop

### INSTALL HIVE
* Download Hive
```bash
cd /opt
sudo wget https://www-eu.apache.org/dist/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz
```

* Unpack files
```bash
sudo tar -xvf apache-hive-3.1.2-bin.tar.gz
```

* Move to appropriate folder
```bash
sudo mv apache-hive-3.1.2/ /opt/hive
```

* Add environment variable to accept hive
```bash
nano ~/.bash_profile
# HIVE
export HIVE_HOME=/opt/hive
export PATH=$PATH:$HIVE_HOME/bin
export CLASSPATH=$CLASSPATH:$HADOOP_HOME/lib/*:.
export CLASSPATH=$HIVE_HOME/lib/*:.
```

* renicializate system
```bash
source ~/.bash_profile
```

* Check hive version
```bash
hive --version
```

### INSTALL POSTGRESQL

* Install PostgreSql
```bash
sudo yum install postgresql postgresql-server -y
```

* Checking PostgreSql status
```bash
sudo systemctl status postgresql
```

* Enable PostgreSql
```bash
sudo systemctl enable postgresql
```

* Give permission to postgres /var/lib/pgsql/data
```bash
sudo chown -R postgres:postgres  /var/lib/pgsql
```

* start postgrsql
```bash
 sudo systemctl start postgresql
```

* Checking again PostgreSql status
```bash
sudo systemctl status postgresql
```

* download JDBC for postgresql and store in hive lib
```bash
cd /opt/hive/lib
wget https://jdbc.postgresql.org/download/postgresql-42.2.4.jar
```


