##Undo certificate generation process
If an exception is raised during previously described certification replacement processes, you can undo the entire process by restoring generated certificate files for its backed up copies.
The process affects the following files:

| File | Usage |
|--- --|-------|
| *BASE_PATH*/**.keystore** | Java keystore used by Apache Tomcat to serve HTTPS encoded content |
| *BASE_PATH*/webapps/create/keys/**create.cer** | Create server public keys |
| *BASE_PATH*/webapps/create/keys/**cas_server.cer** | CAS server public keys |
| *BASE_PATH*/jdk1.7.0_55/jre/lib/security/**cacerts** | Java Runtime trusted public certificates keystore |

This files are backed up before starting the process by appending a timestamp to its name, the process will also display generated filenames.
```console
   19:18:26.035 [main] INFO  update.UpdatePatch - Backup old keystore to: .../iochem-bd/.keystore_161019191826
   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old cacert keystore to: .../iochem-bd/jdk1.7.0_55/jre/lib/security/cacert_161019191826
   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old create.cer public key to .../iochem-bd/updates/../webapps/create/keys/create.cer_161019191826
   19:18:26.036 [main] INFO  update.UpdatePatch - Backup old cas_server.cer public key to .../iochem-bd/updates/../webapps/create/keys/cas_server.cer_161019191826
```
To restore them, we will stop the web service and replace the generated files with the backed up files.
```console
   iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/shutdown.sh
   
   iochembd$  cp BASE_PATH/.keystore_161019191826 BASE_PATH/.keystore
   iochembd$  cp BASE_PATH/webapps/create/keys/create.cer_161019191826  BASE_PATH/webapps/create/keys/create.cer 
   iochembd$  cp BASE_PATH/webapps/create/keys/cas_server.cer_161019191826  BASE_PATH/webapps/create/keys/cas_server.cer
   iochembd$  cp BASE_PATH/jdk1.7.0_55/jre/lib/security/cacerts_161019191826  BASE_PATH/jdk1.7.0_55/jre/lib/security/cacerts
   
   iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/startup.sh
```
With these steps our original certificates will be restored and the faulty update process fixed.