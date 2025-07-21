[Index](index.html)  [Home](getting-started_home.html)

Index

All those documents stated here are intended to help you start using the new Versions 7 and above web technology.

If you are a user who has already access to the node.js platform and if you want to understand how to navigate through the pages and enter data, you may refer directly to the [User interface description pages](ui-definition_index.html).

For a better understanding of the platform associated to the Versions 7 and above, you will find 3 types of documents:  
\* A set of documents introducing the main concepts of this platform.  
\* A set of documents describing the installation and the prerequisites to use the platform.  
\* A set of documents explaining how to start the setup process and connect the platform to X3 folders.

# New platform concepts

* [Versions 7 and above technology for dummies](getting-started_v7-technology-for-dummies.html) details the new vocabulary used and how it maps to the previous Sage X3 version 6 concepts.
* [SData for dummies](getting-started_sdata-for-dummies.html) provides information on what is SData and what are its benefits.
* How is [security](getting-started_security.html) managed on the platform?
* What is [Classic mode](getting-started_classic-mode.html) and how does it work?
* How do the [Home pages](ui-definition_home-page.html) work and what are their limits?

# Prerequisites and installation procedures

Installing Sage X3 V7 (and further versions) requires to install the X3 servers and the node.js administration server. The procedure for installing the X3 server is almost the same as for the V6 servers. The installation of the Version 7 node.js server is new. When both are installed, it will become necessary to connect them together and to perform some administration operations in order to be able to use the ERP function on Version 7.

A demo folder is supplied in standard with Sage X3. The name of this folder is SEED, this means that the first endpoint which you can connect on (aside from the root folder X3) is the SEED endpoint. Once the complete installation path has been done, you can play with this folder as a self-training material.

Using Sage X3 will manage data in the relational database as well as in the mongoDB database. It is your responsibility to ensure the access security to mongoDB and to the relational database. The following [document](getting-started_data-security.html) explains the main precautions to take.

The documents that explains how to install the server are here:

* [Architecture schema](getting-started_architecture-schema.html): describes the architecture and identifies the different servers used.
* [Prerequisites](prerequisites_last-version.html): defines the technical prerequisites for the different servers.
* [Constraints using ERP and HRM on the same site](getting-started_erp-hrm-compatibility.html): describes the rules to respect when HRM and ERP are deployed with the same Syracuse server.
* [About files naming](getting-started_about-files-naming.html): defines how installation files are called on the installation support.
* [Sage X3 installation procedure](getting-started_sage-erp-x3-installation-procedure.html): defines the installation procedure for the different servers (database, process, application, web ... servers).
* [Console](configuration-console_console.html): describes how to use the configuration console.
* [Sage X3 upgrade guide](getting-started_quick-upgrade-guide.html): defines the procedure to upgrade from a release V7 or higher to the latest one.
* [How to upgrade a Version 6 folder](how-to_how-to-upgrade-a-version-6-folder.html): This document explains the procedure to upgrade a folder from version 6 to version 7.
* [Eclipse plugin installation and configuration](how-to_how-to-install-eclipse-and-use-it-to-debug-version-7-code.html): describes the way the Eclipse plugin is installed and set up.
* [Print server presentation and operation guide](getting-started_print-server-presentation-and-operation-guide.html): describes how the Print server component is installed and can be administrated.
* [Security best practices](getting-started_security-best-practices.html): How to set up security on the servers where Sage X3 is deployed.
* [Uninstallation procedure](getting-started_uninstallation-procedure.html): describes how to uninstall the SAFE X3 components.

# Manage the license

Sage X3 is a licensed software, protected by copyright. The use of the software is only permitted if you have acquired a valid license. The license is defined by a license file that must be installed on the server, and that gives you a given number of access rights identified by [badges](administration-reference_badges.html). The information that are inside the file are described in the [following documentation](getting-started_license-file-format.html).

You need at least one license supplied by Sage to run the product, but Sage can grant to partners the possibility to define additional licences files with their corresponding policy file.

The license file and the corresponding policy file are used to define the number of badges to connect as well as additional parameter values. The corresponding parameter values can be also seen in a [dedicated function](administration-reference_supervisor-license-visualization.html). A developer can have access to these parameter values in the context class.

# Starting tools and procedures

When all the servers are installed, a connection phase remains. Several operations have to be done:  
\* [Connection parameters](getting-started_connection-parameters.html): in the administration repository, technical information must be added to describe the connection between Version 7 web server and the X3 folders.  
\* [Sandbox configuration file](getting-started_sandbox-configuration-file.html): on the SAFE X3 hierarchy, a configuration file that indicates the directories the X3 engine has access to must be set up.  
\* [Certificate installation](getting-started_certificate-installation.html): In order to allow the connections between node.js repository and X3 servers to be established in a secured way, certificates have to be created and installed.  
\* [User creation tool](administration-reference_user-imports.html): A user repository is managed on the administration platform. It enables controlling safe connections to several folders from the node.js platform through a single sign-on. This tool allows to generate by default the user repository from user tables found in a folder.  
\* [Portal generation tool](getting-started_portal-generation-tool.html): This tool allows to create default dashboards, vignettes, and menu items from V6 portal and user menus.  
\* [Meta data switching tools](getting-started_meta-data-switching-tools.html): This tool is an assistant dedicated to developers who want to create Versions 7 and above dictionary items (classes, representation) and to use V6 objects in read-only pages mode.  
\* [Visual process recodification tools](getting-started_visual-process-recodification-tools.html): This tool generates additional meta data in dictionaries in order to handle version 6 visual processes in version 7.

Another point has to be noticed: the SEED demo folder is supplied with data, but the data is not indexed by the search engine, that means that the search index is delivered empty. This means that one of the first steps you have to do if you want the search box to return results is to index the Endpoints your platform has been connected to : at least the administration Endpoint and the SEED Endpoint, and of course other Endpoints whenever they exist.

This task is done through the [Search index administration page](administration-reference_search-indexes-administration.html).

# Technical documentations

Some technical documentations will be found in this section:

* [Load balancer](getting-started_load-balancer.html) describes how the load balancer works.
* [Virtualization](getting-started_virtualization.html) describes how the system is able to run in virtualized environments.
* [Security](getting-started_security.html) describes how you can set up the security on the web pages delivered by Sage X3.

  

[Index](index.html)  [Home](getting-started_home.html)