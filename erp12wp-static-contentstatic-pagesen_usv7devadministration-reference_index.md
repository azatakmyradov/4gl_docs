[Index](index.html)  [Home](getting-started_home.html)

Administration reference

The Administration reference documents describe the different functions or activities used to administrate a Sage X3 platform and solution. An activity is launched from the web client through a [launching URL](workbench-reference_launching-url.html) corresponding to a class and a representation. In every document with such an activity, the components of the URL will be introduced.

Different categories of activity exist. The list of activities presented here is given in the order defined by the Administration default menu page:

## Administration

|  |  |  |
| --- | --- | --- |
| Users[Users](administration-reference_users.html) The definition of all users able to connect on the platform.   [Groups](administration-reference_groups.html) The definition of groups; a set of users sharing access rights to endpoints and able to use a list of roles.   [Roles](administration-reference_roles.html) The definition of roles linked to personalized configurations for a user such as default dashboards, dedicated personalized pages, and so forth.   [Security profiles](administration-reference_security-profiles.html) The definition of security profiles that controls the administrative rights and are assigned to roles.  Licenses[License data](administration-reference_license-data.html) Defines the licenses available and the associated data.   [Badges](administration-reference_badges.html) Describes the assignment of badges to roles in order to handle license rights.   [License upload](administration-reference_license-management.html) Management of license files.  Web services[Classic SOAP web services](administration-reference_soap-generic.html) The setup of ingoing SOAP web services defined in Classic mode and published from node.js web server.   [SOAP pool](administration-reference_soapClassicPool.html) The setup of the pool that serves the ingoing SOAP web services.   [REST Web Services](administration-reference_outgoing-rest-web-services.html) The setup of outgoing REST web services. | Settings[Global Settings](administration-reference_global-settings.html)  The definition of global authentication settings.   [Locales](administration-reference_locales.html) The definition of locale rules for data presentation and input such as dates, numbers, and so forth.   [Password policies](administration-reference_password-policies.html) Define a password policy on the signature code in order to ensure the compliance with CFR-21 Part 11 regulations.   [External URL policies](administration-reference_external-url-policies.html) Defines the allowed external URL.   [Proxies configuration](administration-reference_proxy-configuration.html) The setup of proxy servers requested to access external services from the platform.  Authentication[LDAP](administration-reference_ldap.html) The setup of directories for LDAP authentication.   [Oauth2 servers](administration-reference_oauth2.html) The setup of servers for Oauth2 authentication.   [SAML2 authentication](administration-reference_saml2.html) The setup of SAML2 authentication.   [Connected applications](administration-reference_connected-applications.html) Allows to declare connected applications which will be used from a dedicated API.  Certificates[Certificates](administration-reference_certificates.html) The management of certificates.   [Certificates of Certification authorities](administration-reference_ca-certificates.html) The management of certificates signed by a certification authority. | Endpoints[Applications](administration-reference_applications.html)  The definition of the types of software connected to the node web server.   [X3 solutions](administration-reference_x3-solutions.html) The definition of the Sage X3 solution available to be connected on the node web server platform.   [Endpoints](administration-reference_endpoints.html) The definition of the data source associated with a widget or a page (a folder for the Sage X3 application).   [Batch controller](administration-reference_batch-server.html) Settings of Sage X3 batch controller for driving batch requests.  Servers[Hosts](administration-reference_host.html) The definition of the different hosts used to run version V12 processes in a cluster environment.   [Notification servers](administration-reference_notification-servers.html) The setup of servers that sends notification through email.   [CTI services](administration-reference_cti-services.html) Allows to define a CTI service for the Computer Telephony Integration.   [BO servers](administration-reference_business-objects-servers.html)  The definition of logical Business Objects severs corresponding to X3 Business Objects application servers.   [BO profiles](administration-reference_business-objects-profiles.html)  The definition of Business Objects profiles associated to Business Objects servers.  HRM Portal[HRM Servers](administration-reference_hrm-web-servers.html) Allows to creates HRM Servers configuration to be able to use HRM sites throught load balancer.   [HRM Sites](administration-reference_hrm-sites.html) Allows to creates HRM Sites configuration to be able to use Syracuse as HRM proxy. |

## Collaboration

