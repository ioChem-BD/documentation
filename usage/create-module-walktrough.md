# Create module walkthrough

The Create module is a single-page web application aimed at managing input and output files from computational chemistry research work, and to generate derived content from it. Create allows uploading, organizing, visualizing and curing your data, and share it with your project mates.
![Create module main page](/images/CreateMain.png)

The window is composed of three frames, some with several tabs:

* Navigation / Search / Reports frame
* Item Actions frame
* Item Details frame

![Frame composition](/images/CreateMainPageFrames.png)The default operation flow within the Create module starts by navigating/browsing user-uploaded content in the Navigation frame and selecting one of them to display its content. When any Item is selected, both the Item Actions frame and the Item Details frame get actualized and display additional data. Multiple element selection is allowed, this is normally associated to global operations, such for instance when publishing a project, or when generating reports. Multiple element selection also disables Item Actions and Item Details frames.

## Navigation frame

This frame is the entry point of all managing functionalities of the Create module. Three tabs allow us to select the current operative mode:

* Navigation
* Search
* Reports

To switch between modes, the user only has to click on each tab:
![Mode switch tabs](/images/CreateNavigationTabs.png)

### Navigation/Edition mode

The Navigation tab will display a navigation tree composed of nodes and leaves. From now on we will call it our _workspace_.
![Project and calculation navigation tree](/images/CreateNavigationTreeElements.png)
Each node represents what we call a **project**. This is just a container element, like a folder, and can contain other subprojects or simply  a set of single calculations, which are the basic element of your data. A calculation usually contains input files, CML converted output files, additional files, etc ... Navigation tab is the place to gather calculations and organize your data sets in the way you want to eventually publish them.


We can easily recognize projects inside the workspace by looking at the _Type_ column as they are labeled as _PRO_. Another way to recognize them \(when they contain child elements\) is by a small arrow next to their name. When clicking on it the project's content will expand or collapse.
Each leaf represents a **calculation**. It is an ending point and nothing can hang from it. This item represents all data associated to a single calculation, which comes straight from the output of computational chemistry packages.
By selecting a calculation, both the Item Actions frame and the Item Details frame get actualized and display additional data. We can easily discover the original software package used to run that  calculation by looking at the _Type_ column value:

* ADF: Calculation generated with [Amsterdam Density functional](https://www.scm.com/) software package
* GAU: Calculation generated with [Gaussian](http://www.gaussian.com/) software package
* TML: Calculation generated with [Turbomole](http://www.turbomole.com/) software package
* VSP: Calculation generated with [Vienna Ab initio Simulation Package](https://www.vasp.at/) software package

This list will increase as more calculations types are implemented: Molcas, ORCA ...

Other interesting columns that are worth explaning are:

* Description: Text about the project/calculation \(special symbols are allowed\).
* Status: Current element status. Possible values: created/published.
* Handle: Unique identifier of each published element, which can be accessed from the Browse module.This topic will be explained in depth in the section [Publishing Calculations into Browse](/usage/publishing-calculations.md)
* Published flag

There is a context menu to help with repetitive actions. For any element inside the workspace, you have to first select it clicking left click, and then right click it to see its available options in the context menu.

![Element context menu](/images/CreateNavigationTreeContextMenu.png)

Read the [Publishing Calculations](/usage/publishing-calculations.md) section or the [Generate reports](/usage/generating-reports.md "Generating reports") section to learn how to proceed further.

### Search mode

The Search tab will display a form where the user can query all uploaded projects/calculations. Multiple filters are available to refine queries.
Currently, only filter by administrative metadata:

* Name and description of the element, partial text matching search.
* Type of the element \(calculation software type\)
* Substructure \(if ChemAxon plugin is enabled\). This option displays a sketch panel where to draw a partial/full molecule to search for. This option is only available in those ioChem-BD instances that got explicit license from ChemAxon.
* Path, starting path to search for, see more at [path definition](/usage/uploading-content-to-create/using-web-interface.md#paths) section
* User who created the element and Group of users that element belongs to
* Access Permissions assigned to element
* Creation, modification dates
* Current element state

**IMPORTANT: Note that by enriching the Description field with meaningful information will allow you to look for those concepts when performing a search.**
![Multiple field search form](/images/CreateSearchForm.png)

After setting the search parameters you whish, click the _Search_ button to perform a query. A list of results will appear.
![](/images/CreateSearchFormResults.png)
We can click on any listed element to display its particular Item actions and details.
To perform a new query, the _Reset search_ button will clean the form and will bring you back to Search form.

### Report mode

This tab activates advanced operatives to process sets of calculations. This mode is fully reported in the [Generating reports](/usage/generating-reports.md) page. Please check it.

## Item Actions frame

This part of Create is in charge of displaying all actions related to a selected element in the Navigation/Search frames.
Projects do not have any specific action associated. By selecting a project, it will display the initial news page.
Calculations have the following actions, which are accessible in the tabs of this frame:

* 3D structure
* View results
* Download
* RAW CML

### 3D structure

This action displays the molecular structure or simulation cell.In the case of geometry optimization runs, it will show the final geometry. In the case of NEB calculations run with VASP, a special tab will allow visualizing all the points.
We use JSmol \(Javascript version of Jmol\) to display such structures \(and their cells in the case of periodic systems\).
Common JSmol operations:

* Hold left click + drag = Rotate molecule
* Central button scroll = Zoom in / out
* Hold Shift + double click + drag = Translate molecule
* Right click = Display JSmol options menu
  ![JSmol molecule visualization](/images/CreateItemAction3DStructure.png)

### View Results

Some results of the output file uploaded to ioChem-BD are translated into CML \(Chemical Markup Language\), an XML language oriented to chemistry. Such markup language allows easy further conversion into any existing format, such as an HTML5 report, a PDF file, or a JSON file.

Selected data is visualized, normally organized by content:

* General info: Contains calculation administrative and descriptive metadata such is: user name, calculation type, methods used, ...
* Settings: \(VASP only\), most relevant INCAR settings.
* Atom info: Atom type, coordinates and basis used. Eventually cell parameters, lattice vectors and atom valence.
* Molecular info: Implicit Solvation parameters, charge and multiplicity
* Job: Its content varies depending on the quantum chemistry package used to generate the calculation \(ADF software generates different output fields than VASP, for example\). For calculations with multiple jobs this section will appear more than once.

There is an exhaustive description on which fields are captured and how they are visualized. Please refer to [Conversion template reference](http://www.iochem-bd.org/conversion/webhelp/index.html)

![](/images/CreateItemActionViewResults.png)

### Download

This action allows downloading calculation files to your local filesystem.

![](/images/CreateItemActionDownload.png)

### RAW view

This action displays calculation files content inside a text area. On large files, it will start to download the file instead of displaying it.

![](/images/CreateItemActionRaw.png)

## Item Details frame

Any  project or calculation selected in our workspace will immediately refresh this form, displaying its administrative metadata.
Some fields are modifiable f. ex. name, description, owner group, assigned permissions. Other fields are fixed like owner user or creation date.
In the lower area of this frame three buttons provide important actions:

* Create project : Generates a project in the current path using the values in the form
* Modify : Replaces stored values for the selected element with values in the form
* Delete : Deletes selected  element.

![Item details frame with operation buttons](/images/CreateItemDetailsForm.png)

### Upload bar

On the bottom area of this frame there is an empty space. It is left blank intentionally to fit the upload bar. This bar will only appear while uploading calculations via the web interface, showing the progress of the uploading step..

![Upload bar](/images/CreateItemDetailsUploadBar.png)

