---
title: Installation
permalink: /Installation/
---

# Installation procedure

The system administrator must perform following actions prior deploying the ioChem-BD platform.

### Create iochembd system user

As root we will create a user account called _iochembd_, it will hold ioChem-BD files and will be responsible for running the web service that provides access to the software.

```console
  # useradd -m iochembd
```

We can use any other non privileged system user or username to install or run this software, we created iochembd as an example. The following commands will be run as a iochembd user, unless otherwise mentioned.

### Unzip application package

To start ioChem-BD installation, we will first [download](https://gitlab.com/ioChem-BD/iochem-bd/-/releases) and extract the software package in the _iochembd_ user home.

```console
   iochembd$ cd ~
   iochembd$ tar -xvf iochembd-binary-X.X.X.tar.gz
```

All the software is contained inside the single folder you just decompressed, with the following structure:

```console
    iochembd
    ├── apache-tomcat
    ├── browse
    ├── cas
    ├── COPYING
    ├── create
    ├── init-script
    ├── init.sh
    ├── installer.jar
    ├── postinstall.sh
    ├── README.md
    ├── ssl
    ├── third-party
    ├── THIRD-PARTY.txt
    ├── updates
    ├── webapps
    └── webapps2
```

We can place it anywhere in our filesystem: one good candidates is _iochembd_ user home, another one is inside _/opt_ folder. From now on we will talk about _BASE\_PATH_ when we refer to the path of this folder.
All extracted folders and its inner files must belong to the same user and group than the one that will start the web-server service \(in this case _iochembd_\), so it will be able to read and write inside it without problem.

## Init database

### PostgreSQL configuration

If you have just installed the PostgreSQL server package you need to initialise its databases and start the database server, as _root_ user you must run:

```console
root# /sbin/service postgresql initdb
```

You must set also PostgreSQL to start every time you restart your server.

```console
root# chkconfig --level 345 postgresql on
```

Now we will configure PostgreSQL authentication file to allow login with password, we will edit _/var/lib/pgsql/data/pg\_hba.conf_ and add these three lines:

```console
    # TYPE DATABASE USER ADDRESS METHOD
    # IPv4 local connections:
    host iochemCreate iochembd 127.0.0.1/32 md5
    host iochemBrowse iochembd 127.0.0.1/32 md5
```

We can now start the PostgreSQL database service:

```console
root# /sbin/service postgresql restart
```

We will now create a new PostgreSQL database user and set the account password.
From the command line we will change to "root" or "postgres" user account \(one with enough rights to execute the _createuser_ command\) and type the following:

```console
postgres$ createuser -s -d -l -P iochembd

   Enter password for new role:
   Enter it again:
```

After we create the account, please keep this password safe and consider it the **database.password** parameter.
We will now create three databases that will store ioChem-BD data:

```console
postgres$ createdb -E UTF8 --locale='en_US.utf8' -T template0 -O iochembd "iochemCreate"
postgres$ createdb -E UTF8 --locale='en_US.utf8' -T template0 -O iochembd "iochemBrowse"
```

### Run the installation script and fill in the forms

If we changed linux user to _root_ or _postgres_ we must now change back to _iochembd_ user. Now we can execute the visual installer by moving inside _BASE\_PATH_ and executing _init.sh_ script.

```console
iochembd$ cd *BASEPATH*
iochembd$ ./init.sh
```

A form will appear showing that the installer has started.
![none\|frame\|Welcome form](/images/Install_step_1.png)

The next one will display the e-mail parameters configuration, more info at [mail fields](/installation/required_steps.md#mail-settings).
There are two checkboxes that configure email to use encryption.

* with no encrypted email services \(default port 25\) we will set both options unchecked
* with SSL encryption \(default port 465\) we will check first option
* with STARTTLS \(default port 587\) we will check both options

![none\|frame\|E-mail parameters](/images/Install_step_200.png "wikilink")
After filling in all fields, we can test the email parameters by sending a test message. We can click on the _Send test_ button to check this configuration. In the new form we can set the destination email and, if your configuration is valid, in a few seconds we must receive a test message from the installation program in our mailbox. Please check you received the test email because this is a very important step in ioChem-BD configuration, otherwise it will not be able to communicate with users \(on sending reset password emails for example\).

![none\|frame\|Send test dialog](/images/Install_step_2a.png "wikilink")

The next form will ask for all the details related to SSL certificate generation, more info at [certificate fields](/installation/required_steps.md#certificate-fields):

![none\|frame\|Certificate generation](/images/Install_step_3.png "wikilink")

Once our certificate has been generated and associated, a new form will pop up.
In this one we must define the database connection parameters. Once all of them have been filled, we need to click on the _Test connection_ button to check whether the database connection is successful.

![none\|frame\|Database connection form](/images/Install_step_4.png)

The next form will ask for basic login information for ioChem-BD administrator account generation, more info at [administrator account fields](/installation/required_steps.md#administrator-account-settings):

![none\|frame\|Admin account setup](/images/Install_step_5.png)

Last form will ask for installing ioChem-BD, clicking on _Back_ button will start all this steps again.

![none\|frame\|Installation confirmation form](/images/Install_step_6_a.png)

After clicking on _Install_, messages will inform us of the different install stages **it can take a few minutes to finish all steps**.

![none\|frame\|Processing steps](/images/Install_step_7a.png)

Once installation has finished, if you used default port \(443\) or one under 1024 to run ioChem-BD you must **run as root** the script file indicated by installer \(_postinstall.sh_\), in order to open such privileged port to ioChem-BD services.
If you get a message like this:

```console
root#  BASEPATH/postinstall.sh: line 6: setcap: command not found
```

This is because your system doesn't have setcap package installed \(OpenSuse\), run this command to install the package and then run the post install script again.

```console
root# zypper install libcap-progs
root# BASEPATH/postinstall.sh
```

### Edit /etc/hosts

You must add an entry on /etc/hosts to avoid ioChem-BD web services to go outside your network to find your domain, so you must enter the following line on /etc/hosts,

```console
   127.0.0.1     iochem-bd.urv.es            #Please replace iochem-bd.urv.es for your server domain name
```

### Run the web server application to start the web services

The files responsible for managing our web service are:

  * _BASE\_PATH_/apache-tomcat/bin/startup.sh to start service
  * _BASE\_PATH_/apache-tomcat/bin/shutdown.sh to stop service

After starting the web server you can track _BASE\_PATH_/apache-tomcat/logs/catalina.out file to look for start-up errors. If they appear, please [contact us](mailto:contact@iochem-bd.org) in order to assist you as soon as possible.

## Access ioChem-BD main page

Once installation has ended and web service has started, we should be able to access the main page of the ioChem-BD software, from now on _BASE\_URL_.
![none\|frame\|ioChem-BD Homepage](/images/Homepage2.png "wikilink") To access both modules you can click on homepage links or append module name to base URL:

* _BASE\_URL_/create
* _BASE\_URL_/browse

Our browser will "complain" about the self-signed certificate of the HTTPS pages, we just need to add an exception to avoid future questions.
Now that the ioChem-BD software is successfully deployed, we have to create user accounts and define user groups. Please refer to the [Creating users and groups](/installation/user-and-group-generation.md) page.

