##Publishing calculations
Calculations uploaded into the Create module are only accessible to registered ioChem-BD users, this will usually be comprised of a small group of individuals that conform the research group/center. Their calculations will not be accessible until they are published in the Browse module, the public module of ioChem-BD.
Before moving to the publication mechanism, it is interesting to read again the section about the organizational elements that conform each module: [ioChem-BD organizative elements](/platform-introduction.md#modular-architecture).
So published projects become Collections and published calculations become items on the Browse module, it is a mere grammatical change to align with DSpace software naming convention. Once published, both elements are linkable, searchable and viewable publicly.

### Publication requirements
To perform calculation publication, users must meet the following requirements:
   * Publishing user must have defined (on Browse module) a community where to publish.
   * Publishing user must have administrator rights to publish on such community, so he/she will has to be able to create collections and publish items.

The steps required to create a community and assign its administrator falls upon ioChem-BD's system administator and are described on [publishing endpoints definition](/installation/publishing-endpoints-definition.md) page.

### Publication steps
####Select the elements to publish
On Create module, navigate to the project where the desired calculations reside. We can select an individual calculation by clicking on it, or using multiselect with *Ctrl + Click*, *Alt + Click*. Another way to select calculations is right clicking on parent project and choose *Select child elements* from its context menu.

> Note: You must select the project **and its inner calculations** prior publishing. If you only select the project element and not its content you will publish the project but empty of contents. `

Once desired projects and calculations are selected, right click on the current selection to display its context menu. Then select *Publish* option.

![Calculation selection](/images/CreatePublishSelection1.png) 

A dialog box will appear asking for our account password: 

![Credential validation](/images/CreatePublishCredentials.png)

If an error message appears at this point, please read the FAQ entry about [no publishing community defined](/FAQ#nopublishingcommunity).

A new form will be presented, showing all end points available on the Browse module.

![Selected elements form](/images/CreatePublishSetEndpoint1.png)

In the publication process, a project hierarchy will be replaced for a *collection* element with all its subprojects concatenated as a Unix path.

> Note: If they exist, we can select the endpoint where to publish by using drag and drop. Already published elements (the ones with a green tick) cannot be moved because their path has been already set. We can change published calculation and project names by clicking the element name.

###Publication form steps

![Publication options](/images/PublicationOptions.png "wikilink")

On right side of the publication form there is a group of option tabs that allow to define published element metadata and its relation to journal articles.
#####Step 1: Titles and description
This tab allog to configure information related to published calculation:
   * Calculation naming convention : We can choose to prepend full parent projects name into calculation name or set only calculation name
   * Description field: If checked, calculation description field will be added as a metadata field and will be publicly accessible on Browse module.

![Titles and description tab](/images/PublicationOptions1.png) 

#####Step 2: Publication details
The next tab has two options:
   * Generate DOI for top projects: will request a DOI identifier that points to the published collection
   * Embargo published elements: if marked, all published elements will be embargoed.

DOI determination can take some minutes to resolver because it requires to contact third party services (CrossRef). Once DOI has been assigned, you will receive an email with the DOI for the published collection.
The second option will allow you to embargo (restrict) the access to your published content.You can read more about the embargo feature [on this page](/Calculation_embargo "wikilink"). 

![Publication details tab](/images/PublicationOptions2.png)

#####Step 3: Dataset type
This tab allows to add extra manuscript information in the case that the dataset is part of the supporting information of a paper.
You can define the manuscript title, DOI and Journal. In the situation that the paper doesn't have a valid DOI yet, you can check the checkbox *Not yet published, will provide it later*. 
![](/images/PublicationOptions3.png)

#####Step 4: Additional fields
The last step is used to define other authors and institutions related to the dataset. There is also a listbox with chemical terms to enrich the published elements, such terms will be later indexed by Browse module to ease data search.
Once all the step forms have been filled, we will click the Publish button. 
![Additional fields tab](/images/PublicationOptions4.png) 
After the publication process has ended, a resume window will display the link to edit published elements on Browse module and, only if you checked the embargo option, another link to review embargoed elements. 
![](/images/PublicationResume.png) 

<span id="editCollection"></span>
###Published elements manipulation
In the navigation frame, published elements will display a green tick on the right side.
Published projects and subprojects will also have an additional black tick that points to the Browse *Collection edit* page. 
![](/images/EditPublishedElement.png) This page allows to:
   * Change published collection name
   * Set related article information
   * Lift embargo ([read more here](/Calculation_embargo "wikilink"))
   * Copy reviewers link

On the  page that shows, the first section allows to change title, subtitle and description of the published collection:

![](/images/EditCollection.png)

The next section allows set publisher metadata and embargo options:

![](/images/EditCollection2.png)

###View published elements from Create
The projects and calculations published have a handle and a green tick on its right side. 

![Publication handle](/images/CreatePublishHandle.png)

Clicking on the handle link will navigate to the published Browse content. Each collection can hold multiple Items (calculations) inside. 

![Published Collection items](/images/BrowsePublishedElementsDetail.png) 

Each published item displays the uploaded input file, an output converted CML file, additional files and its metadata. 

![Published item detail](/images/BrowsePublishedElementsDetailItem.png "wikilink")