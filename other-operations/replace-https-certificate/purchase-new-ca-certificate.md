##Purchase a new certificate form a Certification Authority (CA)
In this section we will show the steps necessary to request a certificate to a Certification Authority. In this specific case we will use [ssls.com](http://ssls.com) CA to request the certificate, but you can choose any other CA of your choice, the steps will be similar, if not equal.
To buy a certificate we first need to generate a *Certificate Request* file (CSR). Inside it there will be defined the most relevant data of our certificate (domain to register, institution, city, country, etc).
Then we will submit such CSR file to the CA and after it checks that we own the server of that domain, it will generate and send us the public certificate file(s) to install in our server.
### Certificate Request (CSR) file generation 
ioChem-BD platform has coded a tool to leverage the CSR file generation and the installation of the CA generated certificates.
You need to run the following commands from the same user account that runs the ioChem-BD software to avoid file permission errors.
First we will move to the update folder and execute the following command
```console
   iochembd$  cd BASE_PATH/updates
   iochembd$  ./updater.sh -p ReplaceCertificate
   09:39:13.709 [main] INFO  update.UpdatePatch -  Running update vxxx.ReplaceCertificate
   
   1.Generate a certificate request
   2.Apply new issued certificate
   3.Exit
   
   Option: 1
```
We will choose the first option. The program will request some basic information about the certificate. The most important field is the domain name, if we are buying a single domain certificate (as is the case here) you must set the fully qualified domain name. Examples: iochem-bd.iciq.es, iochem.pic.es, www.iochem-bd.org
```console
   Insert certificate parameters;
   What is your (sub)domain?:
   iochem-bd.iciq.es
   What is the name of your organizational unit?
    [Unknown]: ICIQ  
   What is the name of your organization?
    [Unknown]: Institute of Chemical Research of Catalonia
   What is the name of your City or Locality?
    [Unknown]: Tarragona
   What is the name of your State or Province?
    [Unknown]: Tarragona
   What is the two-letter country code for this unit?
    [Unknown]: ES
   Is CN=iochem-bd.iciq.es, OU=ICIQ, O=Institute of Chemical Research of Catalonia, L=Tarragona, ST=Tarragona, C=ES correct?
    (yes/no) :yes                                                                                                     
   Certificate request generated on: .../iochem-bd/create/ssl/request.csr                           
   Your certificate request has been generated on: .../iochem-bd/create/ssl/request.csr            
                                                                                                                   
                                                                                                                   
   End update successfully                                                                                             
   10:21:02.659 [main] INFO  update.UpdateProcess - ioChem-BD updated with patch ReplaceCertificate.                   
   Update process finished.  
```   
###Purchasing the certificate
After the process has ended, there will be new a file called *request.csr* on BASE_PATH/create/ssl folder, that is the certificate request file that we will send to the CA. At this point we must contact the CA to request the certificate.
In the page of the CA we will pick a single domain certificate and then add it the basket. 
Other type of domain certificate can be select if it better suits your needs, but the single domain one is a cheap solution.
![](/images/Acert1.png)
Once selected, customer can select the number of years that the certificate will last until it expires. The longer expiration date, the less certificate updates have to be performed during time.
![](/images/Acert2.png)
In the next step, the payment method must be filled in
![](/images/Acert3.png)
After the payment has been done, the CA page will display a new certificate in the list, ready to be requested.
![](/images/Cert2.png)

The following page will request to paste the content of the CSR file we have generated, so we will copy paste it including the *BEGIN NEW CERTIFICATE REQUEST* and the *END NEW CERTIFICATE REQUEST* lines. Paste CSR file content there.

![](/images/Cert3.png) 

On the next page we will choose the "Jav Tomcat" option.

![](/images/Cert4.png)

The next page will display the supported domains for this new certificate, please double check this fields are valid.

![](/images/Cert5.png) 

###Validating domain ownership
The next step is crucial in the certificate generation process. The CA must check that your are the real owner of that domain. To check it you can choose two validation methods:
   * To store an specific file inside your web server, so the CA will later retrieve it, verifying you are the domain owner, [further instructions here](/other-operations/validate-domain-owner.md#validate-domain-owner-using-CA-provided-file).
   * To send you a verification mail to an specific domain email address , [further instructions here](/other-operations/validate-domain-owner.md#validate-domain-owner-using-email-address)

   
![](/images/Cert6.png) 

After deciding the validation method (via file or email), we must finally fill the contact form. 

![](/images/Cert8.png) 

If you followed the previous steps for validating your certificate, the line of your certificate will now display a green *Active* button on your account.

![](/images/Cert12.png) 

If you click the certificate link, you will be presented a page with the option to download the certificate public keys. We will use this files soon for installing the certificate. 
Click on Download option to get public certificate zip file

![](/images/Cert13.png)

### Installing the certificate

Once we have the certificate .zip file we will extract its contents into the BASE_PATH/create/ssl folder
```console
   iochembd$  cp iochem-bd.iciq.es.zip BASE_PATH/create/ssl    
   iochembd$  cd BASE_PATH/create/ssl
   iochembd$  unzip iochem-bd.iciq.es.zip*
```
After the extraction you must have on *BASE_PATH*/create/ssl folder at least the following files:

   * A keystore.jks file with your private key
   * A \*.crt file with your public key certificate in X509 PEM format
   * An optional \*.ca-bundle with the intermediate CA certificates in X509 PEM format

Now you will use the tool again to install the certificate:
We will stop the web service:
```console
   iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/shutdown.sh
```
Then we will run the tool with option 2:
```console
   iochembd$  cd BASE_PATH/updates
   iochembd$  ./updater.sh -p ReplaceCertificate

   13:45:15.104 [main] INFO  update.UpdatePatch -  Running update vxxx.ReplaceCertificate
   
   1.Generate a certificate request
   2.Apply new issued certificate
   3.Exit
   
   Option: 2
```
--------------------
```console
   Backup old keystore to: .../iochem-bd/.keystore_134516
   Backup old cacert keystore to: .../iochem-bd/jdk1.7.0_55/jre/lib/security/cacerts
   Backup old create.cer public key to .../iochem-bd/updates/../webapps/create/keys/create.cer_134516
   Backup old cas_server.cer public key to .../iochem-bd/updates/../webapps/create/keys/cas_server.cer_134516
   13:45:17.409 [main] INFO  update.UpdatePatch - null
   
   
   End update successfully
   13:45:17.716 [main] INFO  update.UpdateProcess - ioChem-BD updated with patch ReplaceCertificate.
   Update process finished.
```
If the result of the update process is successful, we can start the service. Otherwise please [revert certificate changes](/other-operations/replace-https-certificate/undo-certificate-generation-process.md) and write to contact@iochem-bd.org reporting your errors
```console
  iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/startup.sh
```
