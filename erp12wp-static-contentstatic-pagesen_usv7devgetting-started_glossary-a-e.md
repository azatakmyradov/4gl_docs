[Index](index.html)  [Home](getting-started_home.html)

Glossary A-E

# Access code

An access code is an alphanumeric sequence that restricts access to resources or data. It can be associated with a database record, a column of data (a field) in a table, an activity (a function), an operation, and so forth.

An access code acts as a lock. Once it has been configured on a resource, users have access to this resource only if the access code is included in their assigned list of access codes.

An access code is not specific to a particular user; it is meant to be assigned to many [users](getting-started_glossary-r-z.html#users) through a setup of userâs rights that command the access mode. These rights represent the user's personal privileges and restrictions on a given access code. For example, a user can be given a Read access right on the table âWagesâ in the database, can display the data, but cannot modify nor delete it. On the other hand, a user can have No Execution access right on a process.

**Example:**

The administrator creates a CFO access code and assigns it to the following elements:

1. The wages account.
2. The operation used to post an accounting entry.
3. The authorized credit level property in the customer record.
4. A detailed representation of the credit history for customers.

On this newly created code, the user grants a user named MARTIN access rights that are restricted to Read  
(no Write or Execution authorized).  
Through the CFO access code, MARTIN has the following rights on the above mentioned data and functions.

* To view the wages account (Read access right) without the ability to change its characteristics   
  (Write access right), nor to post accounting entries on this account (Execution access right).
* To display the authorized credit level on a customer record without the ability to update it.

However, the Read access right does not entitle MARTIN to post an accounting entry nor use the credit history inquiry (as Execution access right has been denied).

As per the previous example, the Execution access right can be applied differently depending on the corresponding entity. The way the Execution access right is set on an account determines whether it is allowed to post accounting entries, hence the Execution access right on a representation corresponds to the right of use. For this reason, a detailed representation of the credit history for customers (4 above) is not authorized.

This feature is generic. It already exists in Sage X3 Version 6 and is used in the same manner in Version 7.

Note that a user can be granted rights on all access codes. This privilege is usually granted to administrators. Filtering by access code is disabled for [users](getting-started_glossary-r-z.html#users) having this privilege.

# Accessors

In an object oriented language, a class has [methods](getting-started_glossary-f-p.html#method) which are functions implementing the access interface to an instance of the class. An accessor is a function that provides access to a [property](getting-started_glossary-f-p.html#property) of a class. A manipulator is the term that designates functions used to update a property, but a unique term is used for the Sage X3 engine combining both types of functions.

The evolution of version 7 for the Sage X3 engine makes it possible to define the following accessors:

* `getvalue` is a method called to read the value of a property.
* `setvalue` is a method called to assign a value to a property.

Accessors invoke rules. Rules are dedicated methods called by the engine or the supervisor. For Sage X3, three types of rules exist:

* `Getvalue` triggers an action when a value is read. This method is called by the read accessor.
* `Control` is used to verify the validity of a property when its value changes. The only action that is performed is to accept or refuse the update.
* `Propagate` is used to trigger updates on other properties when a property changes value in an instance.

The `Control` and `Propagate` rules are called by the `setvalue`.

*Note: The initialization (`Init`) method is neither called by the engine nor by the supervisor, but by the development partner once a new class instance has been created. Its use is not necessary if the instance is used only for read purposes.*

## Activity

In a *Document* type interface, the user manages a document and uses a ribbon with a complex list of actions that enables the user to interact with the document. The version 7 platform has not been built that way. Its interface has been designed as a set of activities (for example, *create an order*, *display an order*, or *modify the order which is being displayed*). A user performs only one activity at a time, but other activities can be opened from the current activity, either by replacing the current activity by another, or by opening another activity in a new tab of the browser.

A clear distinction is made between ***stateless*** and ***stateful*** activities:

* ***Stateless*** activities are queries or inquiries. A query is sent to the user interface. Once the answer is given, the server is available for another query which is not necessarily linked to the previous one.
* ***Stateful*** activities are used for operations where a context is necessary to ensure the management of the activity. This context is named a [working copy](getting-started_glossary-r-z.html#working-copy). Typically, data modifications or creations are managed by *stateful* activities.

## Application shell

The application shell is the minimal envelope that appears in the browser when an activity is in progress. This envelope remains lean as it is the case in modern web applications, to have the maximum screen space available for the data directly linked to the activity. This is also done deliberately to avoid the endless bars of choices or esoteric icons. In its place the top bar will provide the main information such as a home button, user defined shortcuts, a search box, and a button that provides access to an extended bar with additional shortcuts including the list of pending drafts, the access to the personalization mode, the possibility to change the user or [role](getting-started_glossary-r-z.html#role) for a connection, and so forth.

A right bar gives access to the current operations (the default is displayed in blue). Finally, a small panel located at the bottom right corner gives access to alerts.

Version 7 has been created as an application using all the Web browser capabilities. Thus, you can define activities as favorites by using the native favorites function in the browsers, using the back button to return to the previous activity, and so forth.

## Application

[SData](getting-started_glossary-r-z.html#sdata) uses URLs to address the resources, resource collections, schemas, and service operations that are exposed by a service. An application is the segment of a resource that identifies the software program managing the resource. In SData URL syntax, Application segment is one of the URL components that include, among others,'Contract' and 'Endpoint' segments.

For example, the application segment for the 'Version 7 administration platform' and the 'Sage X3 software program' can be:'Syracuse' (this was is the internal code name of the original project) and 'Sage X3'. While corresponding contract segments can be 'Collaboration' for 'Syracuse' and 'ERP' or 'HRM' for 'Sage X3'.

The [endpoint](getting-started_glossary-a-e.html#endpoint) identifies a solution and a server folder for the Sage X3 program, which is not the case for the administration platform where the Mongodb database host and port are defined.

## Asynchronism

The controls linked to the version 7 user interface are performed asynchronously, which means that the client sends the modifications done by the user on the fly, but no acknowledgement from the server is necessary to continue the entry.

In standard entry conditions for a connected user, the feedback of the server will come quickly, error messages can be displayed, and default values sent as the entry is performed with no time delay. If the connectivity is bad or if the server is busy, the display of the control results will be delayed without stopping the entry.

## Authentication

The authentication is the action used to identify a user. Two authentications exist in the version 7 administration environment:

* **Syracuse authentication:** This is the first authentication in which the administration server manages its own user referential, and the passwords are controlled by an SSO system. Once [Users](getting-started_glossary-r-z.html#users) are authenticated, they can access their own customized portal to access the data in [mashup](getting-started_glossary-f-p.html#mashup). The data displayed in a portal can originate from several data sources such as different folders, web pages, and other solutions using the version 7 protocol.
* **Sage X3 authentication:** This is the customary Sage X3 authentication by user and folder. A mapping exists between the administration users and the Sage X3 users. This mapping is managed by the administration module.

By default, a user connected to the platform can access the portal displaying public information without signing in. If this happens, a link will be present on the page for users to authenticate and to access their personalized portal.

## Authorizations

Authorizations define the rights granted to a user in a given situation (executed function, data in which it is executed).  
A distinction can be made between vertical habilitations (defining functions, fields, and actions a user can access) and horizontal habilitations (filters on data).

The main authorization principles found in Sage X3 are the following:

* The [roles](getting-started_glossary-r-z.html#role) define functions in an organization such as an accountant, stock manager, and sales representative. Roles are associated with authorizations on activities, operations, entities, and their properties.
* Security profiles are used to associate roles and operational entities such as companies, sites, groups of companies, and groups of sites.
* Row filters are used to define more restrictive filters on some properties using values such as horizontal habilitations. They were named roles in version 6 and before, but the role terminology now has a definition that is closer to the standard computing terminology.
* [Access codes](getting-started_glossary-a-e.html#access-code) establish transversal filtering that can be simultaneously horizontal (excluding rows in tables) and vertical (excluding operations, columns, and/or activities). An access code is associated with the [properties](getting-started_glossary-f-p.html#property) or the records that have to be filtered, and the access to the artifacts protected by the activity codes can be granted with read, write, and execution rights.

A user is associated with a set of [security profiles](getting-started_glossary-r-z.html#security-profile), possibly with row filters linked to a list of values, and optionally with an access code list and their authorizations. This set of characteristics defines what a user is allowed to access.

## Automatic backup

An automatic backup for a draft is automatically performed on the client, but also on the node.js server every time a field is left and a new field entry starts. If any interruption occurs on the client, on the node.js server, or on the Sage X3 server, it will be possible to resume the entry from the latest intermediate saved state.

## Block

A block is a set of fields grouped in the user interface for application logic reasons. A block has its own characteristics such as position in the page, list of fields, and CSS styles. The [personalization mode](getting-started_glossary-f-p.html#personalization-mode) allows a user to change these characteristics to adapt the user interface to their needs. As the blocks are defined in the [representation](getting-started_glossary-r-z.html#representation) dictionary, a default field organization can be defined in standard version.

Blocks are part of the user interface organization, but the grouping in blocks has no influence on the application logic.

## Breadcrumb

A breadcrumb is a [representation](getting-started_glossary-r-z.html#representation) used to present a navigation path in the application software. The client uses this type of graphical component in some dedicated cases such as the personalization mode.

## Card view

A card view is a [representation](getting-started_glossary-r-z.html#representation) of a line in a [grid](getting-started_glossary-f-p.html#grid) as a [block](getting-started_glossary-a-e.html#block). This mode can be used for a line or for all the lines of a grid. The card view mode can also be horizontal if few lines are present on a grid.

## Child classes

A [class](getting-started_glossary-a-e.html#class) can enclose child classes for example, an order including its order lines. It is important to differentiate between the child classes (a set of data is stored) and the references (a product code linked to a product record).

Two types of child classes exist:

* The **âfriend classesâ**, for which the CRUD basic methods are managed by the parent class. This is the case for order lines: the order creation method takes into account the persistence of the lines in the database.
* The **âlinked classesâ**, which have their own CRUD basic methods that are called by the parent class. This is the case for the creation of an address (dedicated entity) that can be called by several document creation methods such as orders, delivery slips, and invoices.

## Child representation

A child representation is a representation included in another [representation](getting-started_glossary-r-z.html#representation). It is used to define a card view type representation in a [grid](getting-started_glossary-f-p.html#grid), and also to define globally a set of [properties](getting-started_glossary-f-p.html#property) linked together for which user interface actions can be defined. For example an address block, for which actions such as geo-localization can be defined and used generically in a set of harboring representations.

## Class

A class is a data structure containing [properties](getting-started_glossary-f-p.html#property) previously named fields. A class can contain properties of any type such as date, alphanumeric, numeric, rich texts or plain texts, binary data such as images, sounds, movies, instances of other linked classes, references to instances of other classes, and arrays composed with the previous listed elements.  
For example, an Â« order Â» class, once instantiated, may contain properties referring to instances of other classes such as the delivering or invoicing address, as well as an array of references to order lines.

The version 7 supervisor manages a class dictionary used to define them, with an optional association to a data type.  
A class has a type that can have four different values:

* ***Normal*** means that accessors can be associated with the properties of the class, but no methods for CRUD operations exist.
* ***Persistent*** means that accessors can be defined and CRUD operations are supported by the class. This is the case for the classes associated with resources usually persisted in a database: the data managed by the class will finally be stored in a database and retrieved through a query. The class definition is then the equivalent of the Sage X3 "object" (in version 6 terminology). On instances of such classes, CRUD methods (Creation, Read, Update, and Delete) will be used. The CRUD management on a class is more powerful than the object management implemented in version 6. If a class represents a document that persists in the database with a header and level(s) of nested lines, the supervisor manages the updates of the header and all the details with no limit of nested level, where the version 6 supervisor only took into account the header level.
* ***Technical*** is used when a class has no accessors, but might have associated methods.
* ***System*** is used for classes that have no accessors and in which no methods can be defined except kernel inbuilt and non-modifiable methods.

The class includes a set of methods describing business logic controls, default values, and functions used for data manipulation on the class properties.

Using a class and its methods can be done through a user interface with a [representation](getting-started_glossary-r-z.html#representation) and its facets, and also through a service (Web service).

## Classic pages

A function developed in version 6 cannot work directly with version 7 if the code and the meta data have not been reviewed and reorganized. The version 7 client use requires the separation between the business rule associated code (in [classes](getting-started_glossary-a-e.html#class)) and the UI associated code (in [representations](getting-started_glossary-r-z.html#representation)). The counterpart of this reorganization is that the code is more robust and easily reusable because the supervisor layer takes into account the updated [operations](getting-started_glossary-f-p.html#operation) even on complex [classes](getting-started_glossary-a-e.html#class).

As this reorganization of the code can take time and to simplify the use of version 6 dictionary elements and code in version 7, an additional UI layer named Transition has been developed for version 7. Hosted by the web server, this layer supports a UI enclosed in the version 7 shell using the version 6 interface logic with a style that is very close to the version 7 style.

In this mode, a connection is established between the Web server and the Sage X3 engine in equivalent conditions to the existing ones in version 6. The node.js server acts as a simple proxy. The switch from a version 7 native page to a Classic page is relatively transparent (the Classic page overlaps the version 7 native page), but the advanced functions ([personalization](getting-started_glossary-f-p.html#personalization-mode)) are limited. The Classic pages component is able to run the version 6 screens without any code reorganization.

## Collection

A collection is a set of [properties](getting-started_glossary-f-p.html#property) present in [classes](getting-started_glossary-a-e.html#class) or [representations](getting-started_glossary-r-z.html#representation) that can be seen as an array of multi-valuated properties. Usually, in the user interface, all the fields associated with a collection are present on a grid.

A collection is identified by a code in the class and representation dictionaries. The collections code used in a class or representation are associated with a minimum and maximum number of occurrences defined directly or through an activity code. Every property of the class or representation can belong to a collection defined in the class or representation.

From a technical point of view, a collection in the Version 7 platform is implemented as an array of child instances. The class these instances are defined by can be either a child class defined in the dictionary, or a technical class created on the fly to group the properties declared in the collection.

## Column

A column corresponds to a property in a database table. This terminology is closer to the usual terminology for databases and will, in the future, replace the Field term that was previously used in Sage X3.

It is important to note that some columns are automatically managed by the Sage X3 version 7 supervisor. These columns have a predefined name and are as follows:

* 'CREUSR', 'UPDUSR', 'CREDATTIM', and 'UPDDATTIM' correspond to the user who has created the record, as well as the date and time of the operation. The 'CREDAT' and 'UPDDAT' should be considered as deprecated, even if they can still be used for compatibility reasons.
* 'AUUID' stores the [UUID](getting-started_glossary-r-z.html#uuid) of the record.
* [UPDTICK](getting-started_glossary-r-z.html#updtick) is a column that is not visible in the dictionary because it is automatically created and updated by a trigger to manage the updates in optimistic mode.

## Contract

In the [SData](getting-started_glossary-r-z.html#sdata) terminology, a contract defines a set of exchange formats. It is the third segment in the SData URL after the server and the application. For version 7, it provides the context of a [Sage X3 application](getting-started_glossary-a-e.html#application) (for example, ERP and HRM).

## CSS 3

CSS (Cascading Style Sheets) is a computer language used to describe the presentation for HTML and XML documents.

The standards defining CSS are published by the World Wide Web Consortium (W3C). Introduced in the middle of the 90s, CSS has been frequently used in the conception of web sites and well supported by the web browsers in the years around 2000. The development of the third level of CSS started in 1999, simultaneously to the development of CSS 2.1.

CSS3 has become modular to ease its updates and its implementation by user agents with more diverse capabilities and needs such as graphical browsers, vocal browsers, and mobile browsers. The browser can consequently implement subsets of CSS3.

Version 7 uses CSS3 to have a clear separation between the capabilities of the client and the way they are presented and used in the user interface.

## Dashboard

The term dashboard is no more used (it has been used at the beginning of the version 7 to define a page made up of [gadgets](getting-started_glossary-f-p.html#gadget)). It has been replaced by two elements: the [landing pages](getting-started_glossary-f-p.html#landing-page) and the [navigation pages](getting-started_glossary-f-p.html#navigation-page).

## Data access rules

The data access rules enable [users](getting-started_glossary-r-z.html#users) to define a set of strict filters on the data when necessary by defining a link between an access rule code and filtering fields, which are properties defined on entities stored in the repository.   
A given user can be related with a list of access rules with associated filter values. This defines strict filter rules on the corresponding data. The data list is filtered by considering that the filtering field can only have the values associated with the rule for the user.

For example, imagine that the 'GROUP' rule defines a filter on business partners, invoices, orders, and receipts on the value of the group customer code property, on every entity concerned. If this rule is activated for a user associated with the SAGE value, only the business partners, orders, invoices, and receipts having SAGE as a group customer will be visible by the user. This is a very restrictive filter.

Note that this type of filter was named 'role' in version 6 and previous versions of Sage X3. The former Sage X3 'role' has been renamed as 'filtering field' associated with access rule codes because the meaning of 'role', as defined by security specialists, is different.

## Database link

This âhistoricalâ expression in Sage X3 is obsolete and must be replaced by the word ["join"](getting-started_glossary-f-p.html#join) even if the engine instruction that implements it remains Link.

## Dataset

In [SData](getting-started_glossary-r-z.html#sdata), a dataset identifies the data source used for a given application and contract. In version 7 for Sage X3, it identifies the combination (solution and folder).

## Disconnected mode

The version 7 user interface is able to work in disconnected mode (usually in an almost temporary way). When an entry is in progress, the information linked to the entry is transmitted in a differential and asynchronous mode. When the server answers, the client returns the modifications made since the last reception. If the server is not available, the entry is not stopped: the modifications made are stored in the local cache. Some controls cannot be performed in this mode especially those based on business logic rules not implemented on the client or not available in cache, and the controls requiring a database access. These controls will finally be performed when the server is available, which will happen quickly in case of temporary disconnection (for example, a mobile device in bad network conditions), or later if the draft is reused to resume an interrupted entry.

## Display mode

This term denominates a mode of functioning for the version 7 interface where the user browses the application data by following hypertext links, just like any information website works. In this mode, the version 7 client works in [stateless](getting-started_glossary-a-e.html#activity) mode: the only context needed is the [authentication](getting-started_glossary-a-e.html#authentication) token. Once the requested page is sent to the user, the version 7 server can manage another task without transition.

## DOM

The Document Object Model (DOM) is a W3C recommendation describing an API independent from any programming language and platform that allows programs or scripts to access or to update the content, the structure, or the style of XML documents. The document can then be processed and the result of the processing can be incorporated in the document that will be presented in the browser.

Every browser version has its own DOM, but successive standardization has been done to make them quite similar. The differences that remain are managed by libraries such as JQuery.

It is important to note that the DOM includes not only a description of the current page and the status of the browser, but also events linked to user interactions (hover, mouse click, and keyboard entry) and events linked to pages or windows.

## Draft

When a modification is in progress in the version 7 interface, a dedicated resource named **draft** is created on the client and on the node.js server. It stores the complete set of data that is entered during a creation or a modification in the user interface. The entry of a draft can be interrupted because the browser stops unexpectedly (for example: power off, system crash, and closing of the browser windows).

When a user starts a session, a function displays the pending drafts and can resume the entry by selecting the corresponding draft. The platform will request the server to restore the context of the interrupted session (a restoration of the working copy will be done), and the process can then resume at the point it had been interrupted.

A draft is usually deleted when the entry is finished and the data has been successfully updated in the database (if the representation is persistent and corresponds to the data managed in CRUD mode), or sent to the server for execution (in a batch execution request). It can also be stored to be used as a starting point of a new entry, or transmitted to another user who will complete the entry, then will transmit it again to another contributor, or will submit the draft to the server.

## Endpoint

The [SData](getting-started_glossary-r-z.html#sdata) protocol can be used to define endpoints specifying the connection path to access published application services. An SData endpoint is a URL made up of the following segments: a server, an application, a protocol, and a [dataset](getting-started_glossary-a-e.html#dataset).

The following is an example of an endpoint SData.

```
http://my_server:80/sdata/accounts_mgt50/gcrm_contract/demo_folder
------  server ------------------/-application------/---protocol---/---dataSet----

```

For version 7, the segments have the following values:

* The syntax for the server is the access [URL](getting-started_glossary-r-z.html#url) to the version 7 platform, followed by the basic protocol (sdata): for example, <http://my_server:80/sdata/>.
* The application can be Syracuse (to access the services supplied by the node.js server), or Sage X3 (to access the services supplied by a Sage X3 server). Also, any other application working with the version 7 protocol could be provided.
* The protocol definition for Syracuse is collaboration. For Sage X3, it can be ERP, HRM, or other protocol name that will be defined later (for example, an SData contract dedicated to a specific data exchange with another software).
* The [dataset](getting-started_glossary-a-e.html#dataset) corresponds to an identified data source. For Sage X3, it is a unique name referencing a solution and folder code combination, exactly like the unique name given in the client-server connection box.

## Entry mode

An entry mode is used to enter information on a page in the version 7 user interface. This information will be stored in the ERP database or used to trigger a process. Entry modes are stored as a draft on the browser and on the version 7 node.js server. This draft updates asynchronously a context on the Sage X3 server. This update mode is [stateful](getting-started_glossary-a-e.html#activity).

## Entry point

An entry point is an optional call to a section of specific code used to change the behavior of a standard âblack-boxâ type component of the software.

[Next entries](getting-started_glossary-f-p.html)

  

[Index](index.html)  [Home](getting-started_home.html)