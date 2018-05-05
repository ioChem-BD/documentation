#About
The massive use of simulation techniques in chemical research generates terabytes of information daily, which constitutes a serious problem known as Big Data. The main obstacle for managing large information volumes is their storage in such a way that facilitates data mining as an strategy to optimize the processes that will enable facing the challenges of a new sustainable society based on knowledge and the rational use of existing resources.

The concepts underlying this project span from the definition of standards to the treatment, hierarchical storage and data recovery, and facilitating data mining of the Theoretical and Computational Chemistry's Big Data, having as main goal the creation of new methodological strategies that will promote an optimal reuse of results and accumulated knowledge. The present project aims at creating a distributed network of repositories for a full management of digital chemistry files.

The main node of the network runs the Find Module, which acts as central server and is feed by any new data published in the repositories. Find Module provides a fast chemical-aware search engine open public service and is hosted at the Barcelona Supercomputer Center (BSC). Also, the first public-access node provided by BSC.

Other ioChem-BD modules automatize relevant data-extracting processes and transforms raw numerical data into labeled data in a database.  It provides the researcher with tools for validating, enriching, publishing and sharing information, as well as tools to access, post-process and visualize data. The final goal is to contribute building a new reference tool in research. Users include computational chemistry research groups worldwide, university libraries and related services, and high performance supercomputer centers. 
![none|frame|ioChem-BD function overview diagram](/images/IoChem-BD_diagram.png "wikilink") <span id="modular"></span>
##Modular architecture
The services available in the repository are actually provided by different modules: Create, Browse and Find. Each one has different objectives in managing chemistry digital assets, and they both complement each other. While there exists one only Find, there are as many Create/Browse modules as nodes in the network.
### Create module
This web service is intended for use in private manner. It is fed with user files uploaded via a web browser or from any box running a Linux shell client, see [Uploading Content page](/usage/uploading-content-to-create.md).

Features:
   * Private interface, content accessed by user permission only
   * Productivity-oriented GUI designed using the zKoss framework
   * Automated document, data graph/chart generation: PDF files of supporting information reports, reaction energy profiles, etc ...
   * Search by keywords, chemical substructure and administrative metadata
   * Compact and intuitive design
   * Publish user selected data to the companion Browse Module

The data is structured inside this module using **projects** and **calculations**, like folders and files inside a file system. Each calculation has to be enclosed inside a project, and a project can be on the root or enclosed inside another project as a subproject. Data organization is totally left to the user's own criteria.

A REST API is in permanent development. Find the documentation here (need to include the link).

### Browse module
This web service is intended for public access. It is fed with projects and calculations published from the Create module.
The Browse module uses entities such are **Community**, **Collection** and **Item** to organize the information.
   * Communities are the basis of hierarchy organization
   * Collections are the end point where to publish elements
   * Items are viewable digital assets. An item can be made of a single or a group of files, all of them related to the same calculation: input and output files, graphics, associated documents, and more.

We can make a direct correspondence of elements between Create and Browse organizational elements:

| Create entity | Browse entity |
|---------------|---------------|
| -             | Community     |
| Project       | Collection    |
| Calculation   | Item          |

It is up to ioChem-BD's system administrator to generate users, groups and communities where to publish content. Collections and items are automatically generated during the process of publication from the Create module.




