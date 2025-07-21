[Index](index.html)  [Home](getting-started_home.html)

Newinstance

This instruction allocates a [class](developer-guide_classes.html) or [representation](developer-guide_representations.html) instance.

# Syntax

```
RESULT = NewInstance CLASS_NAME AllocGroup Null
RESULT = NewInstance CLASS_NAME AllocGroup OTHER_INSTANCE
```

* **CLASS\_NAME** is the name of the class
* **OTHER\_INSTANCE** is another instance that will be freed at the same time

With the first syntax, the engine creates a dedicated allocation group. Be carefull when using this syntax not to exhaust the number of allocation groups which is limited to 1023 (see [ALLOCGRP](4gl_allocgrp.html))

With the second syntax, we use the same allocation group as the instance called "OTHER\_INSTANCE".

The allocation group simplifies memory management. When you free a given group, all the instances in the group will be freed at the same time.

The [ALLOCGRP](4gl_allocgrp.html) built-in property returns the allocation group of an instance. This can be useful for debug purposes, if you want to verify whether two instances belong to the same group or not.

# Example

```
  # Declare customer and sales rep instance
  Local Instance MY_CUSTOMER Using C_CUSTOMER
  Local Instance MY_SALESREP Using C_SALESREP

  # Allocate them in the same allocation group
  MY_CUSTOMER = NewInstance C_CUSTOMER AllocGroup Null
  MY_SALESREP = NewInstance C_SALESREP AllocGroup MY_CUSTOMER
 ...

  # Free them
  FreeGroup MY_CUSTOMER : # FreeGroup MY_SALESREP would have the same effect
```

# Comment

The syntax of `NewInstance` and `FreeInstance` evolved since the beginning, and `FreeGroup` has been added. The old syntaxes using "With" keyword and an allocation group between brackets are deprecated and must no more be used.

# See also

[Structure](4gl_glossary-structure.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [Instance](4gl_instance.html), [SetInstance](4gl_setinstance.html), [allocgrp](4gl_allocgrp.html), [cast](4gl_cast.html), [null](4gl_null.html).

  

[Index](index.html)  [Home](getting-started_home.html)