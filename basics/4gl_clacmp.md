[Index](index.html)  [Home](getting-started_home.html)

Clacmp

`clacmp` allows you to compare two classes (usually two classes that are associated with tables). It compares both the structure and the contents of the class.

# Syntax

```
   clacmp(CLASS_DESCRIPTION,CLASS_DESCRIPTION)
```

* `CLASS_DESCRIPTION` is a class description with the `[ABBR]` syntax, where `ABBR` is the abbreviation of a class.

# Examples

```
  # Check if the two tables have really the same structure 
  Local File MYTABLE [MYT], COPIEDTABLE [CPTB]
  If clacmp([MYT],[CPTB])=0
    # The table structure are identical (columns, type, dimensions), although the indexes can be different.
  Else
    # If it is not the case, the value returned is 2
  Endif

  # Check if two records are absolutely identical
  Local File MYTABLE [MYT], MYTABLE [MYT1]
  For [MYT] Where A="VALUE1"
    Read [MYT1]KEY1="2";"B"
    # Is the line read on [MYT1] absolutely identical to the line read on [MYT] ?
    If clacmp([MYT1],[MYT])=0
      # The data record is identical
    Else
      # As the table has been opened twice, the structure is identical, but the content is not the same (value 1)
    Endif
    Break
  Next
```

# Description

`clacmp` allows you to compare two classes given as arguments. The following values can be returned:  
\* **0** if the class structure and the content of all variables is identical.  
\* **1** if the class structure is identical, but some variables have different values.  
\* **2** if the class structure is not identical.

The result of the function is an [Integer](4gl_integer.html).

# Associated errors

| Error | Description |
| --- | --- |
| 7 | A class does not exist. |

# See also

[clalev](4gl_clalev.html), [clasiz](4gl_clasiz.html), [clanbs](4gl_clanbs.html), [clavar](4gl_clavar.html).

  

[Index](index.html)  [Home](getting-started_home.html)