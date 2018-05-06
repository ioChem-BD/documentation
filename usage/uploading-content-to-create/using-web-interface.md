### Upload content using the Create web interface
####Paths

All elements inside the Create module have an associated path to define its position. It can be reviewed by looking on top of the *Item details* form: 

![Element current path](/images/CreateDetailsPath.png)

Paths work the same way as OS folder/file paths, so you can navigate them up/down and inside/out.
All paths start with a fixed string that contains the username: **/db/username**. This is defined as the root of your path, from here you can create all the projects you need.

> Note :  Calculations are not allowed to be uploaded in the root path. Calculations must be held inside a project.

####Creating a project
Projects created in the root path will be called root projects. To create them, you must first clear the current path by clicking the *Refresh* button, placed on top on the Navigation frame. 
![Refresh and reset path button](/images/CreateNavigationTreeRefresh.png)

With the current path cleared and set to root path, you can start filling in project details on the Item details frame.
**Project name and description fields are mandatory**. No symbol characters can be used in the project name (as they are not allowed either in directory names inside current OS). ![Create project form, note root path on top](/images/CreateItemDetailsCreateProject.png) 

Once edited you must click on *Create project* button. Navigation frame will refresh our workspace and your project will appear inside the project hierarchy.
To create subprojects inside an existing project, you need to click on that project and replace its name and description in the Item details frame, after that you can click on *Create project* and it will be generated inside the selected parent project.

####Calculation upload
To upload a calculation into a project you have to first click on that project. Then on the upper right panel the Create web interface will display a form where you will fill in the calculation name, its description etc.
![Calculation upload form](/images/WebUploadForm.png)
> Note: *Name* field must not contain blank spaces or special characters like \*@\[\]..., otherwise they will be normalized to an underscore symbol.

Then you have to click on the specific format to display its possible file upload combinations, which vary depending on the  calculation type
![Calculation type selection](/images/WebUploadForm2.png)

> Note: Files marked with an asterisk (\*) must be attached (are mandatory) so as to upload this calculation successfully.

Some files can be attached more than once; this is the case of the *Additional file* button. Such special option will display a form from where you can upload multiple files, add images, reports, PDF files, and more. Here is an example of this kind of form.
![Multiple file upload form](/images/WebUploadForm3.png)

> Note: If you upload multiple files with the same name, the Create module will rename them using a numeric code, for example if you attach two geometry.txt files, the second one will be renamed as geometry_2.txt.

Now you can click on the *Load Calculation* button to start uploading your calculation. A bar will appear on the lowest bottom right panel. It will display a upload progress bar. Bear in mind that converting and digesting your fils can takea while, as function of your source files size.
![Upload queue status](/images/WebUploadForm4.png "wikilink")

The progress bar will also display errors that migh otccurr during file upload. You can click on the warning image to display a longer explanation about the upload failure (keep it and it send it to us).
When all of your calculations are uploaded you can click on the *Refresh* button on the *Simple Navigation* tab to refresh its content. The, you can navigate through your newly uploaded data. <span id="shellupload"></span>