# STREAMSETS Installation and Configuration
The StreamSets DataOps Platform helps you deliver continuous data to every part of your business, 
and handle data drift using a modern approach to data engineering and integration.

### Run in terminal(NameNode or another server) with user hadoop

* Download streamsets under home/user directory. Check if java 1.8 is installed, if not you should install first
```bash
cd /opt
sudo wget https://archives.streamsets.com/datacollector/3.13.0/tarball/streamsets-datacollector-core-3.13.0.tgz
```

* unpack files
```bash
sudo tar -xzf streamsets-datacollector-core-3.13.0.tgz 
```

* move to folder opt/streamsets and change owner to group and user hadoop
```bash
sudo mv streamsets-datacollector-core-3.13.0.tgz/ /opt/streamsets
sudo chown -R hadoop:hadoop streamsets/
```

*  add streamsets envirnoment variables under home/user
```bash
nano .bash_profile
# SQOOP
export STREAMSETS_HOME=/opt/streamsets
export PATH=$PATH:$STREAMSETS_HOME/bin
```

* renitialize/Activate
```bash
source .bash_profile
```

* To start streamsets
```bash
streamsets dc
```


