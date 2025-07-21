[Index](index.html)  [Home](getting-started_home.html)

Classes events

**The events are calls made automatically by the supervisor to handle various events and change the default standard behavior of the supervisor layers through additional lines of code.**

**This document describes how events are called and their context.**

|  |
| --- |
| Take care that in V11, the labels and variables used in the scripts associated to the class and representation events have been changed in order to clarify and simplify their management. The label `$METHODS` has been split in three labels :   * `$EVENTS` is now used for all the standard events. The associated variable is `[L]AEVENT` (the scope remains `[L]CURPTH`). * `$METHODS` is now used for the additional methods. The associated variable is `[L]AMETHOD`. The method can be implemented only in the scripts associated to the corresponding class (and therefore `[L]CURPTH` is no more usable). `[L]ARETVALUE` continues to return the result. * `$OPERATIONS` is now used for the additional operations. The associated variable is `[L]AOPERATION`. The method can be implemented only in the scripts associated to the corresponding class (and therefore `[L]CURPTH` is no more usable).`[L]ARETVALUE` continues to return the result. * `$PROPERTIES` is still used for the rules associated to the properties. The path of the property is still defined by `[L]CURPRO`, and the variable containing the rule is now `[L]ARULE`.   FOR COMPATIBILITY REASONS, THE PREVIOUS LABELS ($PROPERTIES and $ACTION) ARE STILL USABLE IN U10, BUT THEY WILL BE DEPRECATED IN V12.  IT IS THEREFORE RECOMMENDED TO MODIFY THE SCRIPTS QUICKLY. |

