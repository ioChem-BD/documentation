##Shell commands
All commands described here allow **-h** parameter that will display a help message containing a wider description of its usage.
### Basic parameters

| Command           | Description                  |
|-------------------|------------------------------|
| [source start-rep-shell](#start-rep-shell) | Connect to repository   |
| [lspro](#lspro)          | List current path contents                |
| [pwdpro](#pwdpro)        | Print current path (similar to pwd)       |
| [exit-rep](#exit)        | Disconnect from repository                |


###Project related commands

| Command                         | Description                   |
|---------------------------------|-------------------------------|
| [catpro](#catpro)   | Display project information               |
| [cdpro](#cdpro)     | Change to project                         |
| [cpro](#cpro)       | Create a new project                      |
| [mpro](#mpro)       | Modify a project                          |
| [dpro](#dpro)       | Delete a project                          |
| [findpro](#findpro) | Find project by it’s name (regex allowed) |

###Calculation related commands

| Command                                                    | Description                        |
|------------------------------------------------------------|------------------------------------|
| [viewcalc](#viewcalc)                          | View calculation information       |
| [dcalc](#dcalc)                                | Delete calculation from repository |
| [loadcalc](#loadcalc)                          | Load calculation into repository   |
| Calculation type specific commands                         |                                    |
| [loadgauss](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadgauss) | Load Gaussian calculation          |
| [loadadf](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadadf)     | Load ADF calculation               |
| [loadturbo](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadturbo) | Load Turbomole calculation         |
| [loadorca](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadorca)   | Load Orca calculation              |
| [loadvasp](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadvasp)   | Load Vasp calculation              |

##Basic parameters explained
###start-rep-shell
Used to connect to the repository, it must be always preceded by **source** or **.** (dot), otherwise neither connection nor commands will work.

| Examples                       |                                          |
|--------------------------------|------------------------------------------|
| *user$* source start-rep-shell | Connect to repository using long format  |
| *user$* . start-rep-shell      | Connect to repository using short format |

###lspro
Displays content of current path: projects and calculations. Otherwise we can define a path to list its content.

| Parameters | Description  |                                                                                                  
|------------|--------------|
| -n *path*  | Relative or absolute path project (optional) |                                                           
| -f         | Display long format in listing (optional)    |
| -o *order* | Order by. Possible values:<br/> n-&gt;name, * o-&gt;owner, g-&gt;group<br/>t-&gt;time, c-&gt;concept, * s-&gt;state (optional) |

|Examples: |        |
|----------|-------|
| *user$* lspro | Sample listing in current path | 
| *user$* lspro -n /db/username/hexenol | Lists by name the content of hexenol project (absolute path)|
| *user$* lspro -o Sc2C82 | Lists by owner the content of hexenol project (relative to current path) |

###pwdpro
Displays the current path, similar to pwd (print working directory) but lists current position inside the project's hierarchy.

| Examples       |                     |
|----------------|---------------------|
| *user$* pwdpro | Prints current path |

###exit-rep
Disconnects from the repository and ends current session. All repository commands are disabled after this command is executed.

| Examples         |                             |
|------------------|-----------------------------|
| *user$* exit-rep | Disconnects from repository |

##Project related commands
###catpro
Displays project information.

| Parameters | Description   |
|------------|---------------|
| -n *path*  | Relative or absolute project path (mandatory) |

| Examples:  |         |
|------------|---------|
| *user$* catpro -n hexenol | Prints project information using relative path |
| *user$* catpro -n /db/username/hexenol | Print project information using absolute path |


###cdpro
Changes path by navigating to parent / child project or an absolute path.

| Parameters | Description                                                |
|------------|------------------------------------------------------------|
| -n *path*  | Relative or absolute project path (mandatory except on ..) |

| Examples:  |    |
|------------|---|
| *user$* cdpro .. | Changes path to parent project |
| *user$* cdpro -n metanol | Navigates to child project called metanol |
| *user$* cdpro -n /db/username/metanol/freq | Navigates to project using full path |

###cpro
Creates new project in current path. If name or description parameters contains blank spaces, they must be enclosed in double quotes.

| Parameters | Description                             |
|------------|-----------------------------------------|
| -n         | Name of the project (mandatory)         |
| -d         | Description of the project (mandatory)  |
| -cg        | Concept Group of the project (optional) |

| Examples: |       |
|-----------|-------|
| *user$* cpro -n metanol -d metanol | Creates metanol project with metanol description |
| *user$* cpro -n metanol -d metanol -cg FRQ | Creates project with description and concept group |
| *user$* cpro -n metanol -d "This is the metanol project description" | Creates metanol project with a long description |


###mpro
Modifies the selected project properties, name, description or even moves it to another project (as a nested project).

| Parameters           | Description                                         |
|----------------------|-----------------------------------------------------|
| -n *path*            | Relative or absolute project path (mandatory)       |
| -p *permissions*     | Permissions of the project. Ex: '110100' (optional) |
| -o *owner*           | Owner of the project (optional)                     |
| -g *group*           | Group owner of the project (optional)               |
| -cg *concept_group*  | Concept Group of the project (optional)             |
| -nn *name*           | New Name of the project (optional)                  |
| -np *path*           | New Parent project (absolute path) (optional)       |
| -d *description*     | Description of the project (optional)               |

|Examples  |       |
|----------|-------|
| *user$* mpro -n /db/username/hexenol -nn hexenolMod | Replaces project name by hexenolMod |
| *user$* mpro -n /db/username/hexenol -np /db/user/alcohols | Moves selected project to another parent project |
| *user$* mpro -n /db/username/hexenol -d "Replaced description" | Replaces description on selected project |


###dpro
Deletes a project by defining its path, all child projects and calculations will also be removed from Create.

| Parameters | Description                                   |
|------------|-----------------------------------------------|
| -n *path*  | Relative or absolute project path (mandatory) |

| Examples          |                         |
|-------------------|-----------------------------|
| *user$* dpro -n metanol  | Deletes metanol project using relative path, our path must be at the level of this project |
| *user$* dpro -n /db/username/alcohols/metanol | Deletes metanol project using absolute path, current path position is not relevant here    |

###findpro
Find project by it’s name (regex allowed)

| Parameters       | Description                                                               |
|------------------|---------------------------------------------------------------------------|
| -n *name*        | Regular expression to find in the name field of project (optional)        |
| -d *description* | Regular expression to find in the description field of project (optional) |
| -p *path*        | Regular expression to find in the path field of project (optional)        |

| Examples |              |
|----------|--------------|
| findpro -n metan\* | Finds projects which name match regular expression metan\* |
| findpro -d "alco\* " | Finds projects which description match regular expression alco\* |


##Calculation related commands
###viewcalc
This comands displays the most relevant information about a calculation.

| Parameters | Description                                   |
|------------|-----------------------------------------------|
| -n *path*  | Relative or absolute project path (mandatory) |
| -f         | If present shows full contents. (optional)    |

###dcalc
This comands deletes a calculation given its name.

| Parameters | Description                                       |
|------------|---------------------------------------------------|
| -n *path*  | Relative or absolute calculation path (mandatory) |

Using full calculation path:
```console
    $ dcalc -n  /db/user/metOH-oxidation/freq1    #Will delete calculation freq1 inside metOH-oxidation project
```
Navigating to parent project and using calculation name:
```console
    $ cdpro metOH-oxidation             #Move to parent project
    $ dcalc -n freq1                    #Will delete calculation freq1
```


###loadcalc
Uploads a calculation into the Create module on the current project path. It is not allowed to upload calculations to the base path (*/db/username*), you must always upload calculations into a project.
This is a generic command that will allow us to upload multiple files and formats, some parameters will be shared by more than one format so they will behave differently depending on the format, so please read the command help (-h parameter) carefully.

#####Common parameters for all calculations:

| Parameters    | Description                                                     |
|---------------|-----------------------------------------------------------------|
| -n *name*     | Name of the calculation inside Create. (mandatory)              |
| -d *desc*     | Description of the calculation. (mandatory)                     |
| -i *filename* | Input file (mandatory)                                          |
| -o *filename* | Output file (OUTCAR on VASP, job.last on Turbomole).(mandatory) |
| -a *filename* | Additional file loading for calculation. (optional)             |

**Note:** Two calculations with the same name and in the same project are not allowed, otherwise upload process will fail.

#####Additional parameters for Turbomole

| Parameters     | Description                       |
|----------------|-----------------------------------|
| -oc *filename* | Turbomole coords file. (optional) |
| -oe *filename* | Turbomole energy file. (optional) |
| -ob *filename* | Turbomole basis file. (optional)  |

#####Additional parameters for VASP

| Parameters     | Description                  |
|----------------|------------------------------|
| -dc *filename* | VASP DOSCAR file. (optional) |
| -kp *filename* | VASP KPOINTS file (optional) |

| Examples  |                 |
|-----------|-----------------|
| *user$*   loadcalc -i ESR_TiF3.run -o ESR_TiF3.run.o33132 -n ESR_TiF3 -d "Sample description" | Upload **ADF** calculation and set its name to ESR_TiF3 |
| *user$*   loadcalc -i control -o job.last -oc coords -oe energy -ob basis -n Fe_Bipy -d Fe_Bipy | Upload **Turbomole** calculation and set its name to Fe_Bipy |
| *user$*   loadcalc -i INCAR -o OUTCAR -n NO_dim -d NO_dim | Upload **VASP** calculation and set its name to NO_dim |

To ease the usage of this command we have developed a group of helper Linux scripts to simplify shell upload 

| Script                     | Function |
|----------------------------|----------|
| [loadadf](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadgauss) | Upload **ADF** calculation             |
| [loadgauss](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadgauss) | Upload **Gaussian** calculation |                                    
| [loadturbo](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadturbo) | Upload **Turbomole** calculation|
| [loadvasp](/usage/uploading-content-to-create/using-shell-client/shell-automated-scripts.md#loadvasp)   | Upload **Vasp** calculations (Nudge Elastic Band and Dimmer are also included) |
