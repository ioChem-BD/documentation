###Shell client

<span id="shellupload"></span> 
This client should be deployed inside HPC clusters, where calculations are generated and reside, or at least on a \*nix machine where calculations are visible.

First we need to download the shell client to this machine. To do so, we will first login on the Create module. 
Then we will click on *Options* in upper right menu bar. We need to click on *Download shell client* so that it displays a form that will request our ioChem-BD password, the same that we used to login.
![Options menu bar](/images/WebUploadForm5.png)
The Create module will generate a .zip bundle with all necessary files inside it. We will place this file inside our desired folder, we will decompress using a command like:
```console
    $ unzip shell.zip
```
After deflating this file we have to add execution rights to the *start-rep-shell* command and secure properties file:
```console
    $ cd shell
    $ chmod +x start-rep-shell
    $ chmod 700 ./resources/resources.properties
```
The next step is to connect to the Create module via our shell client. We will a run start-rep-shell script but using the *source* command to affect current shell and to add a group of specific shell commands.
```console
    $ source start-rep-shell
```
**Note:** Not using *source* or *dot* before the start command will make it impossible to operate via the shell client. It is mandatory to append this command to start the connection properly.
To continue from this point please check the entry where we detail all possible commands used from shell client: [Shell commands](/Shell_commands).