##Define backup policy
We must backup at least ioChem-BD databases and the assetstore folders to be able to restore our system in case of data loss or corruption.   
The first one contains all data information and relations, and the latter contain the uploaded calculation files. We can code an script and crontab it every Sunday night, for example, to backup such fields into a backup destination folder. Here is a sample script that dumps and zips such information, it is advised to crontab it:

```
#!/bin/bash
BACKUP_FOLDER=/home/iochembd/backup     <b># <-- Set your backup folder here</b>
IOCHEM_FOLDER=/home/iochembd/iochembd   # <-- Set your ioChem-BD installation folder here

# Dump PostgreSQL databases, we must provide user password to allow dump to work properly, so please restrict script file rights to 700
export PGUSER=iochembd
export PGPASSWORD=                      # <-- Set iochembd database user password
pg_dump --inserts -h 127.0.0.1 -f $BACKUP_FOLDER/dump_iochemCreate.sql "iochemCreate"
pg_dump --inserts -h 127.0.0.1 -f $BACKUP_FOLDER/dump_iochemCreateChemaxon.sql "iochemCreateChemaxon"
pg_dump --inserts -h 127.0.0.1 -f $BACKUP_FOLDER/dump_iochemBrowse.sql "iochemBrowse"
unset PGUSER
unset PGPASSWORD

#Zip database
gzip $BACKUP_FOLDER/dump_iochemCreate.sql
gzip $BACKUP_FOLDER/dump_iochemCreateChemaxon.sql
gzip $BACKUP_FOLDER/dump_iochemBrowse.sql

#Zip entire Create assetstore folder: $IOCHEM_FOLDER/create/assetstore
#sufix will alternate values 0,1... each week
sufix=$[date +%e/7%2] 
tar -C $IOCHEM_FOLDER/create -zcf $BACKUP_FOLDER/create_week$sufix.tar.gz assetstore

#Zip entire Browse assetstore folder: $IOCHEM_FOLDER/create/assetstore
tar -C $IOCHEM_FOLDER/browse -zcf $BACKUP_FOLDER/browse_week$sufix.tar.gz assetstore
```

