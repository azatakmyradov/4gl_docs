[Index](index.html)  [Home](getting-started_home.html)

Objectvar

This keyword gives access to the Nth properties of the class associated with a given instance ('N' given as a parameter). It might be important if a pointer to a class is sent to a program that will explore the properties of the class.

For a given instance called "MYINSTANCE", 'N' can be in the range (1,MYINSTANCE.objectnbs).

# Syntax

```
MYINSTANCE.objectvar(N)
```

# Example

```
Funprog DUMP_PROPERTIES(OBJ, TEXT)
Value Instance OBJ Using OBJECT
Variable Char TEXT()(1..)
  For I=1 to OBJ.objectnbs
    TEXT(I)=OBJ.objectvar(I)+": "+evalue("OBJ."+OBJ.objectvar(I))
  Next I
End
```

For a complete example, see [Generic Object Dump Example](../api-guide/generic-object-dump-example.md).

# See also

[Structure](4gl_glossary-structure.html), [Instance](4gl_instance.html), [SetInstance](4gl_setinstance.html), [NewInstance](4gl_newinstance.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [cast](4gl_cast.html), [null](4gl_null.html), [objectnbs](4gl_objectnbs.html), [objecttype](4gl_objecttype.html).

  

[Index](index.html)  [Home](getting-started_home.html)