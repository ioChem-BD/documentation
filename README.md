#ioChem-BD chemical software documentation

The ioChem-BD platform [www.iochem-bd.org](http://www.iochem-bd.org) is a multi-headed tool aimed at managing large volumes of quantum chemistry results from a diverse group of already common simulation packages.sample text

The key modules managing the main tasks are to

1. upload of output files from common computational chemistry packages,
2. extract meaningful data from the results, and
3. generate output summaries in user-friendly formats.

A heavy use of the Chemical Mark-up Language \(CML\) is made in the intermediate files used by ioChem-BD. From them and using XSL techniques, we manipulate and transform such chemical data sets to fulfill researchers’ needs in the form of HTML5 reports, supporting information, and other research media.  
Please consider reading the [Basic introduction to ioChem-BD software](/platform-introduction.md) before continuing reading this wiki. Here you will view the features and data flows that this software contains in order to manage quantum chemistry calculations.


### Installation
  1. [System requirements](/system-requirements.md)
  2. [Required steps](/installation/required_steps.md) prior to installation 
  3. [Installation](/installation/installation.md) procedure 
  4. [User and group creation](/installation/user-and-group-generation.md)
  5. Define [backup policy](/backup-policy.md)
  6. [Post installation check steps](/installation/post-installation-check-steps.md)

### Usage

* [Create module](/usage/create-module-walktrough.md) walktrough
* [Uploading content](/usage/uploading-content-to-create.md) into Create
    * From [web interface](/usage/uploading-content-to-create/using-web-interface.md)
    * From [shell client](/usage/uploading-content-to-create/using-web-interface.md)
* [Publishing calculations](/usage/publishing-calculations.md) into Browse
* [Generating reports](/usage/generating-reports.md)
* FAQ

### Advanced system configuration 
* [Customizing system](/advanced-system-configuration/customizing-system-interface.md) interface
* [Replace HTTPS certificate](/other-operations/replace-https-certificate.md)
* Conversion [templates](http://www.iochem-bd.org/conversion/webhelp/index.html) reference

Read more about ioChem-BD at:  
[Managing the Computational Chemistry Big Data Problem: The ioChem-BD Platform](http://pubs.acs.org/doi/abs/10.1021/ci500593j) - Journal of Chemical Information and Modeling : DOI: 10.1021/ci500593j