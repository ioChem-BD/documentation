---
title: Replace HTTPS certificate
permalink: /Replace_HTTPS_certificate/
---

ioChem-BD generates a self-signed certificate during its installation to enable secure HTTPS communications.
The downside of self-signed certificates is that they are not recognized by web browsers, so users will receive a warning message every time they access your ioChem-BD instance.
In order to use a valid HTTPS certificate and avoid such access warnings we encourage to replace that certificate for one expedited by a Certification Authority (CA), or any other valid certificate you already posses.
Two scenarios have been setup for ioChem-BD administrators in order to help in replacing HTTPS certificates, please choose the one that better fits your needs.

-   [Associate an existing certificate you already own](/#associateCert "wikilink")
-   [Purchase a new certificate on a Certification Authority (CA)](/#purchaseCACert "wikilink")

<span id="associateCert"></span>

Associate an existing certificate
---------------------------------

### Requirements

The *openssl* software package needs to be installed in your system and inside the $PATH variable (login with the same user account that runs the ioChem-BD software and try to execute *openssl version* command to check its properly installed).

`   iochembd$  openssl version`
`   OpenSSL 1.0.2h  3 May 2016  `*`(or`` ``another`` ``version)`*

The update process also needs these certificate files

-   A file with the public certificate
-   A file with the certificate private key
-   A file with the intermediate certificates (optional)

------------------------------------------------------------------------

Now we will detail the file names and the format of every file enumerated previously.
The file with the public certificate must be encoded on **X.509 PEM** format and with extension **.crt**. Example:

`   -----BEGIN CERTIFICATE-----`
`   MIIE/zCCBGgCAg4CMA0GCSqGSIb3DQEBBQUAMIGbMQswCQYDVQQGEwJKUDEOMAwG`
`   A1UECBMFVG9reW8xEDAOBgNVBAcTB0NodW8ta3UxETAPBgNVBAoTCEZyYW5rNERE    `
`   ...`
`   3V1dbLU5id63lVD8sUEULyfWFGk3L+Uka5oiSsxwZhdIb/Q=`
`   -----END CERTIFICATE----`

The file with the private certificate must be encoded on **unencrypted PKCS\#8 PEM** format and with extension **.key**. Example:

`   -----BEGIN PRIVATE KEY-----`
`   MHcCAQEEIBdVHnnzZmJm+Z1HAYYOZlvnB8Dj8kVx9XBH+6UCWlGUoAoGCCqGSM49`
`   AwEHoUQDQgAEThPp/xgEov0mKg2s0GII76VkZAcCc//3quAqzg+PuFKXgruaF7K`
`   ...`
`   -----END PRIVATE KEY-----`

Under some circumstances the certificate also has some intermediate certificates that contain its upper level certificates (the ones that the certificate trusts). In this special case you must concatenate all that certificates into a single file on **X509 PEM** format , ordered from them most local to most global and must have **.bundle** extension. Example file content with three intermediate certificates:

`   -----BEGIN CERTIFICATE-----`
`   ....`
`   -----END CERTIFICATE-----`
`   -----BEGIN CERTIFICATE-----`
`   ....`
`   -----END CERTIFICATE-----`
`   -----BEGIN CERTIFICATE-----`
`   ....`
`   -----END CERTIFICATE-----`

------------------------------------------------------------------------

Final checks: To ensure our certification chain is valid before we update ioChem-BD certificates, we will run the following command:

`   iochembd$ openssl verify -CAfile `*`additional`*`.bundle  `*`certificate`*`.crt `
`   certificate.crt : `**`OK`**

Any different response from previous command except OK should be analyzed and it's not advised to continue this certificate update procedure until the certification chain is totally valid.

### Update process

From now on we will talk about *BASE_PATH* when we refer to the path where the software has been installed, please replace it for the real full path
We will run the update process with the same user account that runs the software (in this case *iochembd*), all previous certificate files must also be owned by this user.
To begin, we will stop the web service:

`   iochembd$  `*`BASE_PATH`*`/apache-tomcat-7.0.37/bin/shutdown.sh`

Once the service has stopped, we will generate a directory to copy all certificate files inside

`   iochembd$  mkdir `*`BASE_PATH`*`/create/ssl`
`   iochembd$  cp `*`certificate`*`.crt    `*`BASE_PATH`*`/create/ssl    `*`#Only`` ``file`` ``extensions`` ``are`` ``fixed,`` ``names`` ``and`` ``original`` ``file`` ``paths`` ``can`` ``be`` ``arbitrary`*` `
`   iochembd$  cp `*`certificate`*`.key    `*`BASE_PATH`*`/create/ssl     `
`   iochembd$  cp `*`additional`*`.bundle  `*`BASE_PATH`*`/create/ssl    `*`#Optional`` ``file`*

With the requested files inside the ssl folder, we will launch the tool that replaces self-signed certificates for the new ones.

`   iochembd$  cd `*`BASE_PATH`*`/update`
`   iochembd$  ./updater.sh -p ReplaceDomainCertificate`

The output of this patch will enumerate all steps performed and which files are backed up and replaced:

`      19:18:26.021 [main] INFO  utils.Utils - Running command:[ps, -eaf, -o, pid, -o, cmd]`
`      19:18:26.022 [main] INFO  update.UpdatePatch - Running update vxxx.ReplaceDomainCertificate`
`      19:18:26.035 [main] INFO  update.UpdatePatch - Backup old keystore to: `*`.../iochem-bd/.keystore_161019191826`*
`      19:18:26.036 [main] INFO  update.UpdatePatch - Backup old cacert keystore to: `*`.../iochem-bd/jdk1.7.0_55/jre/lib/security/cacerts`*
`      19:18:26.036 [main] INFO  update.UpdatePatch - Backup old create.cer public key to `*`.../iochem-bd/updates/../webapps/create/keys/create.cer_161019191826`*
`      19:18:26.036 [main] INFO  update.UpdatePatch - Backup old cas_server.cer public key to `*`.../iochem-bd/updates/../webapps/create/keys/cas_server.cer_161019191826`*
`      19:18:26.036 [main] INFO  update.UpdatePatch - Generating pkcs12 certificate file from certs + key`
`      19:18:26.041 [main] INFO  update.UpdatePatch - Generating keystore from pkcs12 certificate`
`      19:18:26.197 [main] INFO  update.UpdatePatch - Replacing certificates with new ones.`
`      19:18:26.616 [main] INFO  update.UpdatePatch - `

`   End update successfully`
`   19:18:26.617 [main] INFO  update.UpdateProcess - ioChem-BD updated with patch ReplaceDomainCertificate.`
`   Update process finished.`

If the result of the update process is successful, we can start the service. Otherwise please [revert certificate changes](/#undoCertificate_generation "wikilink") and contact contact@iochem-bd.org reporting your errors

`   iochembd$  `*`BASE_PATH`*`/apache-tomcat-7.0.37/bin/startup.sh`

Once started, we can check that the ioChem-BD service is running with a valid HTTPS certificate. [none|frame|Green lock indicates a valid certificate](/File:Correct_https_certificate.png "wikilink")

<span id="purchaseCACert"></span>

Purchase a new certificate form a Certification Authority (CA)
--------------------------------------------------------------

In this section we will show the steps necessary to request a certificate to a Certification Authority. In this specific case we will use [ssls.com](http://ssls.com) CA to request the certificate, but you can choose any other CA of your choice, the steps will be similar, if not equal.
To buy a certificate we first need to generate a *Certificate Request* file (CSR). Inside it there will be defined the most relevant data of our certificate (domain to register, institution, city, country, etc).
Then we will submit such CSR file to the CA and after it checks that we own the server of that domain, it will generate and send us the public certificate file(s) to install in our server.
=== Certificate Request (CSR) file generation === ioChem-BD platform has coded a tool to leverage the CSR file generation and the installation of the CA generated certificates.
You need to run the following commands from the same user account that runs the ioChem-BD software to avoid file permission errors.
First we will move to the update folder and execute the following command

`   iochembd$  cd `*`BASE_PATH`*`/updates`
`   iochembd$  ./updater.sh -p ReplaceCertificate`
`   09:39:13.709 [main] INFO  update.UpdatePatch -  Running update vxxx.ReplaceCertificate`
`   `
`   1.Generate a certificate request`
`   2.Apply new issued certificate`
`   3.Exit`
`   `
`   Option: `**`1`**

We will choose the first option. The program will request some basic information about the certificate. The most important field is the domain name, if we are buying a single domain certificate (as is the case here) you must set the fully qualified domain name. Examples: iochem-bd.iciq.es, iochem.pic.es, www.iochem-bd.org

`   Insert certificate parameters;`
`   What is your (sub)domain?:`
`   `**`iochem-bd.iciq.es`**
`   What is the name of your organizational unit?`
`    [Unknown]: `**`ICIQ`**`  `
`   What is the name of your organization?`
`    [Unknown]: Institute of Chemical Research of Catalonia`
`   What is the name of your City or Locality?`
`    [Unknown]: `**`Tarragona`**
`   What is the name of your State or Province?`
`    [Unknown]: `**`Tarragona`**
`   What is the two-letter country code for this unit?`
`    [Unknown]: `**`ES`**
`   Is CN=iochem-bd.iciq.es, OU=ICIQ, O=Institute of Chemical Research of Catalonia, L=Tarragona, ST=Tarragona, C=ES correct?`
`    (yes/no) :`**`yes`**`                                                                                                     `
`   Certificate request generated on: .../iochem-bd/create/ssl/request.csr                           `
`   Your certificate request has been generated on: `**`.../iochem-bd/create/ssl/request.csr`**`            `
`                                                                                                                   `
`                                                                                                                   `
`   End update successfully                                                                                             `
`   10:21:02.659 [main] INFO  update.UpdateProcess - ioChem-BD updated with patch ReplaceCertificate.                   `
`   Update process finished.  `
`   `

After the process has ended, there will be new a file called *request.csr* on BASE_PATH/create/ssl folder, that is the certificate request file that we will send to the CA.
At this point we must contact the CA to request the certificate.
In the page of the CA we will pick a single domain certificate and then add it the basket [none|frame|Other type of domain certificate can be select if it better suits your needs, but the single domain one is a cheap solution](/File:Acert1.png "wikilink") [none|frame|Once selected, customer can select the number of years that the certificate will last until it expires. The longer expiration date, the less certificate updates have to be performed during time](/File:Acert2.png "wikilink") [none|frame|In the next step, the payment method must be filled in](/File:Acert3.png "wikilink") After the payment has been done, the CA page will display a new certificate in the list, ready to be requested.
[none|frame](/File:Cert2.png "wikilink") The following page will request to paste the content of the CSR file we have generated, so we will copy paste it including the *BEGIN NEW CERTIFICATE REQUEST* and the *END NEW CERTIFICATE REQUEST* lines.
[none|frame|Paste CSR file content here](/File:Cert3.png "wikilink") On the next page we will choose the "Jav Tomcat" option.
[none|frame](/File:Cert4.png "wikilink") The next page will display the supported domains for this new certificate, please double check this fields are valid.
[none|frame](/File:Cert5.png "wikilink") The next step is crucial in the certificate generation process. The CA must check that your are the real owner of that domain. To check it you can choose two validation methods:
\* To store an specific file inside your web server, so the CA will later retrieve it, verifying you are the domain owner ([further instructions here](/Replace_HTTPS_certificate_using_CA_certificate#file "wikilink"))

-   To send you a verification mail to an specific domain email address ([further instructions here](/Replace_HTTPS_certificate_using_CA_certificate#mail "wikilink"))

[none|frame](/File:Cert6.png "wikilink") <span id="postVerification"></span> After deciding the validation method (via file or email), we must finally fill the contact form. [none|frame](/File:Cert8.png "wikilink") If you followed the previous steps for validating your certificate, the line of your certificate will now display a green *Active* button on your account.
[none|frame|Activated certificate](/File:Cert12.png "wikilink") If you click the certificate link, you will be presented a page with the option to download the certificate public keys. We will use this files soon for installing the certificate. [none|frame|Click on Download option to get public certificate zip file](/File:Cert13.png "wikilink")

### Installing the certificate

Once we have the certificate .zip file we will extract its contents into the BASE_PATH/create/ssl folder

`   iochembd$  cp `*`iochem-bd.iciq.es.zip`*` `*`BASE_PATH`*`/create/ssl    `
`   iochembd$  cd `*`BASE_PATH`*`/create/ssl`
`   iochembd$  unzip `*`iochem-bd.iciq.es.zip`*

After the extraction you must have on *BASE_PATH*/create/ssl folder at least the following files:

-   A keystore.jks file with your private key
-   A \*.crt file with your public key certificate in X509 PEM format
-   An optional \*.ca-bundle with the intermediate CA certificates in X509 PEM format

Now you will use the tool again to install the certificate:
We will stop the web service:

`   iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/shutdown.sh`

Then we will run the tool with option 2:

`   iochembd$  cd `*`BASE_PATH`*`/updates`
`   iochembd$  ./updater.sh -p ReplaceCertificate`

`   13:45:15.104 [main] INFO  update.UpdatePatch -  Running update vxxx.ReplaceCertificate`
`   `
`   1.Generate a certificate request`
`   2.Apply new issued certificate`
`   3.Exit`
`   `
`   Option: `**`2`**

`   Backup old keystore to: .../iochem-bd/.keystore_134516`
`   Backup old cacert keystore to: .../iochem-bd/jdk1.7.0_55/jre/lib/security/cacerts`
`   Backup old create.cer public key to .../iochem-bd/updates/../webapps/create/keys/create.cer_134516`
`   Backup old cas_server.cer public key to .../iochem-bd/updates/../webapps/create/keys/cas_server.cer_134516`
`   13:45:17.409 [main] INFO  update.UpdatePatch - null`
`   `
`   `
`   End update successfully`
`   13:45:17.716 [main] INFO  update.UpdateProcess - ioChem-BD updated with patch ReplaceCertificate.`
`   Update process finished.`

If the result of the update process is successful, we can start the service. Otherwise please [revert certificate changes](/Replace_HTTPS_certificate#undoCertificate_generation "wikilink") and write to contact@iochem-bd.org reporting your errors

`  iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/startup.sh`

<span id="undoCertificate generation"></span>

Undo certificate generation process
-----------------------------------

If an exception is raised during previously described certification replacement processes, you can undo the entire process by restoring generated certificate files for its backed up copies.
The process affects the following files:

| File                                                   | Usage                                                              |
|--------------------------------------------------------|--------------------------------------------------------------------|
| *BASE_PATH*/**.keystore**                             | Java keystore used by Apache Tomcat to serve HTTPS encoded content |
| *BASE_PATH*/webapps/create/keys/**create.cer**        | Create server public keys                                          |
| *BASE_PATH*/webapps/create/keys/**cas_server.cer**   | CAS server public keys                                             |
| *BASE_PATH*/jdk1.7.0_55/jre/lib/security/**cacerts** | Java Runtime trusted public certificates keystore                  |

This files are backed up before starting the process by appending a timestamp to its name, the process will also display generated filenames.

`   19:18:26.035 [main] INFO  update.UpdatePatch - Backup old keystore to: .../iochem-bd/`**`.keystore_161019191826`**
`   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old cacert keystore to: .../iochem-bd/jdk1.7.0_55/jre/lib/security/`**`cacert_161019191826`**
`   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old create.cer public key to .../iochem-bd/updates/../webapps/create/keys/`**`create.cer_161019191826`**
`   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old cas_server.cer public key to .../iochem-bd/updates/../webapps/create/keys/`**`cas_server.cer_161019191826`**

To restore them, we will stop the web service and replace the generated files with the backed up files.

`   iochembd$  `*`BASE_PATH`*`/apache-tomcat-7.0.37/bin/shutdown.sh`
`   `
`   iochembd$  cp `*`BASE_PATH`*`/.keystore_161019191826 `*`BASE_PATH`*`/.keystore`
`   iochembd$  cp `*`BASE_PATH`*`/webapps/create/keys/create.cer_161019191826  `*`BASE_PATH`*`/webapps/create/keys/create.cer `
`   iochembd$  cp `*`BASE_PATH`*`/webapps/create/keys/cas_server.cer_161019191826  `*`BASE_PATH`*`/webapps/create/keys/cas_server.cer`
`   iochembd$  cp `*`BASE_PATH`*`/jdk1.7.0_55/jre/lib/security/cacerts_161019191826  `*`BASE_PATH`*`/jdk1.7.0_55/jre/lib/security/cacerts`
`   `
`   iochembd$  `*`BASE_PATH`*`/apache-tomcat-7.0.37/bin/startup.sh`

With these steps our original certificates will be restored and the faulty update process fixed.