|  |  |  |
| --- | --- | --- |
| [Teams](administration-reference_teams.html) The definition of lists of users sharing documents.   [Volumes](administration-reference_storage-volumes-management.html) The definition of logical volumes used to store or access documents. | Documents[Documents](administration-reference_documents.html) The documents shared by teams and managed in the mongodb document database.   [Word templates](administration-reference_word-templates-documents.html) The templates predefined for Word reporting purposes.   [Documents tags](administration-reference_tags.html) The definition of tags associated with documents shared by teams.   [Tags categories](administration-reference_tag-category.html) The definition of categories for tags. | Notifications[Notification events](administration-reference_notification-events.html) The setup of events that will trigger automatic notifications to some users.   [Mail templates](administration-reference_mail-templates.html) The setup of templates that describes how the body and the other characteristics of a mail sent from an entity is computed.   [Notification themes](administration-reference_notification-themes.html) The setup of themes used as style sheets for emails sent by the platform. |

## Authoring

|  |  |  |
| --- | --- | --- |
| Pages[Navigation pages](administration-reference_navigation-pages.html) The definition of navigation pages that describes the organization of the links to the ERP pages organized as a "site map".   [Home pages](administration-reference_home-pages.html) The definition of home page (or landing pages) that contains blocks in which [menu items](administration-reference_menu-items.html) are displayed to produce a user friendly page that contains indicators or processes.   [Menu items](administration-reference_menu-items.html) The definition of links on pages that appear in landing pages.   [Menu submodules](administration-reference_menu-submodules.html) List of [menu item](administration-reference_menu-items.html) (links in home pages).   [Menu modules](administration-reference_menu-modules.html) Super-blocks of links (organized in sub-modules) used in [home pages](administration-reference_home-pages.html)   [Menu categories](administration-reference_menu-categories.html) Categories assigned to [menu items](administration-reference_menu-items.html). | [Customized pages](administration-reference_pages.html) The description of the pages modified by personalization. | MobileThe menu items present here correspond to the new mobile/tablet client with auto-adaptative layout capabilities.   [Mobile applications](administration-reference_mobile-applications.html) Describes the new mobile applications .   [Mobile dashboards](administration-reference_mobile-dashboards.html) Allows to create mobile dashboards.   [Mobile gadgets](administration-reference_mobile-gadgets.html) Allows to create mobile gadgats included in the mobile dashboards.   [Upgrade mobile dashboard](administration-reference_upgrade-mobile-dashboard.html) A tool that allows to generate new mobile applications from the previous mobile dashboards. |

## Utilities

|  |  |  |
| --- | --- | --- |
| Export[Export profiles](administration-reference_export-profiles.html) The definition export profiles used to export data and meta data from Endpoints.   [Personalizations management](administration-reference_personalization-management.html) The tool that allows to define filter used to extract dashboards, portlets, menu items, and personalized pages information in a format that makes it possible to import them in another repository.   [Resources packs](administration-reference_resourcepacks.html) Set of export files.  Update[About](administration-reference_about.html) Returns technical information about the platform installed.   [Updates](administration-reference_updates.html) A new way to upgrade folder in "one click" | Import[Import tool](administration-reference_import-tool.html) Tool used to import data in the administration database.   [X3 Users import](administration-reference_user-imports.html) A tool that allows to read the user in a folder database in order to create or update users in the administrattion database.   [Menu profile import](administration-reference_menu-profile-import.html) Allows to import menu items from a Sage X3 folder   [Import sessions](administration-reference_import-session.html) The import session management.  Sage EDI Online[DSN submissions](administration-reference_DSN-submissions.html) List of DSN submissions sent to Sage EDI Online.   [CRM requests](administration-reference_CRM-requests.html) List of CRM requests sent to Sage EDI Online.   [Sage EDI Online portal](administration-reference_sage-EDI-online-portal.html) Direct access to the Sage EDI Online portal. | Installation**Install addin for Office** A link to download the Office plugin   **Install addin for Outlook** A link to download the Outlook plugin   **Ilog Connector** A link to download the connector for Scales and Gantt Ilog modules   **Report developer Connector** A link to download the plugin that allows local development on Crystal Reports. For more information, see the following [document](workbench-reference_reports-sandbox.html) |

## Usage

|  |  |  |
| --- | --- | --- |
| [Search index management](administration-reference_search-indexes-administration.html) The definition of the parameters for the search index updates.   [User broadcasts](administration-reference_user-broadcasts.html) The definition of the parameters for user broadcasts.  Automate[Scheduler](administration-reference_scheduler.html) The definition of scheduled tasks (automation).   [Server logs](administration-reference_server-logs.html) The management of logs on operations that runs on the administration server. | Sessions management[License display](administration-reference_licenseview.html) Displays the current license consumption.   [Sessions information](administration-reference_sessions-information.html) The sessions currently active on the node server and the associated X3 sessions. | Logs[Host trace](administration-reference_traces-records.html) The management of technical traces for support purposes.   [History Logs](administration-reference_mongoDB-traceability.html) Traceability of the modifications on the MongoDB database.   [X3 session logs](administration-reference_x3-session-logs.html) Allows you to create logs on the X3 engine for debugging purposes. |

