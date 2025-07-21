[Index](index.html)  [Home](getting-started_home.html)

Classes

|  |  |  |  |
| --- | --- | --- | --- |
| [Classes and Instances](#classins) | [Persistent and Basic Classes](#persvol) | [Encapsulation](#encaps) | [Advanced Features](#advanced) |

**This document introduces the class management performed in the Sage X3 supervisor and engine layers for version 7.0. It describes the main principles and provides links to additional detailed documents describing how they are used in a Sage X3 platform.**

This is a major change from version 6, where the development partner used tables (called F class, which are a set of fields in a table), and masks (called M class, which are associated with the user interface). Version 7 still supports version 6 concepts in Classic mode, but version 7 development partners will use new concepts called classes that are usually linked to tables and representations that are linked to the UI definition.

# 1. Classes and Instances

A Sage X3 class is very similar to a class in an Object Oriented language. It describes a structure, which is shared by many objects called the instances of the class. It also describes behaviors that are shared by the instances. The following examples illustrate the concept.

* Customer, Sales Order, and Address are classes.
* Customer C47 and Customer C92 are two instances of the Customer class. Sales orders SO27301 and SO18853 are two instances of the Sales Order class.

The Customer class defines what is shared by all customers:

* All customers have a customer code, billing address, a list of shipping addresses, credit limit, and so forth. These elements (customer code and billing address) are called the properties of the class. Together, the properties define the structure of the instance.
* Customers may relocate, be invoiced, be marked as inactive, and so forth. These are behaviors or events that can apply to all customers. These behaviors are coded as script procedures and functions at the class level. These procedures apply to all instances of the class. They are called methods and operations, which will be discussed later.

An instance of a class represents a specific object, for example customer C47 or C92. The instance contains the values of the properties defined by its class. For example, customer C47 may have the following values:

* **Customer code:** C47
* **Billing address:** 444 High St, Palo Alto, Ca 94301
* **Delivery addresses:** 156 University Ave, Palo Alto, Ca 94301, 300 Hamilton Ave.
* **Credit limit:** $80,000.00

Customer C92 will have a different set of values for these properties.

# 2. Persistent and Basic Classes

Most classes will be persistent, which means that their instance data is stored and retrieved from the ERP database. If the class is simple, it can be mapped to a single table in the database. For example, an Address class can be mapped to a single ADDRESS table. Most classes are mapped to a set of tables with joins to express their relationships. For example, a Sales Order class can be mapped to a combination of SO Header, SO Line, and Address tables.

Classes can also be basic. In this case, the instance data is kept only in memory and disappears when the server process terminates. Basic classes are helpful when managing temporary data used by a computation.

# 3. Encapsulation

The class logic (its methods and operations) should ensure that the instance data is always kept in a consistent state. For example, a Sales Order class should guarantee that the totals are always consistent with the line details after the order has been modified.

Classes are also used to organize the code and hide the details of the complex logic that may be needed to manage the objects. For example, the rules that update sales order totals when order lines are modified may be rather complex. These rules should be packaged inside the Sales Order class rather than spread accross various modules of the ERP system.

An entity is a set of records from different tables that have to be controlled and updated to keep the data consistent. A customer, General Ledger entry, product, and sales order are examples of an entity.

To use a class, you have to instantiate it, that is, allocate a block of memory for the values of the properties defined by the class.

**Class properties may be:**

* Simple properties with basic data types such as integer, character strings, decimal numbers, dates, and so forth
* Child entities (a property that is an entity by itself).
* References to other entities (a key value that links on another entity).
* Collections (called âarraysâ in version 6) of properties or child entities.

A class can be used for easing complex data structure handling in a process, or it can be associated to a set of databases tables that stores the content of entities instances. In this case, the class is typed âpersistentâ. Other types of classes exist and are described later.

A class includes methods and operations. Some of them are predefined, while others can be added by the development partner. Both are procedures associated with a class that can be called from another program to operate on class instances. A method operates on a context or class instance, and thus is used only on an existing instance, while an operation can be used even when a context does not exist. The arguments passed to an operation must at least include the identification of the data set on which it operates.

Every property of a class has its standard methods and no other methods can be added. They allow a development partner to hide the technical implementation of the property and supply interface for its use. These methods are the following:

* **GET** is a method called when the value of a property in a class instance is read.
* **CONTROL** is a method called when the value of a property in a class is updated. This method can only verify that the value proposed is correct, change the value to be assigned, or refuse the assignment. It cannot assign other properties unless is done using the PROPAGATE method. At control time, you can have access to the origin value through the snapshot mechanism. This method is also directly called when you perform an update or an insert.
* **PROPAGATE** is a method called after the **CONTROL** method when a modification has been done (the modification was accepted and the field modified).

These three methods are called automatically by the Sage X3 engine when accessing or updating the properties. There is another method that is called by the supervisor in some dedicated cases:

* **INIT** is a method, through the class method AINIT, called after the creation of an instance by the CRUD management generated code when a creation operation is started (not if the instance is fed by a read operation). It is also called on child class instances when a line is inserted.

Some automatic methods also exist on dedicated data types for managing translatable texts, but the scope in this document is only to describe the methods used on every class or property.

# 4. Advanced Features

## Declaration

On the Sage X3 platform, using classes first needs to be declared in dedicated dictionaries. For more information, see [Developer Guide Classes Dictionaries](developer-guide_classes-dictionaries.html).

## Language support

After declaring the classes, the Sage X3 script code can be written with classes, and benefit from the new instructions and functions described in [Developer Guide Classes Script](developer-guide_classes-script.html).

## Standard methods

On persistent classes, standard methods have been implemented to ease the management of complex documents in the database. They are described in [Developer Guide Classes Standard Methods](developer-guide_classes-standard-methods.html).

## Event management

Events provide the development partner the ability to add Sage X3 script code to manage standard events and to change their behavior. For more information, see [Developer Guide Classes Events](developer-guide_classes-events.html).

  

[Index](index.html)  [Home](getting-started_home.html)