[Index](index.html)  [Home](getting-started_home.html)

Api reference guide

The Sage X3 platform provides access to different API described below.

Additional X3 functions have also been developed to replace X3 version 6 functions. These functions are useful in the Versions 7 and above development process. They are also described in this page, module by module. The title of the entry corresponds to the function and the script file that was present in version 6.

# Technical libraries

## Access to the node.js server resources from an X3 script

These libraries are available only for V12 platform (in version V12 native mode or in Classic mode).

* [Call of an outgoing REST web service](api-guide_api-asyrrestcli.html#exec_rest_ws)
* [Access to the storage area](api-guide_api-asyrsarea.html)
* [Execution of javascript functions](api-guide_api-asyrwebser.html#exec_js)
* [Execution of an http request from web server](api-guide_api-asyrwebser.html#exec_http)

## Calling services provided by the X3 platform

Calling web services provided by X3 uses api1 protocol based on http requests:

* The general syntax of an http request is provided in the [API requests](api-guide_api-requests.html) page.
* The way to authenticate is provided in the [Authentication and single sign on principles](administration-reference_authentication-and-single-sign-on-principles.html) page.

The different services associated with the entities are:  
\* The list of entity instances (used by the query facet in the client) through a [GET query request](api-guide_api-get-query.html).  
\* The details of an entity instance (used by the details facet in the client) through a [GET details request](api-guide_api-get-details.html).  
\* Creation of an entity instance (used by the edit facet in the client) through a [POST request](api-guide_api-post.html).  
\* Updating an entity instance (used by the edit facet in the client) through a [PUT request](api-guide_api-put.html).  
\* Deletion of an entity instance (called from the query or details facet in the client) through a [DELETE request](api-guide_api-delete.html).

## Supervisor libraries

These libraries provide access to common services supplied by the supervisor layer. Some of them can be used only in *Classic code* code, some others can be used only in code associated to classes and representations, and some of them can be used independently.

### Libraries dedicated to classic code

### Libraries dedicated to V7 + code

* [Get a sequence number value](api-guide_get-a-sequence-number-value.html)
* [Get the sequence number definition for a given document](api-guide_get-sequence-number-assignment.html)
* [Additional methods of the context class](api-guide_api-context-methods.html)
* [Create a batch task request](api-guide_batch-request.html)
* [Create a URL to access to a classic page or a class/representation page](api-guide_create-url.html)
* [Send a mail with V6 technology (meladx) in the new development mode](api-guide_send-mail.html)
* [Manage asynchronous operations](developer-guide_managing-asynchronous-operations.html)
* [Manage V6 workflow on classes](developer-guide_managing-V6-workflow-on-classes.html)
* [Get parameters sent in the representation URLS](api-guide_get-URL-parameter-values.html)

### Libraries usable in both modes

* [Get a parameter value independently from context](api-guide_api-parameter-value.html)
* [Get links between legislation codes, sites and companies](api-guide_get-links-between-legislation-codes,-sites-and-companies.html)
* [Screen action for file selection](api-guide_file-selection-action.html)
* [Manage reauthentication of users](api-guide_user-authentication.html)
* [Manage sessions informations](api-guide_manage-sessions-informations.html)

## Web services

The technical platform provides a support for [SOAP web services](api-guide_soap-web-services.html). These web services work exactly as the V6 web services worked (the format is the same).

When working with classes and representation, it is also possible to work with [REST web services](integration-guide_ws-overview.html#ws-rest)

The list of SOAP web services added for platform purposes are here:

* [SOAP API for import/export of files](api-guide_api-soap-import-export.html)

## Miscellaneous

A library allows to launch an executable program (on windows only) from the browser (only in classic code). For security reasons, every user has to approve the use of the executable from browser at the first use.  
The corresponding documentation can be found [here](how-to_how-to-launch-exe-from-classic-session.html)

# Accounting libraries

## Currency management

| Subprog description | V6 library | Versions 7 and above library |
| --- | --- | --- |
| [Currency control](api-guide_contdev.html) | CONTDEV From TRTDEV | CONTDEV From TRTDEV\_SYRA |

  

[Index](index.html)  [Home](getting-started_home.html)