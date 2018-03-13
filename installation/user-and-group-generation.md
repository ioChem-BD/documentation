##User and group generation
<span id="useraccountgeneration"></span> The Browse module content is publicly accessible by anonymous users, the Create module, however, requires authentication to access. That is why we must define system users and user groups.
Administrator has two mechanisms to generate user accounts:

* Batch generation using a csv formatted file
* Manual generation using web forms

It is advised to use batch generation mechanism initially to speed up account generation, after that, adding new users can be done with either manual or batch mechanism.
<span id="batch"></span>

###Users/Group structure generation (.csv batch)
We can use this webpage to speed up user and group generation. It will take as input a group of csv formatted lines and process it, performing automatically:

* User creation (with automatic username deduction)
* User group creation
* Publication endpoint generation (if option is checked)
* Send password reset email to all new users (if option is checked)

The following steps will be performed on the Browse module and from an administrator account, the same that we would have defined during installation.
First, we will login by clicking on upper right menu bar "Sign on to" -&gt; "My Browse" button.

![Admin login](/images/First_login.png)

You will be redirected to CAS (Central Authentication Service) page.
On this page we will type **admin.email** and **admin.password** on its login form. If we have any problems with our password, we can click on the *Forgot your password?* link to reset it.
After that, the Browse module will change and a link to the Create module will appear on the right upper menu bar

>Note: You cannot access the Create module directly from an admin account, you need to create a user account to get access through it

On the options on upper right menu bar we will click on Administer.

![Admin administer](/images/Admin_administer.png)

The menu bar will change to administrator mode and more options will be accessible, you can navigate through them but now we will focus on the **Access control** menu.
When clicking on it three options will be displayed, we will focus on first one, *E-People*.
From Administer EPerson page we will click on the *Add multiple E-Person (csv)...* button:

![Admin create user form](/images/Admin_createuser.png)

Next page will display a large textarea where we will paste the list of users to generate. Pasted text must follow this rules:

* All fields must have a value
* All fields must be delimited by semicolons ;
* Don't need to use double quotes on text fields, even if they contain white spaces
* You can use diacritics and symbols on user first and last name and also on user's group name.

![Admin create user via batch process](/images/Admin_createuser_csv.png)
Every line will contain all information about a single user. It will appear in this order:

1. User email
2. User first name
3. User last name
4. User group (the group of users where he/she will belong to)

The user group field is used to easily build user groups, so users with same user group field will be included in that group. Example:

```code
malvarez@iochem-bd.es;Moisés;Álvarez Moreno;Carles Bo group
jprats@iochem-bd.es;Joan;Prats Rubio;Carles Bo group
mperez@iochem-bd.es;Miguel;Pérez Álvarez;Carles Bo group
jbel@iochem-bd.es;Jose;Bel Ortiz;Nuria López group
ncolet@iochem-bd.es;Núria;Colet Serrano;Nuria López group
```

So if we use this lines, ioChem-BD will generate five users and two groups of users:

* Carles Bo group : with users Moises, Joan and Miguel
* Núria Lopez group : with users Jose and Núria

In this case we have named our user groups with the name of the group leader but you can use other naming convention as can be the group research type or whatever that suit your needs.

Note: If this groups already exists (because you already used this .csv tool) and you only want to append the new users to it, please be very careful to set the names of the groups equals to the existing ones, you can check group names on *Access control-&gt; Groups*.

<br/>Otherwise a new user group and a new publishing community will be generated and those users will be assigned to it.


####Options
There are two checkbox options at the bottom of this page that will help on other side aspects of user generation process.
![Admin create user options](/images/Admin_createuser_csv_options.png)
First one is labeled ''Generate publishing communities for each user group and assign created users to it ''. It will help us on defining publishing endpoints on Browse module. If it is checked, the process will also generate a community with the name of the user group where our new users can publish their content into Browse module. Using previous example lines would generate two publishing communities called *Carles Bo group* and *Núria Lopez group*.
In case we need a more complex publishing structure please uncheck this option and read carefully [Publishing endpoints definition](/installation/Publishing_endpoints_definition.md) page.
![Admin automatically generated publishing communities](/images/Admin_createuser_csv_community.png)
Last option is labeled ''Send reset password email to generated users ''. If checked, it will send a *reset password* email to all newly created users, so they can set their account password to start using ioChem-BD software. Finally, a textarea will appear with a resume of all unprocessed lines, displaying the reason why they failed. So its administrator duty to correct such lines and create those users again (only the wrong ones).
![Admin create users via csv, error resume](/images/Admin_createuser_csv_error_resume.png)

###Users/Group structure generation (manual)
The following steps will be performed on the Browse module and from an administrator account, the same that we would have defined during installation.
First, we will login by clicking on upper right menu bar "Sign on to" -&gt; "My Browse" button.
![Admin login](/images/First_login.png)
You will be redirected to CAS (Central Authentication Service) page.
On this page we will type **admin.email** and **admin.password** on its login form. If we have any problems with our password, we can click on the *Forgot your password?* link to reset it.
After that, the Browse module will change and a link to the Create module will appear on the right upper menu bar.

>Note: You cannot access the Create module directly from an admin account, you need to create a user account to get access through it

On the options on upper right menu bar we will click on Administer.
![Admin administer](/images/Admin_administer.png)
The menu bar will change to administrator mode and more options will be accessible, you can navigate through them but now we will focus on the **Access control** menu.
When clicking on it three options will be displayed, we keep on these two:
* E-People : To create, modify and delete ioChem-BD users
* Groups: To build groups of users.

Note: If we want to create multiple users and groups, it is recommended to create all users first, then create all groups, and finally setting each user's Create parameters.

####Creating users
<span id="users"></span> From Administer EPerson page we will click on the *Add E-Person...* button:
![Admin create user form](/images/Admin_createuser.png) On the next form we will :

* set the user's e-mail on **E-mail** and **LDAP /CAS NetID:** textboxes
* add additional user information
* check **can log in**
* leave the Create fields empty

This is an example of a user account creation:
![Admin create user](/images/Admin_createuser2.png)
Finally we click on the **Reset password**' button, the user will then be saved in the database and a reset password link will be sent to the user's e-mail.

####Creating groups
Now that we have created all ioChem-BD users, it is time to group them inside user groups.
We can gather users by research group, team leader, or even create a group with all users. Users can belong to multiple groups.
Click on **Access control** and then on **Groups** menu button. On the next form we will click on **Create group**.
![Admin create group form](/images/Admin_creategroup.png) On the next form we will:
* set group name (avoid using blank spaces, use underscores to separate words)
* assign users to group

then click on **Update group** button.
![Admin assign group users form](/images/Admin_creategroup2.png)

####Assign Create parameters to each user
Once our users and groups are created and assigned we will setup Create account parameters for each user.
To do so we will go back to the **Access control** and **E-Person** menus to edit our newly-created users.
We will edit each user (that we want to have access to the Create module) by setting the last two parameters.
* Create username: must be unique and with no blank spaces nor symbols. Examples : malvarez, jsmith, ...
* Create main user group: we set users main group, all new calculations and projects generated in Create will be set as this group by default
![User edit, Create fields lighted](/images/Admin_createuser3.png) Then we click on the *Save* button to finish. We must repeat this operation for all users.

------------------------------------------------------------------------

These steps conclude ioChem-BD user structure generation. Any additional new users must be added by following the steps defined in the previous section [Creating users](/#users).
The last step in our system configuration is defining endpoints on the Browse module where users can publish their calculations. Refer to [Publishing endpoints definition](/installation/Publishing_endpoints_definition.md) page.