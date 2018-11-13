##Setting the embargo
Under some circumstances, ioChem-BD users need to restrict the access to some elements published on Browse module.

The most common situation is while publishing a manuscript in a journal and its supporting information needs to be accessed by the reviewers. In that special case, the published dataset has to be private to everyone but visible for a reduced number of users (reviewers).
In this case the users who are publishing to Browse module must activate the checkbox *Embargo published elements*

![](/images/PublicationOptions2a.png)

With this option activated, published elements will be visible inside its collection.

![](/images/embargoed-collection.png)

But will request for validation when trying to access any individual item.

![](/images/LoginRequired.png)

###Accessing the embargoed elements
Embargoed collections have its individual item pages restricted. So only using the collection *reviewer link* will have access to:

-   full list of metadata fields,
-   display molecule geometry in a specific viewer (JSmol)
-   view HTML5 resume
-   download calculation related files

Embargoed collections generate an unique URL to review its content, example:
https://iochem-bd-test.iciq.es/browse/review-collection/100/78/7d61fee92da1ef2ac787cccc

After publishing embargoed content from Create module, this links are displayed to the user so they can be shared.
Users can recover this links anytime on Create module by clicking on the black icon next to the project.

![This links point to the Edit Collection page](/images/EditPublishedElement.png "wikilink")

On the edit collection page, users can modify certain aspects of the published elements and also retrieve the Embargo link, this link won't appear if the collection doesn't have embargoed elements
![](/images/EditCollection3.png)

###Lifting the embargo

Once the content has been validated/reviewed, users can lift the embargo on the same *Edit collection* page . Clicking this button will lift the embargo on the collection:

![](/images/EditCollection4.png)

When the embargo is lifted, the embargo section on *Edit collection* page won't appear and review links will cease to work.
