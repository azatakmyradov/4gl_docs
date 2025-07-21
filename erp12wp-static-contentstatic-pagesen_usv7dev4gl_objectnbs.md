[Index](index.html)  [Home](getting-started_home.html)

Objectnbs

This built-in property returns the number of properties of an instance.

This property is used with [objectvar](4gl_objectvar.html) to iterate on the properties of a generic instance.

# Syntax

```
MY_INSTANCE.objectnbs
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

[Structure](4gl_glossary-structure.html), [Instance](4gl_instance.html), [SetInstance](4gl_setinstance.html), [NewInstance](4gl_newinstance.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [cast](4gl_cast.html), [null](4gl_null.html), [objecttype](4gl_objecttype.html), [objectvar](4gl_objectvar.html).

  

[Index](index.html)  [Home](getting-started_home.html)