[Index](index.html)  [Home](getting-started_home.html)

Cast

This function casts a generic instance to an instance of specific class or representation.

# Syntax

```
SPECIFIC_INSTANCE=cast(GENERIC_INSTANCE, CLASS_NAME)
```

* `GENERIC_INSTANCE` is a generic instance, declared with the `OBJECT` class.
* `CLASS_NAME` is the name of the class we are casting to.
* `SPECIFIC_INSTANCE` is the specific instance that we obtain by casting.

# Example

```
# Generic Instance that we will cast later
Local Instance OBJECT_INSTANCE Using OBJECT

# Assign a C_ORDERLINE instance to OBJECT_INSTANCE
# Note: we cannot invoke C_ORDERLINE methods on OBJECT_INSTANCE as it was declared
# as an OBJECT instance rather than a C_ORDERLINE instance.
  OBJECT_INSTANCE = NewInstance With C_ORDERLINE

# Declare an array of 15 C_ORDERLINE instances
Local Instance SORDER_LINES(1..15) Using C_ORDERLINE

  # Assign OBJECT_INSTANCE to the first element of the array
  # A cast is necessary to obtain compatible types.
  SORDER_LINES(1) = cast(OBJECT_INSTANCE, "C_ORDERLINE")

  # Retrieve the objectType property of this array element
  TYPE=SORDER_LINES(1).Objecttype
  # TYPE is "C_ORDERLINE"
```

# Comments

`OBJECT` is a generic class for variables that may hold instances allocated in different classes.   
The `OBJECT` class does not have any properties or methods, besides the built-in properties available on all objects.   
You must cast an `OBJECT` variable with the appropriate class name to access its properties and methods,   
or to assign it to a variable of a specific class.

# See also

[Structure](4gl_glossary-structure.html), [FreeInstance](4gl_freeinstance.html), [Instance](4gl_instance.html), [NewInstance](4gl_newinstance.html), [SetInstance](4gl_setinstance.html), [allocgrp](4gl_allocgrp.html), [null](4gl_null.html)

  

[Index](index.html)  [Home](getting-started_home.html)