

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








