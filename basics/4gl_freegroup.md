[Index](index.html)  [Home](getting-started_home.html)

Freegroup

This instruction frees the memory of an instance and all the instances sharing the same allocation group.

# Syntax

```
FreeGroup INSTANCE_VAR
```

See [allocgrp](../4gl/allocgrp.md) and [NewInstance](../4gl/newinstance.md) for more information on instance allocation and allocation groups.

# Example

```
# Declare two instances
Local Instance MY_CUSTOMER Using C_CUSTOMER
Local Instance MY_SALESREP Using C_SALESREP
Local Instance MY_COUNTRY Using C_COUNTRY

# Allocate both instances in the same allocation group
  MY_CUSTOMER = NewInstance C_CUSTOMER AllocGroup Null
  MY_SALESREP = NewInstance C_SALESREP AllocGroup MY_CUSTOMER
  MY_SALESREP = NewInstance C_SALESREP AllocGroup MY_CUSTOMER
  MY_COUNTRY = NewInstance C_COUNTRY AllocGroup MY_SALESREP

 ...

# Free only the country instance
  FreeInstance MY_COUNTRY : # MY_CUSTOMER and MY_SALESREP still allocated

# Free the allocation group (this would have freed MYCOUNTRY also if it had not already been done)
  FreeGroup MY_CUSTOMER : # FreeGroup MY_SALESREP would have the same effect
```

# Comment

`FreeGroup` frees the memory but does not change the pointers that refer to the resources. Using them after a `FreeGroup` will generate errors. It can be useful to reassign them to a `null` pointer.

```
Local Instance MY_CUSTOMER Using C_CUSTOMER
MY_CUSTOMER=NewInstance C_CUSTOMER AllocGroup Null
...
FreeGroup MY_CUSTOMER
MY_CUSTOMER=null
```

# See also

[Structure](4gl_glossary-structure.html), [Instance](4gl_instance.html), [SetInstance](4gl_setinstance.html), [NewInstance](4gl_newinstance.html), [null](4gl_null.html), [allocgrp](4gl_allocgrp.html), [cast](4gl_cast.html), [FreeInstance](4gl_freeinstance.html).

  

[Index](index.html)  [Home](getting-started_home.html)