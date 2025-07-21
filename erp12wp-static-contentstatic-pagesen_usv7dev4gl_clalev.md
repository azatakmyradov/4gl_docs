[Index](index.html)  [Home](getting-started_home.html)

Clalev

`clalev` allows you to know if a class (usually a table associated class) can be accessed in a given context.

# Syntax

```
   clalev(CLASS_DESCRIPTION)
   clalev(NUMERIC_EXPRESSION)
```

* `CLASS_DESCRIPTION` is a class description with the `[ABBR]` syntax, where `ABBR` is the abbreviation of a class.
* `NUMERIC_EXPRESSION` refers to the slot number for the class. This can be seen in the debugger, but should be considered rather as internal.

# Examples

```
  # List of the classes available in the current context
  Local Integer MAXCLA,I,J
    MAXCLA = 200
  Local Char CLASS_NAMES(20)(1..MAXCLA)
    For I = 1 To MAXCLA
       If clalev(I) <> 0
          J+=1
          CLASS_NAMES(J)=clanam(I)
       Endif
    Next I

  # If the [ORDER] table opened
  If clalev([ORDER])
    # The table is already opened
  Else
    # The table is not opened
  Endif
```

# Description

`clalev` allows you to determine if a class with a given abbreviation is available.

The result of the function is an integer value of 1 (if the class is available) or 0 (if the class is not available).

# Comments

This function was used in version 6 programming to avoid re-opening an already opened table. In version 7, it is deprecated because opening a table has been optimized and also because not opening a table can cause conflicts.

You can still use it when a common subprogram is supposed to use an already opened class, and open it if it is not the case.

# Associated errors

| Error | Description |
| --- | --- |
| 50 | The numeric argument is negative. |

# See also

[clanam](4gl_clanam.html), [clasiz](4gl_clasiz.html), [clanbs](4gl_clanbs.html), [clavar](4gl_clavar.html).

  

[Index](index.html)  [Home](getting-started_home.html)