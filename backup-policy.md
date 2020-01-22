##Define backup policy
We must backup at least ioChem-BD databases and the assetstore folders to be able to restore our system in case of data loss or corruption.
The first one contains all data information and relations, and the latter contain the uploaded calculation files. We can code an script and crontab it every Sunday night, for example, to backup such fields into a backup destination folder. Here is a sample script that dumps and zips such information, it is advised to add it to crontab:

```bash
#!/bin/bash
BACKUP_FOLDER=/home/iochembd/backup     # <-- Set your backup folder here
IOCHEM_FOLDER=/home/iochembd/iochembd   # <-- Set your ioChem-BD installation folder here

#sufix will alternate values 0,1..5 for each week number, change the expression to suit your backup needs 
sufix=$[`date +%e`/7%5]
BACKUP_FOLDER=$BACKUP_FOLDER/$sufix
rm -fr $BACKUP_FOLDER
mkdir -p $BACKUP_FOLDER

# Dump PostgreSQL databases, we must provide user password to allow dump to work properly, so please restrict script file rights to 700
export PGUSER=iochembd
export PGPASSWORD=                      # <-- Set iochembd database user password
pg_dump --inserts -h 127.0.0.1 -f $BACKUP_FOLDER/dump_iochemCreate.sql "iochemCreate"
pg_dump --inserts -h 127.0.0.1 -f $BACKUP_FOLDER/dump_iochemCreateChemaxon.sql "iochemCreateChemaxon"
pg_dump --inserts -h 127.0.0.1 -f $BACKUP_FOLDER/dump_iochemBrowse.sql "iochemBrowse"
unset PGUSER
unset PGPASSWORD

#Zip databases
gzip -f $BACKUP_FOLDER/dump_iochemCreate.sql
gzip -f $BACKUP_FOLDER/dump_iochemCreateChemaxon.sql
gzip -f $BACKUP_FOLDER/dump_iochemBrowse.sql

#Zip entire ioChem-BD  folde
tar -zcvf $BACKUP_FOLDER/iochembd.tar.gz $IOCHEM_FOLDER
```

