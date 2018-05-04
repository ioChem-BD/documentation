# Create module walkthrough

The Create module is a single-page web application aimed at managing input and output files from computational chemistry research work, and to generate derived content from it. Create allows uploading, organizing, visualizing and curing your data, and share it with your project mates.  
![Create module main page](/images/CreateMain.png)

The window is composed of three frames, some with several Tabs:

* Navigation / Search / Reports frame
* Item Actions
* Item Details

![Frame composition](/images/CreateMainPageFrames.png)The default operation flow within the Create module starts by navigating/browsing user-uploaded content in the Navigation frame and selecting one of them to display its content. Whon the Item actions and Details frames. Multiple 

## Navigation frame

This frame is the entry point of all major functionalities of the Create module, and will allow us to change the current operative mode to

* Navigation,
* Search and
* Report generation.

To switch between modes, the user only has to click on each tab:  
![Mode switch tabs](/images/CreateNavigationTabs.png)

### Navigation/Edition mode

The Navigation tab will display a navigation tree composed of nodes and leaves, from now on we will call it our workspace.  
![Project and calculation navigation tree](/images/CreateNavigationTreeElements.png)  
Each node represents a **project**. A container element of other subprojects and calculations. A place to gather related calculations and data sets, they could be used to manage a paper's supporting information calculations, to keep an ongoing work calculation collection, .... It could be similar to a folder inside an OS file structure.  
We can easily recognize projects inside the workspace by looking at the _Type_ column, they will be marked as _PRO_. Another way to recognize them \(when they contain child elements\) is by a small arrow next to their name. When clicking on it the project's content will expand/collapse .  
Each leaf represents a **calculation**. It is an ending point and nothing can hang from it. This item represents a computational chemistry calculation, coming straight from the output of quantum chemistry packages.  
Selecting them will expand more related information on the _Item actions_ and _Item details_ frames. We can easily discover the original software package that created this calculation by looking at its _Type_ column:

* ADF: Calculation generated with [Amsterdam Density functional](https://www.scm.com/) software package
* GAU: Calculation generated with [Gaussian](http://www.gaussian.com/) software package
* TML: Calculation generated with [Turbomole](http://www.turbomole.com/) software package
* VSP: Calculation generated with [Vienna Ab initio Simulation Package](https://www.vasp.at/) software package

This list will increase as more calculations types are implemented: Molcas, ORCA ...

Other interesting columns that are worth explaning are:

* Description: A larger description of project/calculation \(special symbols are allowed\).
* Status: Current element status. Current possible values: created/published.
* Handle + Published flag: Identifier assigned to the element when it is published into the Browse module, this will be explained in depth in [Publishing calculations into Browse](/usage/publishing-calculations.md)

There is a context menu to help with repetitive actions. For every element inside the workspace, you must first select it with a left click and then right click it to see its available options.

![Element context menu](/images/CreateNavigationTreeContextMenu.png)

On the next page \([publishing calculations](/usage/publishing-calculations.md)\) you will learn to populate your workspace.

### Search mode

The Search tab will display a form where the user can query all uploaded projects/calculations and add multiple filters to refine queries.  
Currently we can only filter by administrative metadata:

* Name and description of the element, partial text matching search.
* Type of the element \(calculation software type\)
* Substructure \(if ChemAxon plugin is enabled\). This option displays a sketch panel where to draw a partial/full molecule to search for.
* Path, starting path to search for, see more at [path definition](/usage/uploading-content-to-create/using-web-interface.md#paths) section
* User who created the element and Group of users that element belongs to
* Access Permissions assigned to element
* Creation, modification dates
* Current element state

In future developments we will index calculation internal metadata to index and search by calculation type, final energy, and any user-defined field.  
![Multiple field search form](/images/CreateSearchForm.png)

After setting all search parameters we must click on the _Search_ button to perform a query on current module data. A list of results will appear with matching results.  
![](/images/CreateSearchFormResults.png)  
We can click on each listed element to display its particular Item actions and details.  
To perform a new query, the _Reset search_ button will clean the form and go back to Search form.

### Report mode

Due to its complexity, this mode is fully reported on the [Generating reports](/usage/generating-reports.md) page, please check it.

## Item actions frame

This part of Create is in charge of displaying all actions related to a selected element on the Navigation/Search frame.  
Projects do not have any specific action associated, selecting a project will only display a module news page.  
Calculations have the following actions:

* 3D structure
* View results
* Download
* RAW CML

### 3D structure

This action displays the calculation's molecular structure, in the case of optimization calculations it will show their final geometry.  
We use JSmol \(Javascript version of Jmol\) to display such structures \(and their cells in the case of crystals\).  
Common JSmol operations:

* Hold left click + drag = Rotate molecule
* Central button scroll = Zoom in / out
* Hold Shift + double click + drag = Translate molecule
* Right click = Display JSmol options menu
  ![JSmol molecule visualization](/images/CreateItemAction3DStructure.png)

### View Results

All calculations uploaded to ioChem-BD are translated into CML \(Chemical Markup Language\), an XML language oriented to chemistry. Such markup language allows its easy conversion into any existing format, such as an HTML5 report.  
This report contains multiple sections, grouped by its content type:

* General info: Contains calculation administrative and descriptive metadata such as: user name, calculation type, methods used, ...
* Settings: \(VASP only\), most relevant INCAR settings.
* Atom info: Atom type, coordinates and basis used. On structure calculations there will be cell parameters, lattice vectors and atom valence.
* Molecular info: Solvation parameters, charge and multiplicity
* Job : Its content varies depending on the quantum chemistry package used to generate the calculation \(ADF software generates different output fields than VASP, for example\). On calculations with multiple jobs this section will appear more than once.

There is an exhaustive description on report fields per calculation type on our webpage, please refer to [Conversion template reference](http://www.iochem-bd.org/conversion/webhelp/index.html)

![](/images/CreateItemActionViewResults.png)

### Download

This action allows downloading calculation files to our local filesystem.

![](/images/CreateItemActionDownload.png)

### RAW view

This action displays calculation files content inside a text area. On large files, it will start to download the file instead of displaying it.

![](/images/CreateItemActionRaw.png)

## Item details frame

Every selected project or calculation in our workspace will immediately refresh this form, displaying its administrative metadata.  
Some fields are modifiable f. ex. name, description, owner group, assigned permissions. Others are fixed, like owner user or creation date.  
On the lower section of this frame there are three buttons that:

* Create project : Generates a project in current path using existing form fields
* Modify : Replaces current selected element with form information
* Delete : Deletes selected path element.

![Item details frame with operation buttons](/images/CreateItemDetailsForm.png)

### Upload bar

On the lower side of this frame there is an empty space, it is left blank intentionally to fit the upload bar. This bar will only appear while uploading calculations via the web interface.

![Upload bar](/images/CreateItemDetailsUploadBar.png)

