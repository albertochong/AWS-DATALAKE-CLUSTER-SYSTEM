

# Hue installation and configuration 


## Run in Terminal

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

## Hive Installation and Configuration

* Download Hive
```bash
sudo wget https://www-eu.apache.org/dist/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz
```

* Unpack files
```bash
sudo tar -xvf apache-hive-3.1.2-bin.tar.gz
```

* Move to appropriate folder
```bash

```







