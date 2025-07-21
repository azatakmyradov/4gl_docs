[Index](index.html)  [Home](getting-started_home.html)

Freeinstance

This instruction frees the memory of an instance. The other instances in the same allocation group are not freed; this can be done by using [FreeGroup](4gl_freegroup.html) instruction.

**Take care than using `Freeinstance` rather than `Freegroup` can bring to memory leaks because the children instances are not freed, and can no more be freed (there is no more a pointer that allows finding them). So this instruction should be avoided in most of the cases.**

# Syntax

```
Freinstance INSTANCE_VAR
```

See [allocgrp](../4gl/allocgrp.md), [FreeGroup](../4gl/freegroup.md) and [NewInstance](../4gl/newinstance.md) for more information on instance allocation and allocation groups.

# Example

```
# Declare two instances
Local Instance MY_CUSTOMER Using C_CUSTOMER
Local Instance MY_SALESREP

# Allocate both instances in the same allocation group
  MY_CUSTOMER = NewInstance C_CUSTOMER AllocGroup Null
  MY_SALESREP = NewInstance C_SALESREP AllocGroup MY_CUSTOMER

 ...

# Free the allocation group
  FreeInstance MY_CUSTOMER : # FreeInstance MY_SALESREP would free MY_SALESREP
                             # FreeGroup    MY_CUSTOMER would free both
```

# Comments

`FreeInstance` frees the memory but does not change the pointers that refers to the resources. Using them after a `FreeInstance` will generate errors. It can be useful to reassign them to `null` pointer :

```
Local Instance MY_CUSTOMER Using C_CUSTOMER
MY_CUSTOMER=NewInstance C_CUSTOMER AllocGroup Null
...
FreeInstance MY_CUSTOMER
MY_CUSTOMER=null
```

As soon as an instance might have children instances, the children instances are allocated in the same group, and using `Freeinstance` rather than `Freegroup` will bring to memory leaks. For example:

```
Local Instance MY_ORDER Using C_YORDER
MY_ORDER=NewInstance C_YORDER AllocGroup Null
...
# Let's create an order
OK=Fmet MY_ORDER.AINIT

# Let's add a first line
# This creates a child intance of a class C_YLINE in the same group than MY_ORDER
OK=Fmet MY_ORDER.ADDLINES("LINES",[V]CST_ALASTPOS)

# Let's create the order
OK=Fmet MY_ORDER.AINSERT

# Let's free incorrectly the order
FreeInstance MY_ORDER

# Now, MY_ORDER instance is freed, and trying to access to a property of MY_ORDER would fail
# As the only pointer I created on the line instance was MY_ORDER.LINES(1) that is no more available
# I can no more free the line, so I have a memory leak

# The right way to do it is:
FreeInstance MY_ORDER.LINES(1)
FreeInstance MY_ORDER

# But if for any reason an error was raised during a control, an AERROR sub-instance can have been created
# somewhere and this will also not bee freed at FreeInstance. So finally, the unique way to do it properly is:
FreeGroup MY_ORDER
```

# See also

[Structure](4gl_glossary-structure.html), [Instance](4gl_instance.html), [SetInstance](4gl_setinstance.html), [NewInstance](4gl_newinstance.html), [null](4gl_null.html), [allocgrp](4gl_allocgrp.html), [cast](4gl_cast.html), [FreeGroup](4gl_freegroup.html)

  

[Index](index.html)  [Home](getting-started_home.html)