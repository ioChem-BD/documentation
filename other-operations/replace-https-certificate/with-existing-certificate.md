##Associate an existing certificate
### Requirements
The *openssl* software package needs to be installed in your system and inside the $PATH variable (login with the same user account that runs the ioChem-BD software and try to execute *openssl version* command to check its properly installed).

```console
iochembd$  openssl version
OpenSSL 1.0.2h  3 May 2016  (or another version)
```

The update process also needs these certificate files

   * A file with the public certificate
   * A file with the certificate private key
   * A file with the intermediate certificates (optional)
-----------------------------------------------------------------------


Now we will detail the file names and the format of every file enumerated previously.
The file with the public certificate must be encoded on **X.509 PEM** format and with extension **.crt**. Example:

```console
   -----BEGIN CERTIFICATE-----
   MIIE/zCCBGgCAg4CMA0GCSqGSIb3DQEBBQUAMIGbMQswCQYDVQQGEwJKUDEOMAwG
   A1UECBMFVG9reW8xEDAOBgNVBAcTB0NodW8ta3UxETAPBgNVBAoTCEZyYW5rNERE    
   ...
   3V1dbLU5id63lVD8sUEULyfWFGk3L+Uka5oiSsxwZhdIb/Q=
   -----END CERTIFICATE----
```
The file with the private certificate must be encoded on **unencrypted PKCS\#8 PEM** format and with extension **.key**. Example:
```console
   -----BEGIN PRIVATE KEY-----
   MHcCAQEEIBdVHnnzZmJm+Z1HAYYOZlvnB8Dj8kVx9XBH+6UCWlGUoAoGCCqGSM49
   AwEHoUQDQgAEThPp/xgEov0mKg2s0GII76VkZAcCc//3quAqzg+PuFKXgruaF7K
   ...
   -----END PRIVATE KEY-----
```
Under some circumstances the certificate also has some intermediate certificates that contain its upper level certificates (the ones that the certificate trusts). In this special case you must concatenate all that certificates into a single file on **X509 PEM** format , ordered from them most local to most global and must have **.bundle** extension. Example file content with three intermediate certificates:
```console
   -----BEGIN CERTIFICATE-----
   ....
   -----END CERTIFICATE-----
   -----BEGIN CERTIFICATE-----
   ....
   -----END CERTIFICATE-----
   -----BEGIN CERTIFICATE-----
   ....
   -----END CERTIFICATE-----
```
------------------------------------------------------------------------

Final checks: To ensure our certification chain is valid before we update ioChem-BD certificates, we will run the following command:
```console
   iochembd$   openssl verify -CAfile additional.bundle  certificate.crt 
   certificate.crt : OK
```
Any different response from previous command except OK should be analyzed and it's not advised to continue this certificate update procedure until the certification chain is totally valid.

### Update process

From now on we will talk about *BASE_PATH* when we refer to the path where the software has been installed, please replace it for the real full path
We will run the update process with the same user account that runs the software (in this case *iochembd*), all previous certificate files must also be owned by this user.
We will initially stop the web service:
```console
   iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/shutdown.sh
```

Once the service has stopped, we will generate a directory to copy all certificate files inside:
```console
   iochembd$  mkdir BASE_PATH/create/ssl
   iochembd$  cp certificate.crt    BASE_PATH/create/ssl    #Only file extensions are fixed, names and original file paths can be arbitrary 
   iochembd$  cp certificate.key    BASE_PATH/create/ssl     
   iochembd$  cp additional.bundle  BASE_PATH/create/ssl    #Optional file*
```
With the requested files inside the ssl folder, we will launch the tool that replaces self-signed certificates for the new ones.
```console
   iochembd$  cd BASE_PATH/update
   iochembd$  ./updater.sh -p ReplaceDomainCertificate
```
The output of this patch will enumerate all steps performed and which files are backed up and replaced:
```console
   19:18:26.021 [main] INFO  utils.Utils - Running command:[ps, -eaf, -o, pid, -o, cmd]
   19:18:26.022 [main] INFO  update.UpdatePatch - Running update vxxx.ReplaceDomainCertificate
   19:18:26.035 [main] INFO  update.UpdatePatch - Backup old keystore to: .../iochem-bd/.keystore_161019191826*
   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old cacert keystore to: .../iochem-bd/jdk1.7.0_55/jre/lib/security/cacerts*
   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old create.cer public key to .../iochem-bd/updates/../webapps/create/keys/create.cer_161019191826*
   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old cas_server.cer public key to .../iochem-bd/updates/../webapps/create/keys/cas_server.cer_161019191826*
   19:18:26.036 [main] INFO  update.UpdatePatch - Generating pkcs12 certificate file from certs + key
   19:18:26.041 [main] INFO  update.UpdatePatch - Generating keystore from pkcs12 certificate
   19:18:26.197 [main] INFO  update.UpdatePatch - Replacing certificates with new ones.
   19:18:26.616 [main] INFO  update.UpdatePatch - 
   
   End update successfully
   19:18:26.617 [main] INFO  update.UpdateProcess - ioChem-BD updated with patch ReplaceDomainCertificate.
   Update process finished.
   ```
If the result of the update process is successful, we can start the service. Otherwise please [revert certificate changes](/#undoCertificate_generation "wikilink") and contact contact@iochem-bd.org reporting your errors
```console
   iochembd$    BASE_PATH/apache-tomcat-7.0.37/bin/startup.sh
```
Once started, we can check that the ioChem-BD service is running with a valid HTTPS certificate. ![none|frame|Green lock indicates a valid certificate](/images/Correct_https_certificate.png "wikilink")