---
title: Publishing endpoints definition
permalink: /Publishing_endpoints_definition/
---

Once our users and groups are generated, we must consider building the entity hierarchy on the Browse module to store all published elements coming from the Create module.
As we explained on [Basic introduction to ioChem-BD software](/Basic_introduction_to_ioChem-BD_software "wikilink") page, the Create module will be used to work with calculations coming from HPC clusters. On this module we will be able to read a HTML5 summary of the most important calculations fields, their geometry and perform searches, generate reports and so on.
All this work is done privately inside the Create module but it can be published into the Browse module to share your calculations with the rest of the world. This process is done by publishing Create projects and calculations into Browse, but that raises a question: where to publish on Browse module? So that is the reason why it is necessary to generate a publishing hierarchy on the Browse model to hold all these new calculations and projects.
The hierarchy inside Browse is really up to administrator's choice and needs. Here are some example of this organization:

-   a top community with your institution's name, then inside it, their research groups community and inside them, its researchers community. Here we expect every researcher to publish inside his/her named community:

<!-- -->

    Institute of Chemical Research of Catalonia
    ├── Carles Bo group
    │   ├── Bandeira, Nuno
    │   ├── Gonzalez Fabra , Joan
    │   ├── Melgar, Dolores
    │   └── Serapian, Stefano
    ├── Feliu Maseras group
    │   ├── Besora, Maria
    │   ├── Fernandez, Victor
    │   ├── Kuniyil, Rositha
    │   └── Lakuntza, Oier
    └── Nuria Lopez group
        ├── Bellarosa, Luca
        ├── Capdevila, Marçal
        ├── Garcia, Miquel Alexandre
        ├── Li, Qiang
        └── Rellán, Marcos

-   or rather create multiple top communities per research group and inside them each researcher's community

<!-- -->

    Carles Bo group
    ├── Bandeira, Nuno
    ├── Gonzalez Fabra , Joan
    ├── Melgar, Dolores
    └── Serapian, Stefano
    Feliu Maseras group
    ├── Besora, Maria
    ├── Fernandez, Victor
    ├── Kuniyil, Rositha
    └── Lakuntza, Oier
    Nuria Lopez group
    ├── Bellarosa, Luca
    ├── Capdevial, Marçal
    ├── Garcia, Miquel Alexandre
    ├── Li, Qiang
    └── Rellán, Marcos

-   or even one top community per researcher (no grouping per research group)

<!-- -->

    .
    ├── Bandeira, Nuno
    ├── Bellarosa, Luca
    ├── Besora, Maria
    ├── Capdevial, Maçal
    ├── Fernandez, Victor
    ├── Garcia, Miquel Alexandre
    ├── Gonzalez Fabra , Joan
    ├── Kuniyil, Rositha
    ├── Lakuntza, Oier
    ├── Li, Qiang
    ├── Melgar, Dolores
    ├── Rellán, Marcos
    └── Serapian, Stefano

-   or only create top communities per research group and no subcommunities at all, then all group reseachers will publish directly into his/her group community, grouping all calculations inside it.

<!-- -->

    Carles Bo group
    Feliu Maseras group
    Nuria Lopez group

-   another option instead of creating communities by group/person could be to create them by calculation type, molecule type, please choose the structure you feel that will fit your needs better.

Community generation
--------------------

Once we know how Browse will be structured we will start by creating the top community/ies.
As administrator we will click **Browse** &gt; **Communities and collections** on the upper menubar option.
[none|frame|Communities and collections menu option](/File:Admin_communities_and_collections.png "wikilink") On the next page we will click on the *Create top level community* button. [none|frame|Admin add new top community page](/File:Admin_addtopcommunity.png "wikilink") From the next form we must fill in the mandatory *Community name* textbox. We can also attach an image describing the community or append more info on the Description text field. [none|frame|Admin community add form](/File:Admin_addtopcommunity2.png "wikilink") Once this is done we will click on the **Create** button, and our community will be created
<span id="subcommunity_generation"></span>

### Subcommunity generation

Depending on the needed hierarchy, you will have to generate new subcommunities inside your top communities.
As administrators, we will navigate to the base community via **Browse &gt; Communities and collections**, then click on the desired community.
From the right sidebar we will choose *Create Sub-community* option and follow the same steps as when we create a top community. [none|frame|Community options panel](/File:Admin_addsubcommunity.png "wikilink") <span id="community_publishers"></span>

Assign community publishers
---------------------------

Once our publication structure has been defined, our last step as administrator is to define who will publish and where he/she will publish
To assign publication rights to a community we must define its administrators.

> Note: the ioChem-BD system administrator account has higher levels of administrator than simple users managing their publishing community. So the system admin will be able to remove published collections and items, whereas other users will not.

We will first navigate to the desired community, in this example this will be a specific user community. From the sidebar we will click on the *Edit* button. [none|frame|Edit community sidebar](/File:Admin_addcommunityadmin.png "wikilink") From next form we will click on *Create* administrator button on the right sidebar. [none|frame|Community permissions toolbar](/File:Admin_addcommunityadmin2.png "wikilink") In the new form we will choose which users or groups of users are allowed to publish inside this specific community.
In this demo case we are working with a user community so we will add this only user as administrator. If we are working with a group community with no users, as described in the fourth example, we can add a users' group (right panel) instead of a list of single users (left panel). [none|frame|Set community administrators](/File:Admin_addcommunityadmin3.png "wikilink") We will do so for every user / group of users that we want to be able to publish, otherwise users will not be able to publish in the Browse module.

Resume
======

This last steps conclude the ioChem-BD system installation and configuration. Let us recap all steps taken until we get here:

1.  Gather important system configuration parameters
2.  Create database and start software installation
3.  Copy Create license to installation directory
4.  Start webserver and login as administrator
5.  Generate users and groups from Browse module
6.  Create communities and subcommunities where users will be able to publish their digital assets.

Adding new users to ioChem-BD will require following the steps described in [user generation](/User_and_group_generation#users "wikilink"), and creating a community where to publish or only add a user into a group that has publishing communities defined.