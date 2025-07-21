[Index](index.html)  [Home](getting-started_home.html)

Objecttype

This built-in property returns the name of the class or representation of an instance.

# Syntax

```
MY_INSTANCE.objecttype
```

# Example

```
Local Instance OBJ Using OBJECT
OBJ = NewInstance [GRP] Using C_CUSTOMER
TYPE= OBJ.objecttype
# TYPE is "C_CUSTOMER"
OBJ = NewInstance [GRP] USING C_SALESREP
# TYPE is "C_SALESREP"
```

# See also

[Structure](4gl_glossary-structure.html), [Instance](4gl_instance.html), [SetInstance](4gl_setinstance.html), [NewInstance](4gl_newinstance.html), [null](4gl_null.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [cast](4gl_cast.html).

  

[Index](index.html)  [Home](getting-started_home.html)