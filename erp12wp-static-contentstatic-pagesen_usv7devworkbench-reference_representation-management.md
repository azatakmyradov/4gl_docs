[Index](index.html)  [Home](getting-started_home.html)

Representations

|  |  |  |
| --- | --- | --- |
| [Classic Function](workbench-reference_launching-url.html#classic) | Function code | *GESASW* |

A representation is the description of a data structure dedicated to the user interface. A representation is always associated with a class. In this capacity, it can have its elements such as properties, associated scripts, operations, and methods. These specific elements, added to those already owned by the associated class, support the user interface behavior related rules. An overview of the representation concept is described in the [Developer Guide Representations](developer-guide_representations.html) document.

This workbench functionality enables users to create representations and update them. It feeds dictionary tables and generates code by validating representations. A representation already described in the dictionary is not qualified as usable by the software unless it is validated.

To create or update a representation, it is necessary to enter information in several sections:

|  |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Header](#header) | [General](#general) | [Properties](#properties) | [Methods](#methods) | [Organization](#organization) | [Displayed properties](#exposed) | [Links](#links) | [Menus](#menus) |

Additional information:

|  |  |  |
| --- | --- | --- |
| [Global links available on the class management page](#glolinks) | [Errors list](#error) | [Additional comments](#comments) |

# Header information

Contains information to identify the class:

## Representation code

A unique identification of the representation. It is used to generate automatic script names by the supervisor layer when a [validation](#valid) is performed.

## Description

The description of the representation.

# General section

Describes the main information about the representation. The following blocks are available in this section:

## General

### Class code

Defines the class associated with the representation. The class code is mandatory.

### Instance

Defines the name of the property that identifies the class instance in the representation.

### Used for search results

When this check box is selected, the representation is selected by default to display the data detail by using the link on the search result page. For a given class and a given type, only one representation can be selected.

## Functions

### Authorization

This information is optional. It allows the supervisor to check if the access is authorized to a user. The user profile defines for every user the functions that are allowed and can filter by company and sites.

**Warning**: Make sure that if the function is not filled, the representation is available without restrictions to all users with access to the endpoint. If you want to allow the administration users to filter data for users, a function code must be given. This means that you might have to create a fictitious version 6 function code if the authorization doesn't derive from the access on a given version 6 function, and even a fictitious object if you want to control the access by companies or sites.

### Convergence

This information is not mandatory. It defines the Sage X3 version 6 function invoked in Classic mode when the user modifies a record in **$detail** mode while a **$edit** facet has not been specified for the representation.

## Characteristics

### Activity code

Used to protect specific representations during the standard patching process (if starting by X, Y, or Z), or to make them optional. It behaves as all activity codes defined in dictionaries.

### Module

It indicates the technical module the representation is associated with.

## Type

### Type

Defines the type of device the representation has been created for. The available values are **Desktop** and **Mobile phone**.

### System

Reserved for supervisor use and must not be selected for a normal representation.

## Facets

This grid defines the list of facets supported by this representation. The available facets are **Detail**, **Edit**, **Query**, **Lookup**, and **Summary**. The check boxes are only displayed according to the behaviors that have been selected.

## Managed behaviors

Defines generic behaviors that are managed for the representation. The following table shows a list of built-in links with a dedicated logic:

| Action description | | | Presence on facets | | | Prototype characteristics | | | Comments |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Action | Link label | Target facet | Query | Detail | Edit | Link | Media Type | Target |
| Display detail | Display | $details | ✔ |  |  | $details | JSON | self |  |
| List display | List | $query |  | ✔ |  | $query | JSON | self |  |
| Summary display | Summary | $summary |  | ✔ |  | $summary | JSON | popup |  |
| Create a record | Create | $edit | ✔ |  |  | $create | JSON | self |  |
| Quick edit | Modification of a quety line | $edit on a restricted list of fields | ✔ |  |  | $edit | JSON | self (in a section that opens) |  |
| Duplicate a record | Duplicate | $edit |  | ✔ |  | $duplicate | JSON | self |  |
| Update a record | Update | $edit |  | ✔ |  | $edit | JSON | self |  |
| Delete a record | Supprimer | $result |  | ✔ |  | $delete | JSON | self | $result=message |
| Display in Excel | Excel | $details |  | ✔ |  | $excel | Excel | Excel |  |
| List in Excel | Excel | $query | ✔ |  |  | $excel | Excel | Excel |  |
| List in PDF | PDF print | $query | ✔ |  |  | $pdf | PDF | blank |  |
| Display in PDF | PDF print | $details |  | ✔ |  | $pdf | PDF | blank |  |
| Mail merge in Word | Mailmerge | $query | ✔ | ✔ |  | $wordmailmerge | Word | Wordmailmerge |  |
| List in Word | Word | $query | ✔ |  |  | $word | Word | Word |  |
| Display in Word | Word | $details |  | ✔ |  | $word | Word | Word |  |
| Back | Back |  |  |  | ✔ | $back |  |  |  |

In addition, the built-in links in the **$edit** facet are the following:

| Action | Link label | Target facet | Target |
| --- | --- | --- | --- |
| Selection | Selection | $lookup | popup |
| Creation | Creation | $edit | blank |
| Navigation (tunnel) |  | $detail | blank |

## Collections

Describes the collections defined at the representation level. The collections that have been defined in the class should be declared if one of the following conditions is fulfilled:

* The characteristics of the collections are changed.
* A representation field has been added to the collection.

The following information must be entered in the grid:

### Code

This is a code that identifies the collection:

* If the collection is defined at representation level, it is a single name that cannot exceed a length of 12 characters.
* If the collection is defined at the class or child class level, the path of the class must be given. For example, if a document has a line level in which a collection has been defined, the syntax is **DOC.LINE.COLLECTION**, where **DOC** and **LINE** are the instances of the nested classes. Declaring the collections present at the class level is only useful if additional fields that are present only in the representation must be added.

### Alias

This is a single name that identifies the collection. For a representation collection, the alias is the same as the collection name, and can't be changed. It must be defined when a class path has been given and must be unique for the representation.

### Description

Description of the collection.

### Min no.

Indicates how the property array is first allocated in memory instances. It can be **0**, **1** or **Maximum**.

### Act

Activity code. If assigned, it must be a **sizing** activity code. This allows defining the maximum dimension of the collection according to the value of the activity code. As the memory allocation is now dynamic, it is no longer useful to optimize the memory spent to store documents during processing.

### Max no.

Is the maximum dimension of the collection. It can be entered only if no activity code is present on the collection or it can be kept empty. The collection size automatically grows without limit when new lines are created.

### Sequence number

Refers to a property of the representation that stores the number of lines created in the collection. It is used when the number of lines of a document is stored in the header (used in version 6).

### Insertion, Deletion, Sort, Addition

If these check boxes are selected then line insertion, deletion and sorting operations are possible on the collection. The check box values have the same value in representation if the collection has been defined in the class. You can clear the check box at the class level, but you can't select the check box if the operation is not supported at the class level.

The corresponding methods are **ADDLINE**, **ADELLINE**, and **ASORT**. **ADDLINE** is also used for the addition of lines.

## Scripts

List of scripts in which **$PROPERTIES** and **$METHODS** labels are available for development partners who are prepared to add their code associated with supervisor events (especially for CRUD management). See the [event description](developer-guide_classes.html) for more information about the available events.

The following columns are available in this table:

### Script

Name of the script. The standard naming convention is **repr\_Ryyyy** where:

* **repr** is the class code.
* **yyyy** is **STD** for the first standard script delivered. If others are needed, they should start with **STD**.
* **yyyy** should start with **VER** for vertical scripts delivered.
* **yyyy** should start with **SPE** for specific scripts delivered.

As a script can be shared by different classes, the naming convention is not mandatory.

### Type

Can be **Standard**, **Vertical** or **Specific**:

* **Standard**: Code is supplied by the software vendor.
* **Vertical**: Code is supplied by the software vendor or a partner, dedicated to the coverage of needs for a given activity sector.
* **Specific**: Code is supplied by a partner for a given customer or written by a customer's development team to cover specific needs.

### File

Select here the processes dictionary.

### Order

The order in which the **$METHODS** or **$PROPERTIES** labels are called in the event.

### Activity code

Used to protect the script during the standard patching process (if starting with X, Y, or Z), and to activate/deactivate the call of the script.

# Properties section

**Describes the properties defined at the representation level. Properties defined at the class level must not be listed.**

## Property table

This table defines the property list with the following information:

### Property

The name of the property as it will be used in the Sage X3 script.

### Order

This is an indicative order rank.

### Description

Describes the property in the UI.

### Short description

A short description of the property. It can be used for personalization when designing the UI.

### Type

A data type associated with the property. This refers to the [data type dictionary](workbench-reference_data-types-dictionary.html). This field is mandatory.

### Menu

Useful only if the **M** data type is used. It links to a numbered list that defines all available values for the property. For example, figure 1 corresponds to the **No/Yes** local menu.

### Length

Used when the data type does not determine the length. It can be either a number of characters for string values or a number of digits in **N.M** format, where **N** is the number of digits before the decimal position and **M** is the number of decimals.

### Act

Used to protect specific property in standard classes during the standard patching process (type if starting with X, Y, or Z), or to make them optional depending on the activity code value given when configuring the Sage X3 folder. It behaves as all activity codes defined in dictionaries.

### Collection

Is empty if the property is a single one. Otherwise, it refers to one of the collections defined in the first section of the class dictionary. It might then be either an array of child references (header/lines structure) or a denormalized array stored in several columns of a database.

### Lob table and Lob field

When the data type is a clob or blob managed by the supervisor, this information indicates the table and column where the rich media element is stored. Depending on the table used, the key section will be filled so that the join can be done by giving the value of the key. If the data type is not managed by the supervisor, a program will handle the join and therefore, no information can be entered in these two fields.

### Content type

When the data type is a clob or blob managed by the supervisor, this information displays the content type associated with the data type.

### Mandat

If **Mandat** is set to **Yes**, then the field can be valid only if a value is present.

### Control table

Refers to a control table that is used to perform additional consistency control defined through a simple setup.

### Dependency

It defines a property that is used when the control table depends on another table.

### Access code

Refers to an access code that controls access to the property for a given user based on a setup. See [Access code](getting-started_glossary-a-e.html#access-code) for more information.

### GET accessor

If the check box is activated, a GET accessor calling code will be generated on the property. Otherwise, no code will be generated.

This value can be changed at any time in the dictionary, even in specific developments on standard classes. Once activated, it will not be deactivated by any patch at any time.

It is recommended to activate this check box only on properties where it is necessary since calling GET accessors on every property reduces performances when running.

## Parameters table

This section describes the current line on the property table. If the property type has rules requiring additional parameters, the parameter list appears in this grid. Therefore, entering a value is required to call the rule with the right parameters according to the context.

### Code

Is the code of each parameter. It is presented in display-only mode.

### Description

Is the description of each parameter. It is presented in display-only mode.

### Method

It defines how the parameter is transmitted in the call. It is presented in display-only mode. It can be:

* **By Address**: A reference is sent to the call. Any modification done in the call on the variable directly changes the value of the parameter.
* **By Value**: Parameter is copied and the value sent can be modified during the call with no impact on calling the parameter value.
* **Constant**: A reference is sent to the call, but the parameter is in read-only mode. Any attempt to modify it during call execution generates an error.

### Type

Is the data type of each segment key. It can be any of the following: **Char**, **Integer**, **Decimal**, **Date**, **Enum**, **Clbfile**, **Blbfile**, **Instance**. **Uuident**, or **Datetime**. It is presented in display-only mode.

### Value

Is the formula behind the value assigned for the parameter. Only a subset of the Sage X3 scripting language is used for the formula. The rules are given in the [Developer Guide Restricted Formula for Key and Parameter Values](developer-guide_restricted-formula-for-key-and-parameter-values.html) document.

## Keys table

This section describes the current line on the property table. If the property type is linked to a table (version 6 technology) or a persistent class (version 7), the key components appear:

### Code

Is the column name of each segment key. It is presented in display-only mode.

### Description

Is the description of each segment key. It is presented in display-only mode.

### Type

Is the data type of each segment key. It can be any of the following: **Char**, **Integer**, **Decimal**, **Date**, **Enum**, **Uuident**, or **Datetime**. It is presented in display-only mode.

### Value

Is the formula behind the value assigned to a key segment. If the key is made of several segments, every segment description is usually a property of the class (and frequently the current property). But when a multiple segment key is defined, some elements can be additional properties or constants. Only a subset of the Sage X3 scripting language is used for the formula. The rules are given in the [Developer Guide Restricted Formula for Key and Parameter Values](developer-guide_restricted-formula-for-key-and-parameter-values.html) document.

# Methods section

**Defines the methods for the representation. As the representation is linked to an UI process, only stateful methods are available. Thus, being stateless, operations can only be defined for classes.**

The following information is available in this section:

## Methods table

Gives the list of methods with the following information on every line:

### Code

Identifies the method name that can be called for the representation. Upon running, the **ACTION** variable has this code as a value when the corresponding event is executed within the **$METHOD** label of the representation associated source files.

### Description

Describes the method.

### Return

Is the data type of the value returned by the method when called by **Fmet**. This is the type of the **ARET\_VALUE** variable available in the event associated with the method. It can be any of the following: **Integer**, **Date**, **Char**, **Decimal**, **Clbfile**, or **Blbfile**.

### Activity code

Allows disabling a method by assigning an activity code. At implementation time, if the activity code is not active, the method is not available.

## Parameters table

Gives the list of parameters associated with the current method in the previous grid, with the following information on every line:

### Code

Is the name of the variable containing the parameter value, as it can be seen in the code called by the **$METHODS** event.

### Type

Is the data type of the parameter sent to the method. It refers to the keyword used for the variable declaration. It can be any of the following: **Char**, **Integer**, **Decimal**, **Date**, **Enum**, **Clbfile**, **Blbfile**, **Instance**, **Uuident**, or **Datetime**.

### Description

Is the description of the variable.

### Method

Defines how the parameter is transmitted in the call. It can be:

* **By Address**: A reference is sent to the call, wherein any modification done on the variable directly changes the value of the parameter.
* **By Value**: The parameter is copied and the sent value can be modified during the call with no impact on the calling parameter value.
* **Constant**: A reference is sent to the call, but the parameter is in read-only mode. Any attempt to modify it during call execution generates an error.

### Dim.

Defines if the sent parameter is an array and indicates its first index value. It can be:

* **No**: No array.
* **From 1**: Array with an index starting at 1.
* **From 0**: Array with an index starting at 0.

### Class

Available only if the type is `Instance`. It defines the class of which the parameter is an instance of.

# Organization

**This section specifies the default hierarchical organization that is set up for the representation, as well as additional information used for the query page. A representation defines:**

* A page divided into sections.
* Sections divided into blocks.
* Blocks containing properties that can be single or organized in the collection, usually represented by a table in the UI.

Sections, blocks, and fields are placed by default on a page with a predefined algorithm. The [personalization functions](../ui-definition/personalization.md) enable a user to change the layout without losing the hierarchical organization of the representation.
In this section, the following information can be found:
## Sections table
Refers to the list of sections for the page. The following information must be entered:
### Code
This code must be unique for a representation. It can have up to twelve upper case characters or digits.
### Description
This label is displayed on the page. It is mandatory.
### Display order
This number gives the default input order of the sections. The rank can be discontinuous and can have up to four digits.
### Stacked
Set to **Yes** if you want the entire screen to be arranged in stacked mode.
### Activity code
It is used to protect specific sections during the standard patching process (if starting with X, Y, or Z), or to make them optional. It behaves like all activity codes defined in dictionaries.
## Blocks table
Refers to the list of blocks for the page. The following information must be entered:
### Code
This code must be unique for a representation. It can have up to twelve upper case characters or digits.
### Description
This label is displayed on the page. It is mandatory.
### Section
Indicates the section in which the block is located.
### Display order
This number gives the default input order of the sections in the block. The rank may be discontinued and can have up to four digits.
### Stacked
Set to **Yes** if you want the block to be arranged in stacked mode.
### Column no.
Indicate if you want the block to be on column 1 or 2.
### Activity code
Used to protect specific blocks during the standard patching process (if starting with X, Y, or Z), or to make them optional. It behaves as all activity codes defined in dictionaries.
## Filters table
States the list of filters that can be used for the current representation. The filters present in this list are used in the query facet. A filter set as mandatory is always applied to the query.
Other filters are displayed as links on the right side of the page. Clicking such a link refreshes the query by applying the corresponding filter in addition to the mandatory one if it exists. No combination of filters is done when clicking several links: the new filter set replaces the previous one.
If there is at least one filter that is not mandatory in the grid, an additional link called **no filter** is also present to allow the user to query a list with no other filter than the default one. When entering the query, the filter that has the **default** check box selected applies by default, but it can be replaced by any other filter.
The following information is found in the filter table:
### Code
Identifies the filter, must be unique. A selection action is available on this field to select a filter defined at the class level.
### Class
This check box is display-only. When selected, it indicates that the filter has been set at the class level.
### Description
This translatable dictionary text corresponds to the label displayed for the filtering link present on the page.
### Activity code
If selected, it indicates that the link is optional. It is present only if the activity code value is set to Yes. If starting with X, Y, or Z, it indicates that the link is not standard.
### Mandatory
One filter at most can be defined as **mandatory**. This filter is always used and can be combined with one of the other filters listed in the grid.
### Default
One filter at most can be defined as **default**. This filter is applied by default when using the representation where it is present in the corresponding list of links. However, the user can select another filter by right-clicking on the related link.
### Option condition
Defines the condition applied when the filter is set. It is a logical expression that can include operators, class properties, and constants.
### Error message
This message is displayed when a filter has been set and an attempt to access a record that does not fulfill the filter conditions is made.
## Sort order
This section allows defining the default order used to display the query lines. If not filled, the default index for the main table associated with the class is used.
### Index
Allows entering a default index used for the query. This index can only be one of the indexes present on the main table associated with the class.
### Index descriptor
This information can only be entered if no default index has been defined. A sorting description can be defined here on fields that are present in the query facet with the usual syntax of keys, for instance:
**-FIELD1+FIELD2-FIELD3+FIELD4**
When such a syntax is used, the sorting order is by FIELD1 in descending mode, then by FIELD2 in ascending mode, then by FIELD3 in descending mode, finally by FIELD4 in ascending mode.
This corresponds to the **&OrderBy=FIELD1 Desc;FIELD2;FIELD3 Desc;FIELD4** additional variable in the URL.
# Displayed properties
**A representation displays on the device a list of properties that can be:

* Properties defined in the representation itself.
* Properties present in the main class or its child classes.**

The properties table lists all the available properties. It can be filled in with a right-click action. A window appears for the user to choose among different classes and child classes as well as the properties to be included. It is always possible to enter into a property in a line.

The information present in this table is as follows:

## Alias

This name must be unique in the representation. It is used to designate the property in the data feed exchanged with the client. It can be up to 30 characters long. The first character must be an upper case letter while the others should include upper case letters, digits, or underscore characters. No lower case letters are allowed in the alias.

## Property

This defines the path of the property, with the dot path syntax, which means:

* That a field present in the representation is input by its name. For example, RUNNING\_TOTAL.
* That a field present in the main class is defined as SORDER.CUSTOMER.
* That a field present in a child class is defined as SORDER.LINE.ITEMCODE.

The segments in the path are the child instances codes as they are defined in the representation or class description.

## Collection

If this field is filled, the property is part of the collection that can be:

* Any collection present on the representation.
* Any class or child class used on the representation or not.

The dot path syntax is used to define the collection path, for example:   
**SORDER.LINE.QTY** is the path for a collection in the **ORDERLINE** child class (LINE instance) of the **SALESORDER** class (SORDER instance) associated with the representation.

When a collection is present on a representation, the properties within it are displayed in the user interface as a table. The collection is presented as a list if there is only one member in it.

The properties present in a collection must be ordered sequentially and in the same block. This means that a property can integrate a block only if it belongs to the corresponding collection. An unrelated property, whether it is independent or present in another collection, can't be included among properties of a particular collection.

## Block

This defines the default block where the property is located in the user interface.

## Order

This is the input order for the property entry in the blocks. Ranks can be discontinued and have up to four digits.

## Description, Short description

This indicates the label that can be used in the user interface. The defined label, its presence, and position can be changed in the personalization mode.

## Column no.

Indicate in which column you want the property to be.

## Activity code

Use this activity code to make the property optional. It automatically disappears from the prototype if the activity code is innactive. It protects the property's characteristics if it is a specific activity code.

## Unit

If the property is a numeric value attached to a unit, such as a quantity and an amount for a currency, the property defining the unit used must be set. It has to be one of the properties of the representation. Only a property having a data type attached to a table that manages units can be selected.

## Filter P

If this check box is selected, the corresponding value constitutes a filter when invoking the query facet. For example, if the following case happens:

* **SORDER** is a representation for the sales order, associated with the **SORDER** class; the instance code being **SORD**.
* **COUNTRY** is a property of the class **SORDER**.
* The **SORD.COUNTRY** property, with the **COUNTRY\_ORDER** alias, has the **Filter P** check box selected.

To filter on US country sales orders, the user selects the following option in the URL that calls the **SORDER** representation in query mode:

`...?url=http://myserver:8124/x3/$$prod/DEMO/SORDER?representation=SORDER.$query&where=COUNTRY_ORDER eq 'US'`

Some characters should have been avoided.

It is not necessary to select this check box for all the properties of the query facet because the possibility to filter on the column values is implicit for them. The filter line allows entering values directly.

## Entry P

If this check box is selected, the corresponding value can be a filter whenever the edit or detail facet is called. This is important if one of the parameters is not present in the key.

## Query, Detail, Edit, Lookup, Summary

These columns represent the different facets in which the property can be used. When one of these columns is selected, the property is present in the corresponding facet. Otherwise, it is not.

Following every facet column, there is an **Initial status** that can be **Visible** or **Invisible**. It can be set differently for each facet. This status can be changed afterward by a development partner with a script using an **ASETATTRIBUTE** method.

For the **Edit** column:

* The **Enterable** column indicates if the field is in display-only mode or can be entered in edit mode. A filter can be set on properties present on the query facet where these properties are entered.
* Set the **Hiddable** column to **Yes** for the field to be hidden if the size of the screen is too small. For example, the field can be visible on a desktop display and hidden on a mobile phone.
* Set the **Break after** column to **Yes** to insert a return line after the field for the next field to be on the next line.

# Links

**This section defines links that are available in various places of the user interface to trigger operations or methods according to the context.**

## Filter

As the number of links in a representation can be high, the section presents a restricted list of the available links based on the following filters:

* The **Anchor type** that defines the type of element in the user interface that the link is attached to. It can be: **Property**, **Collection line**, **Page**, or **Record**.
* Two **Display of generated links** and **Only invalid links** check boxes to select only the corresponding links.
* The **Anchor** name.

Generated links are inherited from the data type. They should not be modified. They can be deactivated if they aren't necessary. They can be replaced by other links. This is useful for links that need to be different from the default ones. For example, in a selection or a zoom.

Some links may not work anymore when a patch changes the structure of a representation. For instance, by deleting some of its properties. To keep the representation working despite this effect, links are marked as invalid. To fix this situation, invalid links must be validated again.

### Description of the anchor type and its associated name

A link is attached to an element of the interface. It can be attached to:

* A property. The anchor name is the property alias. It is directly near the property value. This type of link is related to the property. It enables to:

  + Trigger an operation
  + Display more information on the property
  + Guide input of the right values
* A collection line. The anchor name is the collection name. An icon is present at the beginning of the line to give access to the links. Usually, this type of link triggers an operation that applies to the entire line.
* A collection. The anchor name is the collection name. The link is present at the header of the collection and applies to the entire collection.
* The page. No anchor name is given. This type of link appears on the right panel and applies to the page.
* A record. No anchor name is given. This type of link can appear on every line of a query facet, and also on the right panel of a detail or edit facet if a current record is present on the page.

## Parameters table

This grid is filled with the parameter list when a link requires additional parameters to operate. The corresponding values need to be defined. For example, when a method requires an additional parameter.

## Keys table

This grid is filled with the corresponding components when a link requires a key to operate. The value is filled with formulas. For example, for an operation operating on a class. Only a subset of the Sage X3 script language is used for the formula entered. The rules are provided in the [Developer Guide Restricted Formula for Key and Parameter Values](developer-guide_restricted-formula-for-key-and-parameter-values.html) document.

## Links table

This grid contains the details of the existing links filtered according to the type and given anchor. The following information is available:

### Anchor

Defines the anchor in which the link is placed. The anchor is empty for **Page** or **Record** links.

### Code

Identifies the link. For a given anchor, only one link with a given name must exist. Dedicated codes exist for the standard links, for example:

* ADETAILS, ALOOKUP, and AQUERY for links associated with fields.
* ADETAILS, AEDIT, and ADELETE for links associated with the record.
* ASAVE, AABORT, ACREATE, and AQUERY for links associated with a page.

### Generated

This check box can't be modified. It is set when the link is inherited from a data type. The characteristics of the link can't be changed but it can be deactivated or replaced by another link.

### Active link

Modifiable only for generated links. Set to **No** if you want to deactivate the link.

### Invalid

This check box can't be modified because it is set when the link can't be used due to the lack of some parameters on the corresponding facet. This may happen after installing a maintenance patch. A validation attempt generates a log detailing the issues. You can select the **Only invalid links** check box to display only the links concerned by this issue.

You need to address this issue to fix the link. Otherwise, it is not used.

### Description

Corresponds to the text describing the link. It is a translatable text.

### Type

It states what is executed when the link is triggered. The different types of links and their characteristics are as follows:

* **Representation**:
  This link invokes another representation. The representation code is then given and an action code is associated. This action code can be one of the following:
  + **Create record**
  + **Display details**
  + **Modify record**
  + **Delete record**
  + **Display list**
  + **Display as Excel**
  + **List in Excel**
  + **Selection**
  + **Display Summary**
  + **Display in Word**
  + **List in Word**
  + **Mass-mail record**
  + **Mass-mail list**

  The action selected can only be one compatible with the behaviors supported by the representation.

  If the behavior is working on a given record, the key has to figure on the key grid. For example, for **Display details** or **Display Summary**, while no key is expected when the **Create a new record** behavior is defined on the line. This type of link can't be called on an edit facet.
* **Method**:

  A method is triggered when clicking this link. As it is related to a given context, a method can only be called on an edit facet. The instance that the method operates on and the method name have to be selected. Only the instances available on the line can be considered.

  If the instance name is empty, the operating method is the representation method. Otherwise, the instance path must be provided.
* **Operation**:

  An operation is triggered by clicking this link. The instance and the operation name must be provided as well. For an operation, additional information is provided in the **Asynchronous** column. If set to **Yes**, a dedicated session executes asynchronously. Otherwise, the user executes the operation and waits for its completion. Dedicated methods are available to handle asynchronous operations. They are described in [this document](developer-guide_managing-asynchronous-operations.html).
* **X3 Convergence**:

  A version 6 function page is opened in Classic mode using this link. The version 6 function name must be provided.
* **Free**:

  A link defined by its URL is opened by clicking this link. The URL must be provided.
* **Crystal report**:

  Report execution is launched when clicking this link. This kind of link is only possible on a query facet if defined at **Record** level, or on a **Detail** facet defined at **Record** level or **Page** level.

  The report code must then be entered. It refers to a Crystal Report definition defined in the GESARP function. If a redirection has been established for the report through the GESARX function (print code), it is used. This allows associating by a single setup a report code either to a report, a query, an SQL query, an export template, or a business object report. If several codes are associated with the same report code, a popup window opens to select the report to be printed. But in all the cases, a report code must exist otherwise it isn't possible to input it.

  The associated action code can be **Print** or **Print Direct**. When **Print Direct** is selected, the report's parameters can't be modified. This type is also used to filter the list of reports available for a given report code.

  Once the report has been chosen, the parameter list of the record is displayed in the parameter grid, and it becomes possible to enter path values from the representation to fill the parameter values. They can be single values or expressed as a range.

  Note that this kind of execution uses classic mode functions.
  

### Representation

Enter this choice only for a representation link to define the code of the used representation.

### Action

This describes the action available for the type of link. The choice depends on the type of link:

* For **Representation** links, the choice can be: **Create Record**, **Display details**, **Modify Record**, **Delete Record**, **Display List**, **Display As Excel**, **List in Excel**, **Selection**, **Display Summary**, **Display in Word**, **Mass mail Record**, **Mass mail list**.
* For **Operation**, Method, **Classic page** and **Free** links, no choice is entered here.
* For **Crystal Report** links, you can choose **Print** or **Direct Print**.

### Target

This choice can be entered only for a **Representation** link. It can have the following values:

* **Default** is the default value: when clicking on the link, a new page replaces the previous one.
* **New page** opens the representation on a new page or a new browser tab, depending on the browser options.
* **Embedded** is a choice that is only available for a **Page** link that displays a representation with **Display list** action code present on the **Details** facet. When this type of link is used, the query page is displayed simultaneously with the **Detail** page, and filters can be given on the query by filling the parameters grid with constants and/or fields present in the detail facet. The following [documentation](../ui-definition/representation-pages.md#embedded) shows an example of the user interface behavior in this case.

### Instance path

This field describes the path on which methods or operations operate. If empty, it is the representation instance by itself.

### Class code

This field displays the class code associated with the previous instance path.

### Method/Operation

You have to enter the operation or method to be called when a link has this type. Only the method or operation available on the class associated with the instance path can be used.

### Asynchronous

This field defines if an operation is asynchronously executed or not. It can be entered only for **Operation** links.

### Function

Enter the code of the classic function associated with the link. You only need to do this for this type of link.

### URL

You have to enter the URL associated with the **Free** type links. This URL can either be:

* A complete URL. For example,**[http://www.google.com](https://www.google.com)**
* A relative URL for an administration function. This starts with the **/sdata** segment. For instance, **/sdata/syracuse/collaboration/syracuse/users?representation=user.$query** to access the user's query on the administration page.
* A link to a visual process page, with an URL like **{$baseUrl}/PROCESS(%27XXX%27)?representation=PROCESS~XXX.$details**, where **XXX** is the process code. Typing **%27** escapes the single quote character.

An URL link can include variables that are known on the current page. The syntax is **{NAME}**, where **NAME** is the name of the alias defined in the **Displayed properties** section. For example, if:

* A representation has three lines of addresses followed by a postcode and a city name.
* The corresponding aliases are **LINE1**, **LINE2**, **LINE3**, **POSCOD**, **CITY**.

The link to display a map can be **<https://maps.google.com/maps?q={LINE1}+{LINE2}+{LINE3}+{POSCOD}+{CITY}&t=k>**

### Report

Enter the report code to be printed for **Crystal Report** links.

### Menu

For **Page** or **Record** links, you can create a hierarchy of menus in the [Menu](#menus) section. This field defines the menu the link is attached to. If it is empty, then the operation is attached to the first level.

### Order

This defines the sorting order for the links in the menu hierarchies.  
**Note**: Enter a value different than zero to see the link in a mobile representation.

### Attribute

This information describes how the link appears on the UI. Its exact interaction depends on the type of device (mobile, tablet, or workstation). An attribute can have the following values:

* **Simple link**:
  This is a hyperlink that appears in a list associated with the element. This list is usually shown when hovering the mouse over an active place, or clicking a dedicated icon.
* **Detail**:
  This is a hyperlink associated with the field value by itself. Usually clicking a field triggers the link.
* **Lookup**:
  This is a hyperlink associated with the selection action. It is usually used by clicking a magnifying glass located near the field.
* **Summary**:
  This is a hyperlink associated with the summarized view action. It is usually used by clicking a dedicated summary icon located near the field.

### Replacement

The purpose of this function is to replace the default link. The default link is manually created by an automatically generated one. Replacement is operational only on a generated link where a user indicates in the corresponding field the code of the manually created link (a.k.a. non-generated link) to be replaced. Both generated and non-generated links involved in a replacement operation should have the same type and anchor. A generated link can be deactivated if it isn't necessary.

### Activity code

This field allows to protect a specific link or to deactivate the link. It behaves like all the activity codes.

### Detail, Query, Edit, Lookup, Summary

These check boxes define the facets in which the link is available. The check boxes must be selected to make the link available.

# Menus

**This section defines menus that organize the global link section.**

Two tables are present in this section.

## Menu

The first table provides, on every line, a menu definition with the following information:

* A code that must be unique for the representation (without conflict with a link code).
* A title that will be displayed with the menu hierarchy. This text is translatable.
* A parent menu code that is empty if the menu is not a sub-menu of a previous menu.
* An order information code used to sort the line in ascending order of its value.
* An activity code to protect the item menu.

## Default configuration

This table allows you to define the default links that are presented for every facet in the first position with a dedicated style on the global link panel. The only information to enter is the link or menu code and activity code. The other information is displayed.

# Global links available in the **Representations** function.

**Only links other than the usual CRUD and automatic links (PDF rendering, Offices integration, and so forth) are described.**

## Validation

Performs a validation on the representation:

* Checks the global consistency of the representation description.
* Generates the code of the representation (properties, methods, and operations) in an **R\_repr.stc** script, where **repr** is the code of the representation.
* Generates the code of additional Sage X3 scripts where the UI logic associated with the CRUD operation support and the events calls are coded.

The generated program must not be modified. It is automatically recreated at each validation.

## Options > Global validation

Performs a global validation on the representation:

* A validation of the associated class and all of its child classes.
* A validation of the representation.

## Tree structure

This link also exists in the class dictionary. It displays a graphical view of the class or the representation. The displayed view looks like this picture (partial view based on a company class):

![](images_representation_hierarchy.jpg)

This view gives you the detailed list of collections, tables, children classes, scripts. The icons used are described in the following table:

| Icons | Use case and information displayed | | |
| --- | --- | --- | --- |
|  | Representation (node followed by the elements of the representation). | | |
|  | Class that has children elements (scripts, tables, collections or classes: this node followed by the embedded element list). | | |
|  | Table managed (node followed by a list of tables). | | |
|  | Collection of class instances or including several property collections (node followed by a list of classes or arrays). | | |
|  | Scripts list: this node followed by the corresponding scripts. | | |
|  | Elements that don't have additional children details: | Tables | **property:***description* **-** *table\_code* **[***abbreviation***] Class** *class\_name***[***cardinality***]** |
| Collections | **[***dimensions***]** *property\_name* *property\_description* |
| Scripts | *Rank **Type (Standard, Vertical, Specific)* *Script name*** |
|  | Class that has no children elements. | | |
|  | Recursive class (ie. reference to a class that has already been described in the hierarchy). | | |

At the bottom of the window, an array gives the list of the elements with the following information: level, class, parent class, collection, cardinality.

The total number of children class embedded in the class or the representation is displayed, as well as the maximum depth of the hierarchy.

### Notes:

1. When collections or arrays of references are given, they can be given in the following formats:
   * **[ 0 -** *N* **]** where *N* is a constant: in this case, the collection has a variable dimension with a maximum defined by a constant.
   * **[ 0 -** *ACT* **]** where *ACT* is an activity code: in this case, the collection has a variable dimension with a maximum defined by the value of an activity code.
   * **[ Maximum -** *N* **]** where *N* is a constant: in this case, the collection has a constant dimension given by a constant.
   * **[ Maximum -** *ACT* **]** where *ACT* is an activity code: in this case, the collection has a constant dimension size defined by the value of an activity code.
2. The cardinality of a relation is defined with one of these choices:
   * **[0 1]**
   * **[0 N]**
   * **[1 1]**
   * **[1 N]**

# Errors list

This section provides the error messages that can occur when using class management.

### Anchor *xxx* link *yyy* : Property or collection does not exist

A collection or a property that has been used in a link is no longer available in the representation.

### Anchor *xxx* link *yyy* : The *zzz* replacement link must not be generated

A generated link has a replacement link that is self-generated.

### Anchor *xxx* link *yyy* : The *zzz* replacement link must correspond to the same type and action that *ttt*

A replacement link must be consistent with the link it replaces (same anchor and anchor type).

### Anchor *xxx* link *yyy* : The *zzz* replacement link must be active

A replacement link must be in the active status.

### Anchor *xxx* link *yyy* : Link *zzz* not allowed on facet *fff*

This message can appear in several cases:

* On a lookup or summary facet, neither method links nor Classic links are allowed.
* On an edit facet, only the links on representations with a lookup or summary behavior, and the URL links are allowed.

### Anchor *xxx* link *yyy* : This method is / is not an operation

The wrong type has been used.

### Anchor *xxx* link *yyy* : The method does not exist

The code entered does not correspond to a method of the class.

# Additional comments

Note that modifications done on the representation might have an impact on other representations that have a link on a facet of this representation.

This explains why entering the dictionary on a representation can trigger an automatic update on the links. A message is displayed when this happens, and the user is invited to save the updated representation. The link on the representations is also automatically done when a patch is installed or the folder is revalidated.

  

[Index](index.html)  [Home](getting-started_home.html)