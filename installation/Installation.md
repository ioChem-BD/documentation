---
title: Installation
permalink: /Installation/
---
The system administrator must perform the following actions:
### Create iochembd system user
As root we will create a user account called *iochembd*, it will hold ioChem-BD files and will be responsible for running the web service that provides access to the software.
```console
  # useradd -m iochembd
```
We can use any other non privileged system user or username to install or run this software, we created iochembd as an example. The following commands will be run as a iochembd user, unless otherwise mentioned.
### Unzip application package
To start ioChem-BD installation, we will first download and gunzip the software package in the *iochembd* user home.

```console
   iochembd$ cd ~ 
   iochembd$ tar -xvf iochembd_nochem_v10.tar.gz
```
All the software is contained inside the single folder you just decompressed, with the following structure:

```console
    iochembd
    ├── apache-tomcat-7.0.37
    ├── browse
    ├── create
    ├── init-script
    ├── init.sh
    ├── installer.jar
    ├── jdk1.7.0_55
    ├── updates
    └── webapps
```
We can place it anywhere in our filesystem: one good candidates is *iochembd* user home, another one is inside */opt* folder. From now on we will talk about *BASE_PATH* when we refer to the path of this folder.
All extracted folders and its inner files must belong to the same user and group than the one that will start the web-server service (in this case *iochembd*), so it will be able to read and write inside it without problem.

##Init database, create database user and its related databases

### PostgreSQL configuration
If you have just installed the PostgreSQL server package you need to initialise its databases and start the database server, as *root* user you must run:

```console
root# /sbin/service postgresql initdb
```

You must set also PostgreSQL to start every time you restart your server.

```console 
root# chkconfig --level 345 postgresql on
```

Now we will configure PostgreSQL authentication file to allow login with password, we will edit */var/lib/pgsql/data/pg_hba.conf* and add these three lines:

```console
    # TYPE DATABASE USER ADDRESS METHOD
    # IPv4 local connections:
    host iochemCreate iochembd 127.0.0.1/32 md5
    host iochemCreateChemaxon iochembd 127.0.0.1/32 md5
    host iochemBrowse iochembd 127.0.0.1/32 md5
```
We can now start the PostgreSQL database service:

```console
root# /sbin/service postgresql restart
```

<span id="createdatabaseuser"></span> We will now create a new PostgreSQL database user and set the account password.
From the command line we will change to "root" or "postgres" user account (one with enough rights to execute the *createuser* command) and type the following:
```console
postgres$ createuser -s -d -l -P iochembd

   Enter password for new role:
   Enter it again:
```
After we create the account, please keep this password safe and consider it the **database.password** parameter.
We will now create three databases that will store ioChem-BD data:

```console
postgres$ createdb -O iochembd "iochemCreate"
postgres$ createdb -O iochembd "iochemCreateChemaxon"
postgres$ createdb -O iochembd "iochemBrowse"
```

###Run the installation script and fill in the forms
If we changed linux user to *root* or *postgres* we must now change back to *iochembd* user. Now we can execute the visual installer by moving inside *BASE_PATH* and executing *init.sh* script.

```console
iochembd$ cd *BASEPATH*
iochembd$ ./init.sh
```
A form will appear showing that the installer has started. 
![none|frame|Welcome form](/images/Install_step_1.png "wikilink") 

The next one will display the e-mail parameters configuration, more info at [mail fields](/installation/Required_steps.md#mail "wikilink").
There are two checkboxes that configure email to use encryption.

  * with no encrypted email services (default port 25) we will set both options unchecked
  * with SSL encryption (default port 465) we will check first option
  * with STARTTLS (default port 587) we will check both options

