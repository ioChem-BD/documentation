#ioChem-BD introduction
The massive use of simulation techniques in chemical research generates terabytes of information daily, which constitutes a serious problem known as BigData. The main obstacle for managing large information volumes is their storage in such a way that facilitates data mining as an strategy to optimize the processes that will enable facing the challenges of a new sustainable society based on knowledge and the rational use of existing resources.
The concepts underlying this software span from the definition of standards to the treatment, hierarchical storage and data recovery, and facilitating data mining of the Theoretical and Computational Chemistry's BigData, having as main goal the creation of new methodological strategies that will promote an optimal reuse of results and accumulated knowledge. The present project aims at creating a platform of services in the cloud for a full management of digital chemistry files.
ioChem-BD automatizes relevant data-extracting processes and transforms numerical data into labeled data in a database. This platform provides the researcher with tools for validating, enriching, publishing and sharing information, as well as tools in the cloud to access and visualize data. The final goal is to build a new reference tool in research, bibliography management and services to third parties. Potential users include computational chemistry research groups worldwide, university libraries and related services, and high performance supercomputer centers. 
![none|frame|ioChem-BD function overview diagram](/images/IoChem-BD_diagram.png "wikilink") <span id="modular"></span>

##Modular architecture
This chemical software is split into two modules: Create and Browse. Each one has different objectives in managing chemistry digital assets, and they both complement each other.
### Create module
This web service is intended for private use inside your institution. It is fed with calculations uploaded via a web browser or from HPC clusters via a shell client, see [calculation upload page](/usage/Uploading_content_into_Create.md "wikilink").
Features:

   * Private interface, content accessed by user permission only
   * Productivity-oriented GUI designed using the zKoss framework
   * Automated document, data graph/chart generation: PDF files of supporting information reports, energy reaction profiles, etc ...
   * Search by keywords, chemical substructure and administrative metadata
   * Compact and intuitive design

The data are structured inside this module using **projects** and **calculations**, like folders and files inside a file system. Each calculation has to be enclosed inside a project, and a project can be on the root of the project or enclosed inside another project as a subproject. Data organization is totally left to the user's own criteria.
### Browse module
This web service is intended for public access. It is fed with projects and calculations published from the Create module.
The Browse module uses **Community**, **collection** and **item** entities to manage information.
   * Communities are the basis of hierarchy organization
   * Collections are the end point where to publish elements
   * Items are viewable digital assets. An item can be made of a single or a group of files, all of them related to the same calculation: input and output files, graphics, associated documents, and so on.

We can make a direct correspondence of elements between Create and Browse organizational elements:

| Create entity | Browse entity |
|---------------|---------------|
| -             | Community     |
| Project       | Collection    |
| Calculation   | Item          |

It is up to ioChem-BD's system administrator to generate users, groups and communities where to publish content. Collections and items are automatically generated during calculation publication on the Create module.