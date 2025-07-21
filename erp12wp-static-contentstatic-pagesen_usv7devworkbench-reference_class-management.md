[Index](index.html)  [Home](getting-started_home.html)

Class management

|  |  |  |
| --- | --- | --- |
| [Classic Function](workbench-reference_launching-url.html#classic) | Function code | *GESACLA* |

**A class is the description of a data structure managing an entity (for example a customer, a general ledger entry, a product, a sales order, and so forth). An overview of the class concept is provided in the [Developer Guide Classes](developer-guide_classes.html), and a global description of the class dictionary is available in the [Developer Guide Classes Dictionaries](developer-guide_classes-dictionaries.html).**

**This workbench function allows users to create and update classes. It feeds dictionary tables and also generates code through a validation function. When the class described in the dictionary is not validated, it will no longer be used by the software.**

When creating or updating a class, it is necessary to fill several sections:

|  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- |
| [Header](#header) | [General](#general) | [Methods](#methods) | [Standard methods](#stdmethods) | [Properties](#properties) | [Mapping](#mapping) | [Miscellaneous](#miscellaneous) |

Additional information:

|  |  |  |
| --- | --- | --- |
| [Global links available in the class management page](#links) | [Errors list](#error) | [Additional comments](#comments) |

# Header information

Contains information to identify the class.

## Code

Uniquely identifies the class. It is also used to generate automatic scripts names by the supervisor layer when a [validation](#valid) is performed.

## Description

Description of the class.

# General section

Describes the main information related to the class. The following blocks of information are available in this section:

## Management mode

### Type

Defines the conditions of the class use and its behavior. The following choices are available:

* ***Persistent*:** A class associated with an entity stored in the database. Standard methods such as Create, Read, Updated, Delete, and others are available on the class and can be managed by the supervisor layer of Sage X3.
* ***Interface*:** A class supporting at least a partially CRUD operation, but with no link to the database tables. Development partners must write the code associated with the operations they want to support. Examples of such classes are those used to access the system or administration resources such as logs and running processes.
* ***Basic*:** A class associated with entities such as child entities of a persistent class. CRUD operations may also be available on such class, but usually they are not called autonomously.
* ***Technical*:** A class associated with an entity in which methods can be defined, but without any accessors. This type of class is usually reserved for the supervisor (platform).
* ***System*:** A class describing a data structure. No accessors are generated and no methods can be described. This type of class is usually reserved for the supervisor (platform).

### Main table

Entered only if the class is ***Persistent***. Defines the main (header) database table in which the CRUD operates. Other tables will be defined in the [mapping](#mapping) section.

### Index

Defines the main index used to access data. It must be a unique identifier of the record and is usually the first index of the table. Can only be entered if the class is ***Persistent***.

### Keys

* If the class is ***Persistent***, it displays the key components of the index selected. When several segments are present, the key syntax `SEGMENT1+SEGMENT2+SEGMENT3` is exactly as the key definition in the table dictionary.
* If the class is ***Interface***, the key components can be entered with the same syntax if several components exist. The properties used must be properties of the class.

## Additional information

### Activity code

Used to protect specific classes during the standard patching process (if starting with X, Y, or Z), or to make them optional. It behaves like all activity codes defined in the dictionaries.

### Module

Technical module the representation is associated with.

### In cache

If this check box is selected, the class describes a [cached class](developer-guide_cached-classes.html).

### Searchable

If this check box is selected, the data will feed the search engine indexes for the properties that are selected as ***Searchable***). Making a class ***Searchable*** is of course meaningful only if the class is persistent (otherwise, if even an indexation could be possible, how would we retrieve an information that has not been persisted?)

### Context

This field cannot be modified. If this check box is selected, the class is referenced by the context class, which implies that the context class must be validated if modified.

## Collection

Describes all the collections managed in the class. The collection code is assigned in the [Properties](#properties) section:

* To simple properties that describe an array of properties. For technical reasons, a child class will be created (called ***C\_CLASS\_COLLECTION***, the instance is called ***COLLECTION***).
* To a child class that describes a collection of child classes.

A collection has the following attributes:

### Code

Unique identifier for a class.

### Label

Description of the collection.

### Min no

Defines how the property array is first allocated in memory instances. Can be 0, 1, or Maximum.

### Act

This is the activity code. If assigned, it must be a ***sizing*** activity code. This allows defining the maximum dimension of the collection based on the value of the activity code. Because the memory allocation is now dynamic, it is not necessary to optimize the memory spent to store documents in memory during processing.

### Max no

This is the maximum dimension of the collection. An entry can be made if no activity code is present on the collection, or it can be left blank. The collection size will automatically grow without limit when new lines are created. A dimension is mandatory if members of the collection are not defined in a child class.

### Counter

This field refers to a property of the class that stores the number of lines created in the collection. It is used when the number of lines of a document is stored in the header. This is frequently used in version 6.

### Insertion

If this check box is selected, lines can be inserted on the collection. This will be used as the default value on the representations based on the class. The corresponding method is called **ADDLINE**.

### Deletion

If this check box is selected, lines can be deleted on the collection. This will be used as the default value on the representations based on the class. The corresponding method is called **ADDELLINE**.

### Sort

If this check box is selected, lines can be sorted on the collection. This will be used as the default value on the representations based on the class. The corresponding method is called **ASORT**.

### Addition

If this check box is selected, lines can be added at the end of the collection. This will be used as the default value on the representations based on the class. The corresponding method is called **AINSERT**.

## Scripts

A list of scripts in which "$METHODS" and "$PROPERTIES" labels are available for the development partners who will add their own code associated with supervisor events (especially for CRUD management). See the event description in the [Developer Guide Classes](developer-guide_classes.html) for more information about the available events.

The following columns are available in this array:

### Script

This is the name of the script. The standard naming conventions are `class_Cyyyy` where:

* **class** is the class code.
* **yyyy** is **STD** for the first standard script delivered. If others are needed, they should start with **STD** (standard script delivered).
* **yyyy** should start with **VER** for vertical scripts delivered.
* **yyyy** should start with **SPE** for specific scripts delivered.
  As a script can be shared by different classes, the naming conventions are not mandatory.

### Type

This field can be *Standard*, *Specific*, *Vertical*:

* ***Standard*:** is the code supplied by the software vendor.
* ***Vertical*:** is the code supplied by the software vendor or a partner, and is dedicated to the coverage of needs for a given activity sector.
* ***Specific*:** is the code supplied by a partner for a customer or written by a customer's development team to cover dedicated specific needs.

### Execution rank

This is the order in which the "$PROPERTIES" and "$METHODS" labels are called in the event.

### Activity code

Used to protect the script during the standard patching process if starting with X, Y, or Z and is also used to activate/deactivate the call of the script.

# Methods section

Defines the additional methods and the operations available on the class. The difference between an operation and a method is as follows:

* An operation can be run in any context and needs an index code and key value to build the context it operates on. An operation can be called through a link in the interface from any existing page when the key values are provided.
* A method works only if a context exists. It will only operate on the current entity instance.

The following blocks of information are available in this section:

## Method grid

Provides the list of methods or operations with the following information on every line:

### Code

Identifies the name of the method or operation that can be called on the entity. During execution time, the **ACTION** variable contains this code when the corresponding event is executed in "$METHODS" label (in the class associated source files).

### Label

This is the description of the method.

### Return type

This is the data type of the value returned by the method or operation. This is the type of the **ARET\_VALUE** variable available in the event associated with the method. It can be any of the following choices: `Integer`, `Date`, `Char`, `Decimal`, `Clob`, or `Blob`.

### Activity code

This is used to protect the method during the standard patching process if starting with X, Y, or Z and is also used to activate/deactivate the method in the class.

### Operation

This check box must be selected if the line refers to an operation; otherwise, it is a method.

### Index

This must be entered only for operations. It identifies the access index to the class instance values by a 'read' operation that must be performed in the operation. It is the default index of the class. This defines the list of key segments requested when a link triggering this operation is set up in a representation.

## Key definition grid

This grid provides a list of key segment parameters associated with the current operation in the previous grid. This grid is 'display only' and presents the following information:

### Code

This is the name of the key segment.

### Type

This is the data type of the key segment. It refers to a list of keywords used for the variable declaration. Not all data types are available because they must be recognized in the database segment keys. It can be any of the following choices : `Char`, `Integer`, `Decimal`, `Date`, `Enum`, `Uuident`, `Datetime`.

### Label

This is the description of the key segment.

## Parameter definition grid

Provides a list of parameters associated with the current method or operation in the previous grid with the following information on every line:

### Code

This is the name of the variable containing the parameter value, as it can be seen in the code called by the "$METHODS" event.

### Type

This is the data type of the parameter sent to the method. It refers to the keyword used for the variable declaration. It can be any of the following choices : `Char`, `Integer`, `Decimal`, `Date`, `Enum`, `Clbfile`, `Blbfile`, `Instance`. `Uuident`, `Datetime`.

### Label

This is the description of the variable.

### Mode

Defines how the parameter is transmitted in the call. It can be:

* `By Address`: A reference is sent to the call and any modification made in the call on the variable will directly change the value of the parameter.
* `By Value`: A parameter is copied and the value sent can be modified during the call with no impact calling the parameter value.
* `Constant`: A reference is sent to the call, but the parameter is read only. Any attempt to modify it during call execution will generate an error.

### Dim

Defines if the parameter sent is an array and what is its first index value. It can be:

* `No`: No array.
* `From 1`: Array with index starting at 1.
* `From 0`: Array with index starting at 0.

### Class

If the type is `Instance`, it defines the class the parameter is an instance of.

# Standard methods section

Describes the availability of the standard CRUD method and other methods supported by the supervisor layer on the class. The following fields are present in the grid:

## Code

This is for internal use only.

## Label

This describes the standard method.

## Activity code

This allows disabling a method by assigning an activity code. At implementation time, if the activity code is not active, the method will not be available regardless of the next check box value.

## Y/N

If the box is not checked, the method won't be available and thus the code won't be generated in the class.

# Properties section

Describes the properties of the class.

## Property grid

This grid defines the property list with the following information:

### Property

This is the name of the property as it will be used in the Sage X3 script. If the class is a persistent class, it is strongly recommended to give to the properties the same name as the columns of the database tables used for the data storage. If this is not done, the CRUD operation support will need additional code to assign class properties with data coming from database cursor.

### Order

This is an indicative order rank.

### Label

This describes the property and can be used when designing UI through representations.

### Short label

This is a short description of the property and can be used when designing UI through representations.

### Type

This is the data type associated with the property. This refers to the [data type dictionary](workbench-reference_data-types-dictionary.html). If the data type is empty, the property must be referenced on a child class instance.

### Menu

This is useful only if the data type `M` is used. It links to an enumeration that defines all the available values of the property. For example, 1 is the local menu No / Yes.

### Class

This is the class name associated with the property if this property is a class instance. It can be entered only if the data type is not entered (it is then mandatory).

### Collection

This is empty if the property is a single property; otherwise, it refers to one of the collections defined in the first section of the class dictionary. It might then be either an array of children references (header / lines structure) or a denormalized array stored in several columns of a database.

### Length

This is used when the data type does not define the length. It can be either a number of characters (for string values), or a number of digits in N.M format, where 'N' is the number of digits before the decimal position and 'M' the number of decimals.

### Lob table and lob column

When the data type is a CLOB or BLOB, this field is managed by the supervisor. This information describes in which table and column the rich media element is stored. Based on the table used, the key section will be filled so the join can be performed by giving the value of the key. If the data type is not managed by the supervisor, a program will manage the join and no information can be entered in these two fields.

### Content type

Displays the content type associated to the data type.

### Act

Used to protect specific property in standard classes during the standard patching process (when starting with X, Y, or Z), or to make them optional based on the activity code value given when configuring the Sage X3 folder. It functions as all the activity codes defined in dictionaries.

### Mandat

If 'Yes' is selected, a class instance can be valid only if this property is not empty.

### Control table

Refers to a control table that can be used to perform additional consistency control defined through a simple setup.

### Dependence

Defines a property used if the control table is dependent on another table.

### Access code

Refers to an access code that can control the access to the property for a user based on a setup. See [Access code](getting-started_glossary-a-e.html#access-code) for more information.

### Searchable

Defines whether the field is used to feed the search index. The field will be indexed only if the ***Searchable*** flag in the first section is set. But deactivating the flag in the first section will not deactivate this information on every line (this allows to deactivate temporarily an indexation without loosing the detail of the fields that will be indexed).

### Category

Defines a category tag for searching purposes. This category is defined in the miscellaneous table #16. It allows filtering the results of the search. For example, if you define a category "SALESREP", you can assign it to the Sales rep field in a customer record. A Sales rep field is also available on the sales order and sales invoices. When you search for "MARTIN", if "MARTIN" is a sales rep present on 20 customer records, 45 sales orders, and 34 sales invoices, selecting only the sales rep category will restrict the search results to these elements, while "MARTIN" might also be present on thousands of other entities.

### Get accessor

If this check box is activated, a 'get accessor' calling code is generated on the property. If it is not activated, no code is generated.

This value can be changed at any time in the dictionary, even in specific standard classes. After it is activated, it will not be deactivated by any patch.

Activate this check box only on the properties where it is necessary. Calling 'get accessors' on every property will create a negative impact on performances during execution time.

## Keys grid

This section corresponds to the current line on the property grid. If the type of the property is linked to a table (version 6 technology) or to a persistent class (version 7), the key component appears in this grid.

### Code

This is the column name of each segment key and is display only.

### Description

This is the description of each segment key and is display only.

### Type

This is the data type of each segment key and is display only. It can be any of the following choices : `Char`, `Integer`, `Decimal`, `Date`, `Enum`, `Uuident`, `Datetime`.

### Value

This is the formula that provides the value for the key segment. If the key is made of several segments, every segment description is usually a property of the class and frequently the current property. When a multiple segment key is defined, some elements can be either properties or constants. Only a subset of the Sage X3 scripting language is used for the formula entered in this field. The rules are given in the [Developer Guide Restricted Formula for Key and Parameter Values](developer-guide_restricted-formula-for-key-and-parameter-values.html).

## Parameter definitions grid

This section corresponds to the current line on the property grid. If the type of property has rules requiring additional parameters, the parameter list will appear in this grid. Entering a value will then be required to call the rule with the correct parameters based on the context.

### Code

This is the code of each parameter and is display only.

### Description

This is the description of each parameter and is display only.

### Type

This is the data type of each segment key and is display only. It can be any of the following choices : `Char`, `Integer`, `Decimal`, `Date`, `Enum`, `Clbfile`, `Blbfile`, `Instance`. `Uuident`, `Datetime`.

### Mode

This field is 'display only' and defines how the parameter is transmitted in the call. It can be:

* `By Address`: a reference is sent to the call, and any modification made in the call on the variable will directly change the value of the parameter.
* `By Value`: a parameter is copied and the value sent can be modified during the call with no impact calling parameter value.
* `Constant`: a reference is sent to the call, but the parameter is read only. Any attempt to modify it during call execution will generate an error.

### Value

This is the formula that provides the value for a parameter. Some limitations exist on the type of formula that can be used because the value must be evaluated in the context of the client. The rules are provided in the [Developer Guide Restricted Formula for Key and Parameter Values](developer-guide_restricted-formula-for-key-and-parameter-values.html).

# Mapping section

Defines how the CRUD operations, if they exist, are linked to the database tables for the main instance of the class, and the instances of child classes. It can be entered only if the class is ***Persistent***.

## Main table

This field displays the characteristics of the main table. The supervisor layer support expected is CRUD.

### Table

This is the main table as defined in the first section. This field is 'Display only'.

### Index

This is the index as defined in the first section, followed by its description. This field is 'Display only'.

### Reading

If this check box is selected, the generated program associated with the class will manage the 'read' operation. If cleared, the development partner must write the code for reading the data from the main table in the corresponding "AREAD" event.

### Creation

If this check box is selected, the generated program associated with the class will manage the creation operation. If cleared, the development partner must write the code for reading the data from the main table in the corresponding "AINSERT" event.

### Modification

If this check box is selected, the generated program associated with the class will manage the 'update' operation. If cleared, the development partner must write the code for reading the data from the main table in the corresponding "AUPDATE" event.

### Deletion

If this check box is selected, the generated program associated with the class will manage the 'delete' operation. If cleared, the development partner must write the code for reading the data for the main table in the corresponding "ADELETE" event.

### Filter

Allows to use a formula that will be used to filter the data. The formula can only include columns from the main table associated to the class.

## Table join grid

This grid displays the characteristics of the 'join' on other tables managed in the class as child classes and the supervisor layer support expected for CRUD on the sub-levels.

### Reference

This is the property of the class that is a reference to the child.

### Class

This field is 'display only', it provides the class code associated with the Reference property.

### Destination table

This is the table in which the class referenced will be persisted.

### Abbrev

The Sage X3 scripting engine requires an abbreviation for the [F] database buffer used for the exchanges with a database table. If not filled, it will be the default abbreviation of the table. It must be filled with another abbreviation if the table is already online (for example, when several links to the same table are present in the grid).

### Origin table

This is the table from where the join is performed and can be either the header table, or one of the tables present in the previous lines of the table join grid.

### Abbrev

This is the abbreviation for the origin table that will be filled if an abbreviation has been entered on the line referencing the origin table in the table join grid.

### Type

This is the type of join and can be one of the following choices: `0,1`, `0,n`, `1,1`, or `1,n`.

### Main index

Defines the index on which the 'join' is done. The ***Key-properties Mapping*** grid will be filled with the code of the different components of the key.

### Sorting index

If filled, it defines the initial order of the lines when a 'read' operation is done on a class instance. If not filled, the main index is used.

### Join expression

This is an list of expressions separated by a semicolon. Every expression represents the value of the corresponding key element when the join is performed.

### Selection expression

This is an optional condition that will filter the lines returned by the join. The syntax is the Sage X3 scripting syntax used in the ***Filter*** instruction.

### Activity code

Used to protect modified or specific lines in the grid or to disable some lines if the associated activity code is set to ***inactive***.

### Class management

If this check box is selected, the supervisor layer will implement the CRUD operation by calling the method implemented in the class defined on the line. If this check box is cleared, the CRUD operations support will be embedded in the code of the main class when the corresponding check boxes are selected.

### Deletion/Insert management

If this check box is selected, any update on the lines level will be performed by deleting and inserting all the lines rather than updating, deleting and inserting the modified lines. Selecting this check box affects the performances, but it might be necessary if the key of the line records changes every time lines are updated or inserted (for example, if the line number is reassigned).

### Reading

This field can be entered only if the ***Class management*** check box is cleared on the line. If the check box is selected, the generated program associated with the main class will manage the 'read' operation. If cleared, the development partner must write the code for reading the data from the main table in the corresponding "AREAD" event.

### Creation

This field can be entered only if the ***Class management*** check box is cleared on the line. If the check box is selected, the generated program associated with the main class will manage the creation operation on the corresponding child class. If cleared, the development partner must write the code for reading the data for the main table in the corresponding "AINSERT" event.

### Modification

This field can be entered only if the ***Class management*** check box is cleared on the line. If the check box is selected, the generated program associated with the main class will manage the 'update operation' on the corresponding child class. If cleared, the development partner must write the code for reading the data from the main table in the corresponding "AUPDATE" event.

### Deletion

This field can be entered only if the ***Class management*** check box is cleared on the line. If the check box is selected, the generated program associated with the main class will manage the 'delete operation' on the corresponding child class. If cleared, the development partner must write the code for reading the data from the main table in the corresponding "ADELETE" event.

## Key-properties assignment grid

Every line in the previous grid defines a child instance or a collection of child instances. In order to automate the assignments of the children properties that establish the links between the linked table and the master table, this grid displays, for every lines in the previous grid,the following information:

### Class

Displays the child class.

### Key property

Displays the property of the class that is associated to a key component.

### Data type

Displays the corresponding data type.

### Parent class

Displays the parent class, that is the class from which the link is established.

The two last columns of the grid allow to define values that have to be assigned automatically to these children properties during the CRUD operation. This will automatically generate the corresponding propagation rules, and an initialization rule ("ADDLINE" event), so the developer will not have to care about it. A value can be defined as:

### Parent property

In this case, a parent property value is used to assign the child value.

### Constant

In this case, a constant value is used.

Note that only one of these two fields can be filled. If none is filled, no automatic assignment will be done. This is usually the case with the last key element.

# Miscellaneous section

Defines additional information dedicated to access rights.

## Dedicated properties

These properties are used for data access filtering on data managed by the class.

### Legislation property

If the field contains a value, it identifies a property of the class where a legislation code can be entered. In the database, the corresponding column can be empty and the record is accessed by everyone, or it can contain a legislation code and the user must have the right to access the corresponding legislation. This enables the supervisor performing an automatic filtering on the data set accessible in a class instance for a user.

### Company property

If the field contains a value, it identifies a property of the class where a company code is entered. In the database, the corresponding column can be empty and contains the company the data is linked to. This allows the supervisor performing an automatic filtering on the data set accessible in a class instance for a user for CRUD operations depending on its rights (it might have a read access but not a write access on some companies).

### Site property

If the field contains a value, it identifies a property of the class where a site code is entered. This is used for filtering data in a more detailed level than [company](#compfilter) but with the same possibilities.

### Access code property

If the field contains a value, it identifies a property of the class where an access code is entered. This is used for filtering data in a different level from [company](#compfilter) but with the same possibilities. The major difference is that the access code can be empty in the database. If the access code is empty, the data set has no access restrictions.

## Filters

Defines additional filters that can be selected when the class is used to access only a sub-set of the data managed by the class. Several filters can be entered in a grid.

### Code

Identifies the filter.

### Description

Describes the filter.

### Condition

A filtering condition expressed with the Sage X3 script language (same syntax than the *Filter* instruction). Only columns present in the header table or in the tables directly linked with a (1,1) join to the main table can be used.

### Error message

An error message that will be sent to the user if a request is made on an instance that does not fulfill the filtering condition.

## History

Contains information to ensure compatibility with the version 6 code for data access restrictions.

### Linked object

Reference to a version 6 "object" defined in the object dictionary ("GESAOB" function).

This is used to handle the filtering of data by companies and sites in Version 7 native mode. The filters that apply are the ones associated with the "object". This is necessary for transition reasons when the filter per company and/or site for a user is still performed at "object" level.

# Global links available on the class management

Only the links other than the usual CRUD and automatic links (PDF rendering, Offices integration, and so forth) are described in this document.

## Validation

Performs a validation on the class:

* Checks the global consistency of the class description.
* Generates the code of the class (properties, methods, and operations ) in a "C\_class.stc" script, where **class** is the code of the class.
* Generates the code of additional Sage X3 scripts where the business logic associated with the CRUD operation supports as well as the event calls are coded.

**Note:** The generated program **must not be modified** as it will be automatically recreated during validation.

## Hierarchy

This link opens a window that displays the hierarchy of the class. It is also available on representations. The detail about this function can be found in the [representation documentation](workbench-reference_representation-management.html#hierarchy).

# Errors list

This section provides the error messages that might occur when using the class management.

| Message | Explanation |
| --- | --- |
| *XXX*: disabled representation. | This message is sent when the representation is not valid and cannot therefore be used, because other errors occurred when the representation was saved. |
| * *XXX*: Non-existent class. * *XXX*: Non-existent table. | These messages are sent when the corresponding entities referenced in the representation don't exist. |
| A technical or system class cannot be used in a representation. | The class referenced by the representation cannot be used. |
| *XXX*: Disabled class. | This message is sent when the class is not active (for instance because there is an activity code on it that has been set to *inactive*). |
| Representation of *Mobile / Tablet* type: X3 function not authorized. | X3 functions code used for triggering a Classic link can only be present on Desktop representations. |
| Activity code *XXX* associated with Group *YYY* is not of Sizing type. | Activity codes used to size collections must be Sizing activity codes. |
| The collection *XXX/MAXCOL*: Activity code *ZZZ* : Value 0 impossible for representation classes. | Sizing a collection in a representation with an activity code equal to 0 is forbidden. |
| * Filter *XXX* Field error "*Field description*" : Mandatory field. * Filter *XXX*: *Other message*. | On the filters, some controls are performed: the field is mandatory, the SData where syntax must be correct. |
| * Property *xxx(lll)*: Code already used for a property or collection. * Property *xxx(lll)*: Alias is mandatory. * Property *xxx(lll)*: Only the properties of the main class and linked classes 0,1 or 1,1 can be exposed in the lookup facet. | Miscellaneous controls failed when controlling the properties. |
| * Property *xxx(lll)* Parameter *PPP*: Value not defined. * Property *xxx(lll)* Key *KKK*: Value not defined. * Property *xxx(lll)* Parameter *PPP*: *other error messages*. | Errors encountered on the parameters or keys attached to a property. |
| * Property *xxx(lll)*: Data type does not exist. * Property *xxx(lll)*: The content type on the data type is necessary to use a Clob or Blob data type. * Property *xxx(lll)*: Both the table and the field of the lob are mandatory for a Rich media data type with supervisor management. * Property *xxx(lll)*: Specify the data type or collection . | Errors encountered on the data type attached to a property. |
| * Anchor *AAA* Link *LLL*: Non existent code. * Anchor *AAA* Link *LLL*: The replacement link *LLL* must be ungenerated. * Anchor *AAA* Link *LLL*: The replacement link *LLL* must be activated. * Anchor *AAA* Link *LLL*: The replacement link *LLL* must match the type and action of link *LLL*. * Anchor *AAA* Link *LLL*: Link to a representation of *TTT* type not authorized. * Anchor *AAA* Link *LLL*: Representation of *TTT* type: Link to an X3 function not authorized. * Anchor *AAA* Link *LLL*: Link *LLL* not authorized on facet *FFF*: Property *PPP* is a key. * Anchor *AAA* Link *LLL*: Link of  type not authorized. This link must be deactivated or deleted. * Anchor *AAA* Link *LLL*: Link *LLL* not authorized on facet *FFF*. | Miscellaneous errors encountered on links. |
| * Exposed property *EEE*: The property code is already used in alias *AAA*. * Exposed property *EEE*: Mandatory field. * Exposed property *EEE*: The unity property must be specified only in the numeric properties. * Exposed property *EEE*:Property *PPP* is not a unit. * Exposed property *EEE*:The unity property must exist in the same facets. * Exposed property *EEE*:Please specify a displayed property. * Exposed property *EEE*:This data type cannot be entered. * Exposed property *EEE*:Sizing collection not authorized in query mode. * Exposed property *EEE*:Only the properties of the main class and linked classes 0,1 or 1,1 can be exposed in the query facet. * Exposed property *EEE*:Only the properties of the main class and linked classes 0,1 or 1,1 can be exposed in the lookup facet. | Miscellaneous errors found on the exposed property tab. |

# Additional comments

Note that modifications done on the class might have an impact not only on the representations embedding the class, but also on the representations that have a link on a facet of theses representations.

This explains why entering in the dictionary on a representation can trigger an automatic update on the links. A message is displayed when this happens, and the user is invited to save the updated representation. The link on the representations is also automatically done when a patch is installed or the folder is revalidated.

  

[Index](index.html)  [Home](getting-started_home.html)