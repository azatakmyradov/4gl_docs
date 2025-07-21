[Index](index.html)  [Home](getting-started_home.html)

Setinstancenosys

This instruction performs an assignment between the properties of a class instance and the content of a file class or a mask class (for example, an [F:xxxx] table buffer or [M:yyyy] mask class), in one direction or the other. It works exactly as setinstance, but it excludes technical properties from the assignment.

This transfer is based on the property names and the column names; the transfer is done only on the common names.

* The syntaxes (1) and (2) are transferring only elements that are not in arrays / collections.
* The syntaxes (3) and (4) are dedicated to this kind of transfer.

When the transfer is done between a collection in an instance and an array in the mask (ie. a block identified by a rank from 1 to 99), the current collection index is given in the syntax, and the current index in the mask array is given by the `nolign` system variable (that goes from 1 to the number of lines).

This instruction is used intensively by the CRUD operation support implemented in the supervisor layer. The name of the columns in the database tables and the name of the property in a class must be the same if the development partner wants to benefit from a complete automatic management of class persistence in the database. If this is not the case for some properties, the development partner must write the assignment directly in the corresponding events available in CRUD management.

# Syntax

```
(1)   SetInstancenosys [F:xxxx] With INSTANCE_NAME
(2)   SetInstancenosys INSTANCE_NAME With [F:xxxx]

(3)   SetInstancenosys [M:xxxx] RANK With INSTANCE_NAME.COLLECTION(INDEX)
(4)   SetInstancenosys [M:xxxx] With INSTANCE_NAME
(5)   SetInstancenosys INSTANCE_NAME.COLLECTION(INDEX) With [M:xxxx] RANK
(6)   SetInstancenosys INSTANCE_NAME With [M:xxxx]
```

\*\*Notes:\*\*

* [F:xxxx] is the buffer-class description, that can also be written [xxxx] if there is no ambiguity.
* [M:xxxx] is the screen class description, that can also be written [xxxx] if there is no ambiguity.
* INDEX is a numeric expression that gives the index of the line that will be transferred.
* RANK is the rank - ie the block number in the mask - of the array to be transferred in the screen (the line is given by `nolign`)

The properties that are excluded from the transfer are the following:

| Property | Description |
| --- | --- |
| Updtick | Revision number |
| AUUID | Unique ID |
| CREDAT | Creation date |
| UPDDAT | Update date |
| CREUSR | User who performed the creation |
| UPDUSR | User who performed the last update |
| CREDATTIM | Creation date time |
| UPDDATTIM | Update date time |

# Examples

This first example involves only a class and a table:

```
# Instance pointer on a customer class
Local Instance MY_CUSTOMER Using C_CUSTOMER
Local File CUSTOMERS [CUST]

# Let's create a instance in memory for a customer
  MY_CUSTOMER = NewInstance C_CUSTOMER AllocGroup Null

# Let's read a customer record, and transfer the data in the instance created
  Read [CUST]CODE="CUST1234"
  SetInstancenosys MY_CUSTOMER With [F:ORD]
```

This second example involves a class with a collection, a mask with an array, and two tables (header / line) :

```
# Instance pointer on a sales order class
Local Instance MY_SALESORDER Using C_SALESORDER

# Table declaration
Local File SALESORDER [ORD], SALESLINE [LINE]

# Mask declaration
Local Mask SALESORDER [ORD]

# Other variable declaration
Local Shortint LNUM

# Let's create an instance in memory for a customer
  MY_SALESORDER = NewInstance C_SALESORDER AllocGroup Null

# Let's read a salesorder header, and transfer the data in the instance created
  Read [ORD]ORDERID="0012345"
  SetInstancenosys MY_SALESORDER With [F:ORD] 

# Let's read the lines that in a collection
  For [LINE]ORDLIN Where [LINE]ORDLIN=[F:ORD]ORDLIN
    LNUM=fmet MY_SALESORDER.ADDLINE("LINES",[V]CST_ALASTPOS)
    If LNUM>=0
      SetInstancenosys MY_SALESORDER.LINES(LNUM) With [F:LINE]
    Else
      Break
    Endif
  Next

# Here we might work and modify sales order instance
  ....

# Let's transfer the class in a mask that has the line array at rank 20
# We suppose here that :
#  - all the lines are valid (no test about ASTALIN property in LINES)
#  - the logical order is the same than the physical order (nolign directly used as the loop index)
  SetInstancenosys [M:ORD] with MY_SALESORDER
  For nolign=1 to maxtab(MY_SALESORDER.LINES)
     SetInstancenosys [M:ORD] 20 With MY_SALESORDER.LINES(nolign)
  Next nolign
```

# See also

[Structure](4gl_glossary-structure.html), [Instance](4gl_instance.html), [SetInstance](4gl_setinstance.html), [NewInstance](4gl_newinstance.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [allocgrp](4gl_allocgrp.html), [cast](4gl_cast.html), [null](4gl_null.html)

  

[Index](index.html)  [Home](getting-started_home.html)