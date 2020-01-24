
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

* Configuring Hive. o configure Hive with Hadoop, you need to edit the hive-env.sh file
```bash
cd $HIVE_HOME/conf
cp hive-env.sh.template hive-env.sh ---> create new file from template
nano hive-env.sh
export HADOOP_HOME=/opt/hadoop
export HIVE_CONF_DIR=/opt/hive/conf

cp hive-default.xml.template hive-default.xml ---------------------> create new file from template
nano hive-default.xml ----------------------------> Edit the hive-default.sh file and add the following lines:
<property>
        <name>hive.metastore.event.db.notification.api.auth</name>
        <value>false</value>
        <description>should metastore do authorization against database notification related apis such as get_notification
                 if set true only superusers in proxy settings have the permission.
        </description>
</property>
```

* Check hive version
```bash
hive --version
```

### INSTALL POSTGRESQL

* Install PostgreSql to store metastore
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

### CREATE METASTORE

* Go to script located in 
```bash
cd /opt/hive/scripts/metastore/upgrade/postgres
```

* Connect to Postgresql and run scrips like this
```bash
sudo -u postgres psql

CREATE USER hiveuser WITH PASSWORD 'mypassword'; 
CREATE DATABASE metastore; 
GRANT ALL PRIVILEGES ON DATABASE metastore to hiveuser; 
\q
```

* Connect to Postgresql again and run scrips like this to create objects and give previleges
```bash
sudo -u postgres psql

postgres=# \c metastore 
metastore=#\i /opt/hive/scripts/metastore/upgrade/postgres/hive-schema-3.1.0.postgres.sql
postgres=# \c metastore 
metastore=# \pset tuples_only on 
metastore=# \o /tmp/grant-privs
metastore=# SELECT 'GRANT SELECT, INSERT, UPDATE, DELETE ON "' || schemaname || '". "' || tablename ||'" TO hiveuser ;' metastore=#    FROM pg_tables 
metastore=# WHERE tableowner = CURRENT_USER and schemaname = 'public'; 
 \o 
metastore=# \pset tuples_only off 
metastore=# \i /tmp/grant-privs
 
\q
```


* Go to Hive folder and create hive-site.xml e put some configuration about metastore
```bash
cd $HIVE_HOME/conf
nano hive-site.xml
<configuration>
  <property>
     <name>javax.jdo.option.ConnectionURL</name>
     <value>jdbc:postgresql://localhost:9083/metastore</value>
     <description>metadata is stored in a postgresql server</description>
   </property>
   <property>
     <name>javax.jdo.option.ConnectionDriverName</name>
     <value>org.postgresql.Driver</value>
     <description>POSTGRESQL JDBC driver class</description>
   </property>
   <property>
     <name>javax.jdo.option.ConnectionUserName</name>
     <value>hiveuser</value>
     <description>user name for connecting to postgresql server</description>
   </property>
   <property>
     <name>javax.jdo.option.ConnectionPassword</name>
     <value>mypassword</value>
     <description>password for connecting to postgresql server</description>
   </property>
</configuration>
--


* Initialize Hive
```bash
hive
