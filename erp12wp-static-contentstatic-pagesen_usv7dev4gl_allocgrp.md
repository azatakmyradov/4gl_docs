[Index](index.html)  [Home](getting-started_home.html)

Allocgrp

This built-in property returns the allocation group of an instance. Allocgrp is essentially a technical property and is rarely used.

The allocation group is shared between instances that have to be freed at the same time. This is ensured by the mention of a group in `NewInstance`syntax.

AllocGroup has to be followed by the identifier of the allocation group to be used:  
 - **Null** : in this case the runtime creates a new allocation group. (example: AllocGroup Null). The number of allocation groups is **limited to 1023**. Be carefull when using this syntax not to exhaust the number of allocation groups. This is particurlarly the case when creating an array of instances (see following example).  
 - **[ALLOCATION GROUP]** : in this case the runtime reuses the [ALLOCATION GROUP]. (example : AllocGroup MYORDER).

# Syntax

```
MYINSTANCE.allocgrp
```

# Example

```
# This program creates a C_SALESORDER instance 
# with C_SORDERLINE child instances and C_LINEDETAILS grandchild instances.
# All these instances are created in the same allocation group.

Local Instance MYORDER Using C_SALESORDER
MYORDER=NewInstance C_SALESORDER AllocGroup Null

# Instantiate 5 lines and 3 line details in every line
  For I=1 to 5
    MYORDER.LINE(I)=NewInstance C_SORDERLINE AllocGroup MYORDER
    # MYORDER.LINE(I).allocgrp is equal to MYORDER.allocgrp
    For J=1 to 3
      MYORDER.LINE(I).SUBLINE(J)=NewInstance C_SLINEDETAILS AllocGroup MYORDER.LINE(I)
      # or (simpler !)
      # MYORDER.LINE(I).SUBLINE(J)=NewInstance C_SLINEDETAILS AllocGroup MYORDER
    Next J
  Next I

# Handle the sales order and then insert it into the database
  Call MANAGE_MY_ORDER(MYORDER)
  Fmet MYORDER.AINSERT

# Free all instances (they are all in the same allocation group)
  FreeGroup MYORDER
```

# See also

[Structure](4gl_glossary-structure.html), [Instance](4gl_instance.html), [SetInstance](4gl_setinstance.html), [NewInstance](4gl_newinstance.html), [null](4gl_null.html), [FreeInstance](4gl_freeinstance.html), [cast](4gl_cast.html)

  

[Index](index.html)  [Home](getting-started_home.html)