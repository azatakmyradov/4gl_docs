[Index](index.html)  [Home](getting-started_home.html)

Classic mode

## Introduction

**In order to work in Versions 7 and above native pages, a version 6 Sage X3 function needs to have new associated dictionary entities, and also to reorganize the code in a way that it works properly in service mode along with classes support.**

**An existing tool enables users to generate classes and representations from an object; however, it is restricted to support 'read' operations only (the query and details pages).**

## The Classic mode

Switching an existing function to a full V12 mode is a significant time consuming effort. To guarantee the availability of all version 6 functions with the new Versions 7 and above client, even if development or business partners lack the time needed to switch the code, a **Classic** mode is embedded in the Versions 7 and above client.

The following principles are applied:

* In a dashboard, a menu item refers to a version 6 function by its name. At execution time, a page displays the version 6 screen and connects to the Sage X3 server using the version 6 protocol.
* The version 6 function launched from the Versions 7 and above home page or navigation page (as mentioned above), works with the same features as in version 6. A left list is available, the controls are blocking and synchronous, the cursor movement is completely controlled by the server, and a limited page personalization is allowed on such pages.
* The look of the screen has been reviewed to be as close as possible to the new Versions 7 and above pages.

This mode called **Classic mode** does not require any modification in the existing version 6 code to work.

## New display mode switch

Switching an existing object to a new page in display-only mode is faster and requires less modifications. This is done by creating a class and a representation with only the support of the 'read' operation. An [automated tool](getting-started_meta-data-switching-tools.html) decreases the amount of work to be performed to support this feature.

Only the query, detail, and lookup facets are supported in this case. The user can choose a record from an entity through a selection list and display the details of the selected record.

If the switch has been performed for some Sage X3 functions:

* The access to these functions will be done in native Versions 7 and above mode with a query facet page and a detail display. Personalization will be possible on these pages.
* When an 'edit' operation is requested on a record, the client will automatically switch to **Classic mode**, and a page having a left list displaying the current record will appear. The user can then update the data as in version 6.

## More details on the Classic mode

The UI of the Classic pages is described in detail in the [UI Classic pages](ui-definition_classic-pages.html) documentation.

  

[Index](index.html)  [Home](getting-started_home.html)