|  |  |  |
| --- | --- | --- |
| [Scripts Files and Event Implementation](#scripts) | [Scripts Files Name Normalization](#scriptsnorm) | [Events with Standard CRUD Code](#stdevents) |
| [Variables, Properties, and Methods in Events](#propevent) | [Event Execution on Nested Classes](#nestedevents) | [Event Execution when UI is Involved](#uievents) |
| [Sage X3 Script Managing Events Example](#eventexample) |

# 1. Scripts Files and Event Implementation

In the Scripts section of the class dictionary, the development partner can define a list of ordered scripts (standard, vertical, or specific). In every script, four labels called `$EVENTS`, `$METHODS` `$OPERATIONS` and `$PROPERTIES` must exist:

* In `$PROPERTIES`, we manage the events linked to properties methods (rules).
* In `$EVENTS`, we manage the global events associated to the class standard methods?
* In `$METHODS`, we manage the additional methods defined.
* In `$OPERATIONS`, we manage the additional operations defined.

**Note: the previous labels $ACTION and PROPERTIES that made the triage to rules, methods or operations is now obolete.**

When the control is given to one of these labels through a `Gosub` instruction, some variables are available to define the calling context:

* `ARULE` is a character string that provides the rule executed.
* `AMETHOD` and `AOPERATION` are character strings used respectively for defining the method and operation requested.
* `CURPTH` is a character string that provides the class path used for child class, which is explained later in this document (only for standard events).
* `CURPRO` is a character string variable that provides the property concerned (only for rules).

The `ARULE` value is used for properties and can be one of the following:  
\* `INIT`, `GET`, `CONTROL`, `PROPAGATE` for the rules.

The `AEVENT` value is used for standard events and can have the following values:  
\* `AINSERT`, `AREAD`, `AUPDATE`, `ADELETE` only for the persistent class if the standard corresponding CRUD operation is not generated.  
\* Other codes such as `AINSERT_CONTROL_BEFORE`, corresponding to events allowing a development partner to add code at a given step of the standard CRUD operations. These event have a name that start systematically with a A.

When a standard event is called for an instance of a child class, it is called as many times as the level is nested. For instance, it is called two times with a single level of nesting:

* In the first step, it is called for the child class.
* In the second step, it is called for the main class (`CURPTH` identifying the complete path to the child class element) thus allowing to complete the event.

When a rule is called for an instance of a child class, it is also called as many times as the level is nested; but in this case, `CURPTH` is not used : the path is given in `CURPRO` depending on the current level. For example, in the header script, `CURPRO` will be equal to "LINES.PROPERTY", while in the line script, `CURPRO` will be equal to "PROPERTY".

In the code associated to `$PROPERTIES`, `$EVENTS`, `$METHODS` and `$OPERATIONS` labels, the development partner has access to different properties. Some of them are defined at calling time by the supervisor, and others are defined as additional properties in the class that are not defined in the class dictionary.

Be aware that this code is called through a `Call` instruction FOLLOWED BY A `Gosub`. Thus, the scope of the local variables declared in an event code is limited to the event where it is called. For example, when a sub-program is called by the `$PROPERTIES` event, a local variable declared in that event is not visible for the next one:

```
$PROPERTIES
Case [L]ARULE
   When "INIT"
      ...
   When "CONTROL"
      Local Integer MY_VARIABLE
      ...
   When "PROPAGATE"
      # Even if PROPAGATE rule is called once the CONTROL is successful, MY_VARIABLE is not visible here
   When "GET"
      ...
Endcase
Return
```

  
The same rule applies for tables on line: at the end of any event, the tables are closed and have to be declared at the beginning of each event execution.

# 2. Scripts Files Name Normalization

A normalization exists for the Sage X3 script files names declared in a class:

* A default standard script called **CLASSNAME\_CSTD** is defined with rank 1000.
* The ranks in multiple of 1000 are reserved for standard extensions.
* Specific and vertical script file names should start with X, Y, or Z and can use other ranks.
* The ranks are not significant. Only the relative order is considered and can be easily changed if a
  conflict exists (for example, two scripts cannot have the same rank).

# 3. Events Associated with Standard CRUD Code

This section describes the different events available in standard CRUD operation performed on a persistent class.

These events are called on the methods previously defined through an `Fmet` instruction, followed by `Gosub` calls on every script associated to the classes and/or representations in the dictionary, in the order where they are defined. Depending on the type of event, a different label is called:

* the `$EVENTS` label is called for the standard events associated to standard methods
* the `$METHODS`and `$OPERATION` labels are called for methods and operations defined at class or representation level.
* the `$PROPERTIES` label is called for the rules defined on the properties of classes or representations.

Usually, a script containing the code of the event looks like this:

```
##########################################################################################################
# EVENTS
##########################################################################################################
$EVENTS
Case CURPTH
  When ""
   Case AEVENT
      When "event_name"
        Gosub METHOD_LABEL : # "event_name" is the standard event to be handled, and METHOD_LABEL the corresponding label

    Endcase
  Endcase
Return

##########################################################################################################
# RULES
##########################################################################################################
$PROPERTIES
Case [L]CURPRO
     When "property_path"
        Gosub PROP_LABEL : # "property_path" is the property path to be handled, and PROP_LABEL the corresponding label

Endcase
Return

# Example of rules handling (only the rules used are usually defined)
$PROP_LABEL
Case [L]ARULE
     When "INIT" : # Init method
     ...
     When "CONTROL" : # Control method
     ...
     When "PROPAGATE" : # Propagatin method
     ...
     When "GET" : # Get method
     ...
     When "AINIT" : # Init method
     ...
     When "AINIT" : # Init method
     ...

##########################################################################################################
# METHODS
##########################################################################################################
$METHODS
Case [L]AMETHOD
    When "method_name"
        Gosub METHOD_LABEL : # "method_name" is the method to be handled, and METHOD_LABEL the corresponding label
...
    Endcase
  Endcase
Return

##########################################################################################################
# OPERATIONS
##########################################################################################################
$OPERATIONS
Case AOPERATION
      When "operation_name"
        Gosub OPERATION_LABEL : # "operation_name" is the operation to be handled, and OPERATION_LABEL the corresponding label

    Endcase
  Endcase
Return
```

  
The following tables summarizes the events called during CRUD operation.

## Global events ($EVENTS)

| Type of events | Calling conditions | Details |
| --- | --- | --- |
| Global AINIT event | Global event that is called at the end of the AINIT method (all the INIT rules associated to the different properties have already been called). | This event is called by the supervisor:  * when a creation is performed through a representation using the *Create* link. * when a line is inserted in a grid by using the *Insert* link (on the child instance). * when a line is inserted in a collection by using the ADDLINE method.   If the developer creates a line in a script, the AINIT method must be called manually after the class instantiation. This calls performs all the init rules on the properties (ARULE has a value equal to [INIT](developer-guide_event-init.html)), and ends with the event AINIT (AEVENT as a value equal to AINIT). |
| Global ACONTROL event | Global event that is called after all the CONTROL rules associated to the different properties have been called. | This event is called by the supervisor before an insert or an update:  * After the [AINSERT\_CONTROL\_BEFORE](developer-guide_event-ainsert_control_before.html) and [AUPDATE\_CONTROL\_BEFORE](developer-guide_event-aupdate_control_before.html) events that depends on what has been modified. * Before the [AINSERT\_CONTROL\_AFTER](developer-guide_event-ainsert_control_after.html) and [AUPDATE\_CONTROL\_AFTER](developer-guide_event-aupdate_control_after.html) events. * When the class embeds collection of children instances, the control is first done on the children instances in AORDER order (CURPTH being the collection name) and then on the class (CURPTH being empty). |
| CRUD operation events | Called by the corresponding standard methods (AINSERT, AREAD, ADELETE, AUPDATE) on a class when the check boxes associated to the CRUD methods are not set in the class dictionary. The code of the event has to store or retrieve the data. If the boxes are set, the code that updates the database is generated at class validation and the event is not called. | | Value of aevent | Definition | | --- | --- | | [AINSERT](developer-guide_event-ainsert.html) | Creation method. | | [AREAD](developer-guide_event-aread.html) | Read method. | | [AUPDATE](developer-guide_event-aupdate.html) | Update method. | | [ADELETE](developer-guide_event-adelete.html) | Delete method. | |
| CRUD control events | Called when a CRUD operation is performed (AINSERT, ADELETE, AUPDATE). The CRUD methods can be called:  * automatically by the supervisor when standard CRUD links are triggered from the UI. * manually by the developer if such a CRUD operation is triggered from a script.  **No database transaction is in progress when these events are executed, and no data update has to be done in these events.** | | Value of AEVENT | Definition | | --- | --- | | [AINSERT\_CONTROL\_BEFORE](developer-guide_event-ainsert_control_before.html) | Before the insertion of a line in the database, and before the controls on the fields. Can be used to assign default values on properties. | | [AINSERT\_CONTROL\_AFTER](developer-guide_event-ainsert_control_after.html) | After all the controls have been performed and before the database insert operation. | | [ADELETE\_CONTROL\_BEFORE](developer-guide_event-adelete_control_before.html) | Before the deletion of a line and the automated consistency control of the referential integrity based on the dictionary definition. | | [ADELETE\_CONTROL\_AFTER](developer-guide_event-adelete_control_after.html) | After all the consistency controls have been performed and before the database line deletion. | | [AUPDATE\_CONTROL\_BEFORE](developer-guide_event-aupdate_control_before.html) | Before the controls of the properties and before the update of a line. Can be used to assign default values. | | [AUPDATE\_CONTROL\_AFTER](developer-guide_event-aupdate_control_after.html) | After the controls of the properties and before the update of a line. Can be used to perform additional consistency controls. | |
| CRUD update events | Called when a CRUD operation is performed (AINSERT, ADELETE, AUPDATE).  The CRUD methods can be called:  * automatically by the supervisor when standard CRUD links are triggered from the UI. * manually by the developer if such a CRUD operation is triggered from a script.   **A database transaction is in progress to update the data when these events are executed. Setting an error will abort the transaction and trigger the rollback events.** | | Value of AEVENT | Definition | | --- | --- | | [AINSERT\_BEFORE](developer-guide_event-ainsert_before.html) | After all the controls have been performed, but before the database insertion. | | [AINSERT\_AFTER](developer-guide_event-ainsert_after.html) | After the database insertion has been successfully performed. | | [ADELETE\_BEFORE](developer-guide_event-adelete_before.html) | Before the deletion of a line and after the automated consistency control of the referential integrity have been performed. | | [ADELETE\_AFTER](developer-guide_event-adelete_after.html) | After the successful deletion of a line. | | [AUPDATE\_BEFORE](developer-guide_event-aupdate_before.html) | Called before the updates and after all controls of the properties have been performed. | | [AUPDATE\_AFTER](developer-guide_event-aupdate_after.html) | Called after the successful database line update. | |
| CRUD error handling events | Called only when errors occur during the transaction execution. A rollback is performed, and then the control is given to the event to perform additional operations if necessary. | | Value of AEVENT | Definition | | --- | --- | | [AINSERT\_ROLLBACK](developer-guide_event-ainsert_rollback.html) | A database insertion failed. | | [ADELETE\_ROLLBACK](developer-guide_event-adelete_rollback.html) | A database deletion failed. | | [AUPDATE\_ROLLBACK](developer-guide_event-aupdate_rollback.html) | A database update failed. | |
| CRUD collection handling events | Called on the management of lines in collections (when the ADDLINE or ADELLINE standard methods are called). These methods can be called:  * automatically by the supervisor when the user updates a collection through links presents on a version 7 native page. * manually by the developer if the methods are called in a script to automate a collection. | | Value of AEVENT | Definition | | --- | --- | | [ADDLINE\_BEFORE](developer-guide_event-addline_before.html) | Before the line insertion in a (1,N) or (0,N) collection. | | [ADDLINE\_AFTER](developer-guide_event-addline_after.html) | After the line insertion in a (1,N) or (0,N) collection. | | [ADELLINE\_BEFORE](developer-guide_event-adelline_before.html) | Before the line deletion in a (1,N) or (0,N) collection. | | [ADELLINE\_AFTER](developer-guide_event-adelline_after.html) | After the line deletion in a (1,N) or (0,N) collection. | |
| CRUD read events | Called when the read method is called (in a script, or automatically from a version 7 native page). | | Value of AEVENT | Definition | | --- | --- | | [AREAD\_BEFORE](developer-guide_event-aread_before.html) | Before the database is read. | | [AREAD\_AFTER](developer-guide_event-aread_after.html) | After the database is read. | |
| Query events | Called during queries (no working copy is available; therefore, "This" is not available). The query is defined in the calling order. These events are useful when an interface class is used. In this case, no request is generated in the database to extract data.  **These events are called only for representations.** | | Value of AEVENT | Definition | | --- | --- | | [AQUERY\_DECODE\_CRITERIA\_AFTER](developer-guide_event-aquery_decode_criteria_after.html) | Used to define the columns present in the query. | | [AQUERY\_PRIMARYKEYS\_AFTER](developer-guide_event-aquery_primarykeys_after.html) | Used to define the link key to be read (database table, other pseudo-table, or link opened with [LNK]abbreviation). | | [AQUERY\_OPEN\_AFTER](developer-guide_event-aquery_open_after.html) | Called after the decoding of the query URL. Provides access to data and parameter of the query. | | [AQUERY\_CRITERIA\_AFTER](developer-guide_event-aquery_criteria_after.html) | Used to define the query criteria. | | [AQUERY\_JOIN\_AFTER](developer-guide_event-aquery_join_after.html) | Used to define the "Link" that is used to retrieve the data. | | [AQUERY\_TRANS\_AFTER](developer-guide_event-aquery_trans_after.html) | Executed on an instance ("This" is available). Values of the lines in the query grid can be assigned. | | [AQUERY\_CLOSE\_AFTER](developer-guide_event-aquery_close_after.html) | Used when the query is closed. | |
| Search events | Called when a query is performed by the search engine to feed the search indexes. | | Value of AEVENT | Definition | | --- | --- | | [ASEARCH\_OPEN\_AFTER](developer-guide_event-asearch_open_after.html) | Used at the beginning of the execution, just after the tables of the query have been opened. | | [ASEARCH\_JOIN\_AFTER](developer-guide_event-asearch_join_after.html) | Used just after a Link has been done to execute the query. | | [ASEARCH\_CLOSE\_AFTER](developer-guide_event-asearch_close_after.html) | Called at the end of the query execution. | | [ASEARCH\_TRANS\_AFTER](developer-guide_event-asearch_trans_after.html) | Used every time a record has been found during the search extraction. | |
| Methods or operations | A method or an operation `XXXX` where `XXXX` is the code of the method or the operation | Any operation or method that is described in the Method tabs of the class, and any operation that is described in the Operation tab of the representation will trigger an event that the name of the operation or method, in the $METHODS or $OPERATION label. The context is slightly different when we run an operation or a method:  * A method is stateful; ***this*** represents the current instance of the class; additional parameters that might have been added are declared as local variables (class [L]) with their declaration name. * An operation is stateless; ***this*** is a class instance pointer that is not filled at all. Additional parameters that should have been added are declared as local variables (class [L]) with their declaration name. The can be used to fill the instance and trigger stateful methods if needed. But at the end of the execution of the event, the instance will be destroyed (we are in stateless mode). Note that an operation can run in synchronous or asynchronous mode. More information about the asynchronous mode can be found [here](developer-guide_managing-asynchronous-operations.html). |

## Property events associated to rules ($PROPERTIES)

These events are called through $PROPERTIES for every property on the operations associated with it. `CURPRO` contains the name of the property concerned, and "This" gives access to the current instance where the property is managed.

| Value of ARULE | Details |
| --- | --- |
| [INIT](developer-guide_event-init.html) | This method is called by the supervisor:  * when a creation is performed through a representation using the *Create* link. * when a line is inserted in a grid by using the *Insert* link (on the child instance). * when a line is inserted in a collection by using the ADDLINE method   If the developer creates a line in a script directly, the AINIT method must be called manually after the class instantiation. |
| [GET](developer-guide_event-get.html) | Called when accessing a property value (for example, in a formula that needs the value to perform a control or make an assignment on another property). This rule is called only if the *Get accessor* checkbox is set for the given property in the class definition. This event should not be activated on too many properties, for performance considerations. |
| [CONTROL](developer-guide_event-control.html) | Called every time an assignment is performed on a property of an instance, except when the assignment is performed in the AREAD\_AFTER event. It is also called in the final control of a class before an insertion or an update, after verification that the field is not empty if mandatory, and after the control of format consistency. |
| [PROPAGATE](developer-guide_event-propagate.html) | Called after the **CONTROL** rule when a modification has been performed (when the modification is accepted and the field modified). |

# 4. Variables, Properties, and Methods in Events

At event execution time, development partners have access to:

* Some supervisor variables describing the context call of the event (for example, `[L]ARULE`).
* Properties of the class in which the call is performed when a working copy exists. These properties are accessed through the current class instance available through the `This` keyword. Some additional technical properties such as context description and access to parents are also available as properties.
* Methods that can be called through `Fmet` on a class instance (usually `This`).

The most important variables, properties, and methods are described as follows:

## Variables available in events

The following variables are local:

### ARULE

The `ARULE` string defines the rule called. The different values this string can have will be defined in the next pages.

### AEVENT

The `AEVENT` string defines the standard event code called. The different values this string can have will be defined in the next pages.

### AMETHOD

The `AMETHOD` string defines the method code called. The values of this string correspond to the method names defined at the class level.

### AOPERATION

The `AOPERATION` string defines the operation code called. The values of this string correspond to the operation names defined at the class level.

### CURPRO

The `CURPRO` string variable defines the property in which the event has been called (through `$PROPERTIES`label):

* If a rule defined on a child class property is defined in the script associated to the main class instance, then the path including the child instance is provided.

### CURPTH

The `CURPTH` string defines the class scope relatively to the script where te event is called.

Example of a `SALESORDER` class having a child class `SORDERLINE`:

| Type of method | Level where the script is called | ARULE value | CURPRO value | CURPTH value | Operating on |
| --- | --- | --- | --- | --- | --- |
| Rule ($PROPERTIES) associated with a DISCOUNT property (GET, CONTROL, INIT, PROPAGATE) on MYORDER.LINE(3) | SALESORDER | GET, CONTROL, INIT, or PROPAGATE | LINE.DISCOUNT | empty | this.DISCOUNT (the property) |
| Rule ($PROPERTIES) associated with a DISCOUNT property (GET, CONTROL, INIT, PROPAGATE) on MYORDER.LINE(3) | SORDERLINE | GET, CONTROL, INIT, or PROPAGATE | DISCOUNT | empty | this.DISCOUNT (the property) |
| Standard event ($EVENTS) associated with a CRUD operation (such as AINSERT\_CONTROL\_BEFORE) | SORDER | AINSERT\_CONTROL\_BEFORE | empty | empty | this (SORDER instance) |
| Standard event ($EVENTS) associated with a CRUD operation (such as AINSERT\_CONTROL\_BEFORE) | SORDERLINE | AINSERT\_CONTROL\_BEFORE | empty | empty | this (SORDERLINE instance) |
| Method ($METHODS) or operations ($OPERATIONS) defined in SORDER class (for example, VALIDATE) | SORDER (1) | VALIDATE | empty | empty | this (SORDER instance) |

(1) A method or operation will call only the label in the scripts associated with the class in which it has been defined and **not the scripts attached to child classes**.

### This

Gives access to the class instance in which the event has been called. Any property of the current class instance can be called through `this.PROPERTY` syntax.

## Properties of `This` available in events

### ASTALIN

`this.ASTALIN` is an integer defined by the supervisor as an additional property when a persistent class is created. The value defines which operations have been performed during a CRUD session. They are useful for child instances collection to identify which lines have been inserted, modified, or deleted in an update operation. They are defined by the following constants:

* `[V]CST_ALL`: Associated with an instance where no modification has been performed.
* `[V]CST_ANEW`: Identifies a new class instance that must be inserted at CRUD completion.
* `[V]CST_AUPD`: Associated with a modified instance where an update must be performed at CRUD completion.
* `[V]CST_ADEL`: Identifies an instance in which a deletion is requested.
* `[V]CST_ANEWDEL`: Identifies a new instance in which a deletion is requested. Nothing will be performed at CRUD completion.

### APARENT

`this.APARENT` property of a child instance gives access to the parent instance. This can be useful when a nested structure is used and if the event located on a line level needs to access to header values.

### snapshot

`this.snapshot` is a reference to the original value of the properties in a class when an insertion or an update is in progress. If `this.PROPERTY` is the current value (for example, in the CONTROL event), `this.snapshot.PROPERTY` gives the value that was in the property at the beginning of the operation. The following example illustrates a modification in progress on a document with HEADER and LINE classes.

* On the update events called on the header, `this` is the reference to the current header instance and `this.snapshot` is the reference to the header values after the read operation.
* On the update events called on a line, `this` is the reference to the current line instance and `this.snapshot` is the reference to the line values after the read operation.
* On the update events called on a line, `this.APARENT` is the reference to the header instance and `this.APARENT.snapshot` is the reference to the structure storing the previous values of the header instance.
* If the modification that was made on the document consists of an insertion on a line, the insert events will be called for the line. On these events, `this` is the reference to the current line instance and `this.snapshot` is the reference to the line values that are empty.

### ACTX

`this.ACTX` property gives access to the current instance of the `ACONTEXT` class. This class stores information related to the current context, especially in the following properties:

* `USER` provides the connected user code.
* `AFOLDER` provides the folder name attached to the resource.
* `LAN` and `LANISO` provide the language code, currently for three characters, and the ISO language code for five characters.
* `LOGIN` provides the login information for 30 characters.
  Additional information is stored in the context. For more information, see [Workbench reference Context Dictionary](workbench-reference_context-dictionary.html).

The use of global variables is strongly discouraged. The ACTX class (and its methods) has been performed to allow a fast access to parameters as well as global values.

### UPDTICK

`this.UPDTICK` is an integer property attached to a persistent class instance and stored in the database. It represents the current version of the line in the database. If a line has not been created, this property has a value of 0. At creation time, a database trigger fills this property with 1, and the value is returned in the class instance. In every successful modification, this property is incremented by 1 by a database trigger. When a modification attempt is performed, the instruction `RewriteByKey` updates the line only if the `UPDTICK` value in the database is still the value that has been read when the user loaded the data for modification. If this is not the case, an error will occur because the record was modified by another user.

### ALLOCGRP

`this.ALLOCGRP` is a property attached to a persistent class instance that defines the allocation group used when declaring this instance. All the instances sharing the same allocation group are freed together. The following syntax is used to ensure that a DETAIL instance shares the same allocation group as a HEADER instance:

```
this.DETAILS(I)=NewInstance C_DETAIL AllocGroup this
```

### ANUMLIN

* Deprecated, to be replaced by methods.

`this.CHILD(index).ANUMLIN` property is present on all child classes managed as a collection. This is a line number dynamically assigned at the read operation that will not change if an insertion or deletion is made. The new line inserted will receive a new number equal to the maximum number assigned plus 1. Retrieving a child instance with the line number `LINENUM` can be performed by using the following method of the parent class:

```
I=Fmet this.AGETINDBYLINE("CHILD", LINENUM)
```

  
The result can then be used to access the instance by the syntax `this.CHILD(I)`.

### AORDER

`this.CHILD(index).AORDER` property is present on all child classes managed as a collection. This is a line number that defines the display order if the property is published in a representation. This value is usually assigned when the instance is filled at the read operation. Any change on this property will change the order in which the lines are presented. Thus, inserting a line in the array can be performed by adding a new instance at the end of a child instance array when the AORDER properties have been changed so the line inserted appears in the right position.

## Other parameters available in events

### Parameters of operations

An operation handles key values that allows to find the current instance on which the operation is executed, and possibly additional parameters that are identified by a code. All these parameters are sent when the operation is called with the name used in the class dictionary on the parameter values. For the key segments, the name are the column names of the key elements in the main table associated to the class; but the other elements can be defined freely.

### Example

Let's imagine that an operation has been defined to change a value on the customer record. This method has been called SET\_MYPROP. The first argument identifies the customer. As the main table is BPCUSTOMER, and as the key used for the operation is BPC0, that has a unique segment based on the column BPCNUM, the first argument will always be BPCNUM. The second argument can be called freely (for instance NEWVALUE). In the event, the developer will test AMETHOD and if AMETHOD is equal to "SET\_MYPROP", code such as the following one can be written:

```
$METHOD_SET_MYPROP
 Local Integer OK
 OK = Fmet This.AREAD([L]BPCNUM)
 If OK=[V]CST_AOK
   This.MYPROP=[L]NEWVALUE
   OK = Fmet This.AUPDATE
   ...
```

## Methods available for `This`

### ASETERROR(PRO,MES,NUM)

The `this.ASETERROR` method is used to set an error during a control.

* `PRO` is a string identifying the context (for example, `CURPRO`).
* `MES` is a string containing the message in the right language.
* `NUM` is a numeric value (for example, an http error code).
  This method is used to set an error stored in a dedicated data structure which is available through the following property.

### AGETMAXERROR(PROPERTY\_NAME)

This method returns the highest error code found in the error classes for a given property. PROPERTY\_NAME is a string containing the property for which the error is requested. If the property is empty, the error relates to the errors found during class methods execution.

### ADELETEERROR(PROPERTY\_NAME)

This method cancels the errors associated with a given property. PROPERTY\_NAME is a string containing the property for which the error has to be cancelled. If the property is empty, the errors found globally for the class will be cancelled.

### ASETATTRIBUTE(PROPERTY\_NAME, ATTRIBUTE\_NAME, VALUE)

This method is used to change attributes values associated with properties. On classes, only some attributes are used, but other attributes related to the user interface can be set up for class properties embedded in representations.

The available attributes are described below. If they are not assigned by this method, the value defined in the class dictionary is used.

| Code | Attribute | Possible values |
| --- | --- | --- |
| $isMandatory | Mandatory property. This attribute is set at class level. | true, false |
| $isDisabled | The property cannot be inputted. This attribute is valid only for properties in a representation. | true, false |
| $isHidden | The property is not displayed. This attribute is valid only for properties in a representation. | true, false |

Some other attributes are managed by the supervisor and depend only from the meta data defined in the representation dictionary. Thus they cannot be changed dynamically. For instance:

* a field defined as **Technical** for a facet in the representation will never appear on the page, and will also not be visible in personalization mode.
* a field with the *Enterable* check box not set for the Edit facet can be only displayed with no input possibility in any case.

For the fields having the *Enterable* check box set for the Edit facet, their state can be dynamically changed in a script by using the *ASETATTRIBUTE* method with the ***$isDisabled*** attribute. They can also be hidden by using the *ASETATTRIBUTE* method with the ***$isHidden*** attribute.

The fields defined with an *Initial state* equal to **Visible** (resp. **Invisible**) for a given facet will be visible (resp. invisible) by default on the facet. But this state can be changed dynamically in a script by using the *ASETATTRIBUTE* method with the ***$isHidden*** attribute.

Of course, any visible field can be hidden by personalization, and any hidden (not technical) field can be made visible by personalization.

# 5. Event Execution on Nested Classes

There are many events available due to the complex hierarchy of classes that exists for the management of a complex entity. For example, we can have a `MYDOC` instance of a `DOCUMENT` class that has a collection of `LINE` class called `DOCLINE`, which has a collection of `SUBLINES` named `DETAIL`.

## Example of insertion

In this example, let's consider inserting new data using the 'AINSERT\_CONTROL\_BEFORE' event. The description of the event calls nesting is relevant if the complete CRUD execution code is generated at the `DOCUMENT` level (if the Class management check box is not set on the *Mapping* section in the class dictionary). In that case, the events are called with the following logic:

```
AINSERT_CONTROL_BEFORE
  called in the files associated with DOCUMENT class:
   - on class DOCUMENT
   - for the document instance
   - this is the MYDOC class instance
   - CURPTH is empty (the control is done for the current class)
  For every LINE instance in the document (loop on I):
  |   AINSERT_CONTROL_BEFORE called in the files associated with LINE class:
  |    - on class LINE for the current line DOCLINE instance
  |    - this is the MYDOC.DOCLINE(I) class instance
  |    - CURPTH is empty (the control is done for the current class)
  |   AINSERT_CONTROL_BEFORE called in the files associated with DOCUMENT class:
  |    - on class DOCUMENT for the MYDOC.DOCLINE(I) instance
  |    - this is the MYDOC class instance
  |    - CURPTH is "DOCLINE" (the control is done for the child class)
  |   For every SUBLINE in the line instance (loop on J):
  |   |  AINSERT_CONTROL_BEFORE called in the files associated with SUBLINE class:
  |   |   - on class SUBLINE
  |   |   - for the current SUBLINE instance
  |   |   - this is the MYDOC.DOCLINE(I).DETAIL(J) class instance
  |   |   - CURPTH is empty (the control is done for the current class)
  |   |  AINSERT_CONTROL_BEFORE called in the files associated with LINE class:
  |   |   - on class LINE
  |   |   - for the current LINE instance
  |   |   - this is the MYDOC.DOCLINE(I) class instance
  |   |   - CURPTH is "DETAIL" (the control is done for the child class)
  |   |  AINSERT_CONTROL_BEFORE called in the files associated with DOCUMENT class:
  |   |   - on class DOCUMENT
  |   |   - for the current DOCUMENT instance
  |   |   - this is the MYDOC class instance
  |   |   - CURPTH is "DOCLINE.DETAIL" (the control is done for the grand child class)
  |   Next SUBLINE instance (loop on J)
  Next LINE instance (loop on J)
```

  
This allows adding code, in the events available on classes, that will be executed in addition to the class code when the class instance is a child of another class. In such cases, parent classes can be accessed through `APARENT`. For instance, a property `PROP1` of the `DOCUMENT` class can be accessed in the code attached to `SUBLINE` through the following syntax: `this.APARENT.APARENT.PROP1`.

This principle of code nesting exists on all the other events listed above, but on the 'AINSERT\_AFTER', the event is performed on the nesting level after the events on the sub-level have been performed. This means that the order is as follows:

1. Perform the events on all the sub-lines associated with the first line.
2. Perform the event on the first line.
3. Continue to the other lines with the same logic, and after all lines have been managed, perform the event for the document.

## Example of a complex update

The previous example (Insertion) works when an insertion of a new instance of a class is performed.

On updates, when child class collections exist on a class, an update operation on a complex document can consist of inserting lines, deleting lines, or modifying lines. You must consider that a modification of a document will call the events defined for deletion, insertion, or modification on the child classes, depending on the modification encountered.

In fact, it will depend on the `this.ASTALIN` property for a given instance at a given level:

* If the value `[V]CST_ALL` or `[V]CST_ANEWDEL` is found, nothing will be called. The line has not been modified, or has been temporarily inserted and then deleted.
* If the value `[V]CST_ANEW` is found, the events associated with an insertion will be performed.
* If the value `[V]CST_AUPD` is found, the events associated with an update will be performed.
* If the value `[V]CST_ADEL` is found, the events associated with a deletion will be performed.

If a modification is done, the modification events will be performed at the document level.

The loop nesting principles are anyways the same, the 'BEFORE' operations are nested in descending level, while the 'AFTER' operation is performed on the lowest level of a collection of child class instances before performing it on the class including the collection.

## Notes:

1. This works also if a class has two child classes that are not nested. In this case, the loops are performed on the two child class instances independently.
2. When nested classes are declared, the calls on the CRUD events are performed at the different level as described above. **On other class methods, the call is performed only on the scripts declared in the corresponding class and not on the child classes**.

# 6. Event Execution when UI is Involved

## Events

When the code associated with events is executed in service mode, no UI event interferes with the methods described previously, and the description of the nested event calls that has been done in the previous section is complete.

When a UI is involved in the process, there is a parent class associated with the main class (representation).

An additional level of event will be executed because the representation instance that can include additional properties dedicated only to the UI will also include a reference to the main class. The complete path of a sub-line property would then be in the representation event:

`REPRESENTATION.DOCUMENT.LINE.SUBLINE.FINAL_PROPERTY`, and the event on the different events would also be called from the files associated with the representation using `CURPRO="MYREP.MYDOC.LINE.SUBLINE"` where  
``this` would be equal to `MYREP.MYDOC.LINE(I).SUBLINE(J)`.

Some additional events dedicated to UI methods and operation also exist. They are documented in the representation description.

## Dedicated UI methods

### Links enablement or disablement

Dedicated methods exist to enable or disable links associated to the page level and to the record level.

**They work only in *Details* facet (not in *Edit* mode).**

These methods are the following:

* **ASETLINKDISABLE** disables a link.
* **ASETLINKENABLE** enables a link.

The parameters are, in both cases:  
\* **CODLNK** : a string that contains the code of the link  
\* **AFFLNK** : a local menu that can have one of the two following constant values: CST\_AFFLNKREC and CST\_AFFLNKPAG.

### Example of use:

```
# After reading a record, we might disable links according to the content of the class
$AREAD_AFTER
If this.MYCLASS.MYPROP="A1"
    [L]ASTATUS = fmet this.ASETLINKDISABLE("AEDIT",[V]CST_AFFLNKREC)
    [L]ASTATUS = fmet this.ASETLINKDISABLE("TEST",[V]CST_AFFLNKPAG)
    [L]ASTATUS = fmet this.ASETLINKDISABLE("ADELETE",[V]CST_AFFLNKREC)
    [L]ASTATUS = fmet this.ASETLINKDISABLE("ENR",[V]CST_AFFLNKREC) 
Elsif this.MYCLASS.MYPROP="A2"
    [L]ASTATUS = fmet this.ASETLINKDISABLE("AQUERY",[V]CST_AFFLNKPAG)
    [L]ASTATUS = fmet this.ASETLINKDISABLE("ACREATE",[V]CST_AFFLNKPAG)
    [L]ASTATUS = fmet this.ASETLINKENABLE("ENR",[V]CST_AFFLNKPAG)
Else
    [L]ASTATUS = fmet this.ASETLINKDISABLE("AEDIT ",[V]CST_AFFLNKPAG)
    [L]ASTATUS = fmet this.ASETLINKDISABLE("ADELETE ",[V]CST_AFFLNKPAG)
    [L]ASTATUS = fmet this.ASETLINKDISABLE("AQUERY",[V]CST_AFFLNKPAG)
Endif
```

# 7. Sage X3 Script Managing Events Example

This example illustrates a 'SORDER' class having a 'SORDERLINE' child class. It is the of a script declared in 'SORDER' class, which calls separate subprograms.

```
###############
# CLASS SORDER
###############
# EVENTS
###############
$EVENTS
Case CURPTH
   When ""         
     Case AEVENT
       When "AINSERT_CONTROL_AFTER"        : Gosub AINSERT_CONTROL_AFTER : # Standard CRUD method
       When "AUPDATE_CONTROL_AFTER"        : Gosub AUPDATE_CONTROL_AFTER : # Standard CRUD method
       When "AINSERT_BEFORE"               : Gosub AINSERT_BEFORE        : # Standard CRUD method
       When "AUPDATE_BEFORE"               : Gosub AUPDATE_BEFORE        : # Standard CRUD method
     Endcase
   When "LINE"
     Case AEVENT
       When "AINSERT_CONTROL_AFTER"   : Gosub LINE_AINSERT_CONTROL_AFTER : # Standard CRUD operation on line
       When "AUPDATE_CONTROL_AFTER"   : Gosub LINE_AUPDATE_CONTROL_AFTER : # Standard CRUD operation on line
       When "AINSERT_BEFORE"          : Gosub LINE_AINSERT_BEFORE : # Standard CRUD operation on line
     Endcase
Endcase

###############
# METHODS
###############
$METHODS
Case AMETHOD
   When "VALID"                        : Gosub VALID                 : # Class method
Endcase
Return
###############
# OPERATIONS
###############
$OPERATIONS
Case AOPERATION
   When "POST"                        : Gosub POST                 : # Class operation
Endcase
Return
#############
# RULES
#############
$PROPERTIES
Case CURPRO
  When "PROP1"       : Gosub PROP1 : # Methods attached to property PROP1
  When "PROP2"       : Gosub PROP2 : # Methods attached to property PROP2
  When "LINES.PROP3" : Gosub PROP3 : # Methods attached to property PROP3 of a LINE child instance
Endcase
Return
#######
$PROP1
Case ARULE
   When "INIT"      : Gosub PROP1_INIT      : # Init rule attached to PROP1
   When "CONTROL"   : Gosub PROP1_CONTROL   : # Control rule attached to PROP1
   When "PROPAGATE" : Gosub PROP1_PROPAGATE : # Propagate rule attached to PROP1
   When "GET"       : Gosub PROP1_GET       : # Get rule attached to PROP1  
Endcase
Return
#######
$PROP2
Case RULE
   When "INIT"      : Gosub PROP2_INIT      : # Init rule attached to PROP2
   When "CONTROL"   : Gosub PROP2_CONTROL   : # Control rule attached to PROP2
   When "PROPAGATE" : Gosub PROP2_PROPAGATE : # Propagate rule attached to PROP2
   When "GET"       : Gosub PROP2_GET       : # Get rule attached to PROP2
Endcase
#######
$PROP3
# As the rule is attached to a line instance
# "this" is here the line instance and this.PROP3 the property on the current line
Case ACTION
   When "INIT"      : Gosub PROP3_INIT      : # Init rule attached to PROP3
   When "CONTROL"   : Gosub PROP3_CONTROL   : # Control rule attached to PROP3
   When "PROPAGATE" : Gosub PROP3_PROPAGATE : # Propagate rule attached to PROP3
   When "GET"       : Gosub PROP3_GET       : # Get rule attached to PROP3
Endcase

Return
```

  

[Index](index.html)  [Home](getting-started_home.html)