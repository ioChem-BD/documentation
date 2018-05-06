### Upload content using the Create web interface
####Paths

All elements inside the Create module have an associated path to define its position among all others elements. It can be revised by looking on top of the *Item details* form: 

![Element current path](/images/CreateDetailsPath.png)

Paths work the same way than OS folder/file paths, we can navigate them up/down and inside/out.
All paths start with a fixed string that contains the username : **/db/username**. This is defined as the root of our path, from here we can create all the projects we need.

> Note : No calculations are allowed to be uploaded on root path. They must be held inside a project.

####Creating a project
Projects are the base to start uploading calculations and content in a hierarchical manner. Over time, as uploaded content gets larger, nested projects and a more complex ordering structure will become necessary to manage research data. Its up to users to build a structure that suit their needs.

So projects created on root path will be now called root projects. To create them, you must first clear the current path by clicking the *Refresh* button, placed on top on the Navigation frame. 
![Refresh and reset path button](/images/CreateNavigationTreeRefresh.png)

With the current path cleared and set to root path, we can start filling in project details on the Item details frame.
**Project name and description fields are mandatory**. No symbol characters can be used in the project name (as they are not allowed either in directory names inside current OS). ![Create project form, note root path on top](/images/CreateItemDetailsCreateProject.png) 

Once edited we must click on *Create project* button. Navigation frame will refresh our workspace and our project will appear inside the project hierarchy.
To create subprojects inside an existing project, we need to click on that project and replace its name and description in the Item details frame, after that we can click on *Create project* and it will be generated inside the selected parent project.

####Calculation upload
To upload a calculation into a project we have to first click on that project. Then on the upper right panel the Create web interface will display a form where we will fill in the calculation name, its description etc.
![Calculation upload form](/images/WebUploadForm.png)
> Note: *Name* field must not contain blank spaces or special characters like \*@\[\]..., otherwise they will be normalized to an underscore symbol.

Then we have to click on the specific uploaded format to display its possible file upload combinations, which vary depending on the selected calculation type
![Calculation type selection](/images/WebUploadForm2.png)

> Note: Files marked with an asterisk (\*) must be attached (are mandatory) so as to upload this calculation successfully.

Some files can be attached more than once, this is the case of the *Additional file* button. Such special option will display a form where we can upload multiple files, we can now add images, reports, PDF files, and so on. Here is an example of this kind of form.
![Multiple file upload form](/images/WebUploadForm3.png)

> Note: If we upload multiple files with the same name, the Create module will rename them using a numeric index, for example if we attach two geometry.txt files, second one will be named as geometry_2.txt.

Now we can click on the *Load Calculation* button to start uploading our calculation. A progress bar will appear on the lowest right panel. It will display upload progress, bear in mind that it can take some time to convert and digest our file depending on the size of the source files.
![Upload queue status](/images/WebUploadForm4.png "wikilink")

This progress bar will also display errors that occurred during file upload. We can click on the warning image to display a longer explanation of upload failure.
When all of our calculations are uploaded we can click on the *Refresh* button on the *Simple Navigation* tab to refresh its content an display new uploaded calculations. <span id="shellupload"></span>