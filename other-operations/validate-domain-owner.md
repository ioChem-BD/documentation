##Validate domain owner using CA provided file
If you selected to validate using a file provided by the CA, you will be presented a form that allows to download the validation file. You can download this file anytime from your user account. 
![](/images/Cert11.png)
The CA needs this file to be accessible on top of your domain, so if you downloaded a file called *45807864968745967459.txt* to validate the domain *iochem-bd.iciq.es* then the CA needs to access the URL:
<http://iochem-bd.iciq.es/45807864968745967459.txt>
The request will be always done on HTTP port 80. Depending on the type of web services that run on your server machine this file will need to be copied to ioChem-BD or to another web service folder that runs on that port.
If the port is free, you can use the ioChem-BD software to store such validation file by letting it run on port 80. These are the steps to do it:
Stop ioChem-BD web service:
```code
   iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/shutdown.sh
```
Copy the downloaded file into webapps2/ROOT folder
```code
   iochembd$  cp 45807864968745967459.txt BASE_PATH/webapps2/ROOT
```
Edit *BASE_PATH*/apache-tomcat-7.0.37/conf/server.xml and uncomment the following Catalina2 line

```code 
<Service name="Catalina2">
     <Connector port="80" protocol="HTTP/1.1" connectionTimeout="20000" /> <!-- Uncomment this line --> 
     <Connector port="9010" protocol="HTTP/1.1" connectionTimeout="20000" />
     <Connector port="8010" protocol="AJP/1.3" redirectPort="9010" />
     <Engine name="Catalina" defaultHost="doi.iochem-bd.org">
       <Realm className="org.apache.catalina.realm.LockOutRealm">
           <Realm className="org.apache.catalina.realm.UserDatabaseRealm" resourceName="UserDatabase"/>
       </Realm>
       <Host name="doi.iochem-bd.org" appBase="../webapps2" unpackWARs="true" autoDeploy="true">
           <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" prefix="localhost_access_log." suffix=".txt" pattern="%h %l %u %t "%r" %s %b" />
       </Host>
     </Engine>
   </Service>
```

Now start again the server:

```code
   iochembd$  BASE_PATH/apache-tomcat-7.0.37/bin/startup.sh
```
If everything is correct, you now must be able to access the file, so will do the CA, validating you as the domain owner. *Note:* This action can take hours to accomplish.
You can leave ioChem-BD running on port 80 or undo this last step now that certificate is validated. To do so, just stop the ioChem-BD web service, comment the previously uncommented line and start the web service again, Now you can proceed with the remaining [certificate installation steps](/other-operations/replace-https-certificate/purchase-new-ca-certificate.md#validating-domain-ownership).

##Validate domain owner using email address
If you choose to validate via email, you need to choose among different email addresses. The selected e-mail address will receive a link to end the request process. 
![](/images/Cert7.png) Now you can proceed with the remaining [certificate installation steps](/other-operations/replace-https-certificate/purchase-new-ca-certificate.md#validating-domain-ownership).