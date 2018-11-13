### Shell client

Our unique Linux shell client is intented to be deployed into your Linux box, where your calculations are generated and reside, or  on a \*nix machine where calculations are visible.

First we need to download the shell client into that box. To do so, you will first login in your Create Module.
Then you click on _Options_ in upper right menu bar. You need to selecy  _Download shell client_ so that it displays a form that will request your ioChem-BD password, the same that you used to login.

![Options menu bar](/images/WebUploadForm5.png)

The Create module will generate a .zip bundle with all  files. Decompress it using a command like:

```console
    $ unzip shell.zip
```

After deflating this file you have to add executing rights to the _start-rep-shell_ command and secure some properties file.

```console
    $ cd shell
    $ chmod +x start-rep-shell
    $ chmod 700 ./resources/resources.properties
```

The next step is to connect to the Create module via our Linux shell client. Call the _start-rep-shell_ script. IMPORTANT: the call has to be made using the _source_ command so to affect the current shell and to add our set of specific shell commands.

```console
    $ source start-rep-shell
```

**Note:** Not using _source \(_or _dot\) _ before the _start-rep-shell_ command will produce connection error events. It is mandatory to append the "source" command to start any remote connection properly.


More infornation: [Shell commands](/usage/uploading-content-to-create/shell-commands.md)