# Miscellaneous documents

These documents refers:

* either to functions that are not directly available from administration menus, but from Quick administration link in the [user preferences panel](ui-definition_user-preferences-panel.html).
* or to additional information not directly linked to pages.

The following pages are available:  
\* [Administration reference Super Administrator](administration-reference_super-administrator.html): The definition of a super administrator with administration rights on the platform.  
\* [Administration reference Dashboards](administration-reference_dashboards.html): The definition of portal pages containing [portlets](administration-reference_portlets.html) that can be menus, ERP or administration pages, and external pages. This entity has been replaced by [home pages](administration-reference_home-pages.html) and [navigation pages](administration-reference_navigation-pages.html) and is now only used for the description of mobile applications.  
\* [Administration reference widgets](administration-reference_portlets.html): The autonomous components found in a dashboard.  
\* [Administration reference Configuration File](administration-reference_configuration-file.html): A file located on the node web server that defines default parameters.  
\* [Administration reference Friend servers](administration-reference_friend-servers.html): The definition of other node servers on which the platform can connect.  
\* [Administration reference Outgoing REST Web services](administration-reference_outgoing-rest-web-services.html): Definition of external web services that can be called from SAFE X3 platform.

# Supervisor Setup functions

In this section, you will find the supervisor functions that have already been switched to Versions 7 and above technology, and the new functions related to Versions 7 and above technology. These functions are related to a Sage X3 endpoint, and handle meta data stored in a Sage X3 folder. The links are organized by supervisor menus.

## Development

The supervisor development menu handles all the functions related to the workbench. The corresponding documentation can be found [here](workbench-reference_index.html).

### Utilities

This sub-menu of development contains tools that didn't change since the version 6, except for the following list:

* [Supervisor License Visualization](administration-reference_supervisor-license-visualization.html): The management the rights associated to the licenses installed on a given folder.
* [Tool that checks the compliance of addons, vertical, specific developments to be hosted on cloud](administration-reference_supervisor-vertical-consistency-controls.html). The objective is to have the best resilience possible when applying patches in the environment.

## Setup

This menu gives access to setup operation at the folder level:

* A direct link from this menu to folders management is present. The corresponding documentation is available in the standard help path.
* A particular operation, the folder validation or revalidation, generates all the structure of the folder and performs the updates needed, for instance, when the version changes. A technical documentation available [here](administration-reference_folder-validation.html) describes the technical process of folder validation.

In the setup menu, we also have several sub-menus:

### Statistics

In this menu, the definition of the statistical functions are present. On all these functions, the same user interface than in V6 is used, and the way the data is stored didn't change since version 6. But the validation of the statistics generates a script that accesses to the statistical data from Versions 7 and above native pages. This is described in the following link:

* [Supervisor administration Statistics](administration-reference_supervisor-administration-statistics.html): The implementation of the Sage X3 statistics with the new client.

### Printouts

In this menu, the requester functions are present. On all these functions, the same user interface than in V6 is used. But for the Query tool and the Graphical query tool, the validation of the queries generates a script that runs differently the queries in order to access to the query data from Versions 7 and above native pages. This is described in the following link:

* [Supervisor Administration Requester](administration-reference_supervisor-administration-requester.html): The implementation of the Sage X3 requester with the new client.

## Usage

This menu includes some tools related to the administration platform. The following functions are related to the new platform or have been changed in version V12:

* [Attachment upgrade](administration-reference_attachment_upgrade.html) : the tool that upgrades the attachment tables in order to store the file path with a volume.

## Interactive dashboards

This menu includes some tools related to the version 6 dashboards and some features are still relevant for the home page, especially:  
\* the portal view that define default values usable as query parameters (parameter `&portview=value`). See the [requester documentation](administration-reference_supervisor-administration-requester.html#addparam) for more details.  
\* the visual process editor, that works like previously and is documented in the version 6 setup menu pages documentation. Some tricks are described to implement the links in the [following documentation](how-to_how-to-create-visual-process-links.html).

  

[Index](index.html)  [Home](getting-started_home.html)