---
title: Required steps
permalink: /Required_steps/
---
#Steps prior installation
The ioChem-BD installation procedure will ask for some configuration information that the sysadmin must provide in order to enable all the functionalities of the software.
So please write down all these fields and keep them at hand during the installation process
## Required information
In this section we will list all fields that will be prompted for the user to fulfill, all accompanied at the end by a little description of its usage in the system.
We define *Field name* column in the tables as an easy way to refer to these parameters during installation.
###Mail settings
<span id="mail"></span> It is advised to create an email account at your institution for ioChem-BD software, otherwise you can use a personal email address as sender of all notifications.

|Field name|Description|Sample values|
|----------|-----------|-------------|
|<strong>smtp.server.hostname</strong>|SMTP server hostname|smtp.urv.cat|
|<strong>smtp.server.port</strong>|Port number used by the mail server|25<br/>587|
|<strong>smtp.mail.from</strong>|Sender e-mail address, all notifications from ioChem-BD will be sent using this e-mail address|iochem-bd@urv.cat<br />iochem-bd@iciq.es<br />username@institution.com|
|<strong>smtp.mail.username</strong>|(Optional) If mail server requires authentication, set email account username||
|<strong>smtp.mail.password</strong>|(Optional) If mail server requires authentication, set email account password||

###Certificate fields
<span id="certificate"></span> ioChem-BD software should run on a web server that must be publicly accessible. This will not only allow its users to access it from anywhere but will also be used to interconnect Browse modules from different institutions to build a bigger data repository of theoretical chemistry results. So it must be accessible as a domain or as part of a subdomain of the destination institution.

| Field name | Description | Sample values |
|-----------|---------------|---------------| 
| **host.hostname** | Public qualified host name of the web server<br/>Never use *localhost* as hostname. | iochem-bd.iciq.es<br/>rodi.urv.es<br/>argo.urv.es|
|  **host.ip** | Public ip of the web server | 130.206.36.13 |
| **host.port** | Port where the software will run and will be browsed (default: 443) <br/>Never use 80 because ioChem-BD uses HTTPS instead of HTTP | 443 (default) |

All communications inside this software, shell client &lt;-&gt; modules , module &lt;-&gt; module, user browser &lt;-&gt; module are safety encrypted using SSL certificates; right now it uses self-signed certificates but in future revisions we will add support for Certification Authority (CA) certificates.
> Note: To build the certificate, you must provide a few fields to generate it correctly . Please keep in mind that the field defined in **${cert.organization}** will be the organization name, which will be appended to all generated content and displayed in ioChem-BD web pages.

| Field name | Description | Sample values |
|------------|-------------|---------------|
| **cert.organizational.unit** | Organizational unit defined inside SSL certificate|Dept.Computational Chemistry<br/>Quantum Chemistry Group |
| **cert.organization** | Name of your organization (avoid acronyms/abbreviations when possible) | Universitat Rovira i Virgili<br/>Institute of Chemical Research of Catalonia|
| **cert.city** | City/location of your organization | Tarragona<br/>Barcelona<br/>Paris |
| **cert.state** | State/Province or your organization | Catalonia - Spain<br/>France |
| **cert.country.code** | Country code (two characters, [check it here](http://www.nationsonline.org/oneworld/country_code_list.htm)) | ES<br/>FR |

###Database settings
These fields will be used by ioChem-BD to define its database connection parameters.

| Field name | Description | Sample values |
|------------|-------------|---------------|
| **database.host** | Hostname of postgresql server | localhost |
| **database.port** | Postgresql port number | 5432 |
| **database.username** | Postgresql username ([defined during installation process](/installation/installation.md#createdatabaseuser)) | iochembd |
| **database.password** | Postgresql password ([defined during installation process](/installation#createdatabaseuser "wikilink")) |          |

###Administrator account settings
<span id="admin"></span> During the last steps of installation you will be prompted to generate an ioChem-BD administrator account, such account will be the one in charge of managing and configuring all the software package.
For the sake of ioChem-BD's security it is advised that the administrator [creates a "non-admin" user account](/installation/Structure_generation#useraccountgeneration "wikilink") if he/she wants to work with Create module as a normal user.

|Field name|Description|Sample values|
|----------|-----------|-------------|
|**admin.email**|Administrator email and also username inside the system|iochem-bd@urv.cat<br />iochem-bd@iciq.es<br/>username@institution.com|
|**admin.password**|Administration account password||
|**admin.telephone**|Contact phone that will appear on system errors and notifications|+34 977-XXX-XXX|