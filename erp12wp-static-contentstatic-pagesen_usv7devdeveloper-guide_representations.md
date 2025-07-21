[Index](index.html)  [Home](getting-started_home.html)

Representations

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| [Representations and facets](#facets) | [Associated classes](#class) | [Representation structure](#structure) | [Links](#links) | [Events on UI](#events) |

**This document describes how representations are handled by the Sage X3 supervisor and engine layers for version 7. It describes the main principles and provides access links to additional documents stating how they are used in the Sage X3 platform.**

Version 7 initiates new concepts for development partners who will henceforth deal with âclassesâ (usually linked to tables) and ârepresentationsâ (linked to the User Interface definition). This is a change from version 6 in which the development partner used to deal with tables (called F class, a set of fields in a table) and masks (called M class, usually associated with the user interface). Version 7 handles backward compatibility with version 6 through the Classic mode.

# 1. Representations and facets

A Sage X3 *representation* is very similar to a *class* in an object oriented language. It describes a *structure* that is shared by many objects called the *class instances*, and *behaviors* that are shared by the instances. Technically, there is no difference between a class instance and a representation instance.

A representation is always associated with a class as it describes a data structure used for user interface. When an instance of a representation is available, the class is seen as a child class of the representation.

Managing a class through a user interface implies the existence of many different use cases that share common elements. A representation has different facets, which prevent having too many representations to define. The representation describes the whole data structure used for a class user interface while a facet describes a use case of the representation as it defines a representation restricted view. Only some properties and few links may be available.

Available facets are:

* Lookup : This facet is used when a reference to an entity must be selected. For example, if a customer must be selected when entering a sales order, a selection pop-up window will be used which is described by the customer representation lookup facet.
* Query : This facet is used when starting an activity linked to a class. It presents a list of records in a grid in which sorting, selection, and paging operations can be performed. A zoom from a selected line will display the entity instance, and other links can be available on each line to perform operations on this line.
* Details : This facet is used to display the detail of an entity record.
* Edit : This facet is used when a creation or a modification of an entity record is performed.
* Summary : This facet is used when a summarized view of a record must be displayed. This replaces the File / Property function that exists in version 6.

Some other technical facets exist for dedicated purposes, but they don't appear in the dictionary.  
From the protocol point of view, the URL that accesses a class and a representation with a given facet has the following syntax:

```
...?url=/sdata/x3/$$prod/FOLDER/CLASSNAME?representation=REPNAME.$FACET
```

  
or

```
...?url=/sdata/x3/$$prod/FOLDER/CLASSNAME('KEY')?representation=REPNAME.$FACET
```

  
Where :

* FOLDER is the current folder.
* CLASSNAME is the name of the class.
* REPNAME is the name of the representation.
* FACET is the name of the facet.
* ('KEY') is the current key value used only for detail and summary facet.

Examples:

```
...?url=/sdata/x3/$$prod/DEMO/CUSTOMER('MARTIN')?representation=CUSTOMER.$details
...?url=/sdata/x3/$$prod/DEMO/CUSTOMER?representation=CUSTOMER.$query
...?url=/sdata/x3/$$prod/DEMO/CUSTOMER('MARTIN')?representation=CUSTOMER$summary
```

  
The syntax is more complex if the edit mode is used (there is a working copy that must be created), but the representation and the facet in the syntax can be found:
Example:

```
...?url=/sdata/x3/$$prod/DEMO/CUSTOMER('MARTIN')/$workingCopies?representation=CUSTOMER.$edit
```

# 2. Associated classes

A representation is always associated with a class. When an instance is created for a representation, the data present in the class is seen as a child instance (the name of the child instance is given in the representation dictionary). For example, if the CUSTOMER representation has an associated CUSTOMER class with an instance name equal to CUST, and if MYCUST is the instance of the CUSTOMER representation:

* `MYCUST.DISPLAYED_BALANCE` is a property used only for UI purposes, described as a property of the representation.
* `MYCUST.CUST.NAME` is a property of the CUSTOMER class.

# 3. Representation structure

A user interface describes a list of properties organized in hierarchical groups as follows:

* A representation describes a page.
* A page is divided into sections (at least one section).
* A section is divided into blocks (at least one block).
* A block contains properties.
* The properties can also be members of a collection. If several properties are members of the same collection, the properties will be organized as a grid. If there is only one member in a collection, a list of values will be presented.

The personalization tool enables a user to change this organization, but defining a default structure is important to propose default user logic. The personalization tool will also define sections as consecutive portions of the page, tabs, or columns.

# 4. Links

A representation description includes links which are seen in the user interface as hyperlinks intended to trigger an operation or a method.

## Link level

The links can be placed at different levels:

* At page level: They will appear in the right list of links on the page.
* At record level: They will appear on the right list of links (on detail and edit facet) only if a current record is online; they will appear on every line if present on query facet.
* At property level: They will appear as a link on the property.
* At collection line or collection level: They will appear as a global link on the line of a grid, or as a global link on the grid.

## Automatic or manual links

The links can be defined in different ways:

* Automatic links: these links are automatically inherited from the context and don't need to be entered. They can nevertheless be deactivated if necessary, or even replaced by another link. The different automatic links are:

  + the links that have been defined on the data type are automatically generated on the corresponding fields
  + the links associated to the CRUD operations that are available for the class associated to the representation are automatically generated as page or record links.
* Manual links: these links are set up manually and can correspond to:

  + operations defined on the class as record links.
  + methods defined on the class or the representation as record links.
  + links that opens a new representation, or a web page.
* A property link can be inherited from the data types associated with the property.

# 5. Events on UI

When a representation is used to perform operations or methods on a class, events are called at the level of the class and at the level of the representation.

Scripts are defined in the representation level and the events are called according to the same logic. The [Developer Guide Representation Events](developer-guide_representations-events.html) explains in detail how these events are called.

  

[Index](index.html)  [Home](getting-started_home.html)