[Index](index.html)  [Home](getting-started_home.html)

Clanam

`clanam` allows you to know the name of a class (usually a table associated class) if available in a given context. The class name is returned with the complete class path.

# Syntax

```
   clanam(CLASS_DESCRIPTION)
   clanam(NUMERIC_EXPRESSION)
```

* `CLASS_DESCRIPTION` is a class description with the `[ABBR]` syntax, where `ABBR` is the abbreviation of a class.
* `NUMERIC_EXPRESSION` refers to the slot number for the class. This can be seen in the debugger, but should be considered internal.

# Examples

```
  # Check the number of classes that have MYT in their code
  Local File MYTABLE [MYT]
  Local char CLASSES(10)(1..10)
  local Integer I,J
  For I=1 to 200
    If pat(clanam(I),"*MYT*")
      J+=1 : CLASSES(J)=clanam(I)
    Endif
  Next I
  # At this point, J should be at least equal to 2, and the 2 class names "[F:MYT]" and "[G:MYT]" should have been found.

  # Is the table with [ABC] abbreviation opened?
  If clanam([ABC])<>""
    # The table is opened
  Endif
```

# Description

`clanam` allows you to return the name of a class available in the execution context. If the class is not available, then the return is an empty string.

The result of the function is string character.

# Associated errors

| Error | Description |
| --- | --- |
| 50 | The numeric argument is negative. |

# See also

[clalev](4gl_clalev.html), [clasiz](4gl_clasiz.html), [clanbs](4gl_clanbs.html), [clavar](4gl_clavar.html).

  

[Index](index.html)  [Home](getting-started_home.html)