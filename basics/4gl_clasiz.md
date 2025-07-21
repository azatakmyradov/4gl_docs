[Index](index.html)  [Home](getting-started_home.html)

Clasiz

`clasiz` allows you to know the size used by a class (in bytes).

# Syntax

```
   clasiz(CLASS_DESCRIPTION,OPTION)
   clasiz(NUMERIC_EXPRESSION,OPTION)
```

* `CLASS_DESCRIPTION` is a class description with the `[ABBR]` syntax, where `ABBR` is the abbreviation of a class.
* `OPTION` is an integer expression returning 1 or 2.
* `NUMERIC_EXPRESSION` refers to the slot number for the class. This can be seen in the debugger, but should be considered internal.

# Examples

```
  # Check the size used by the local variable class
  SIZE1=clasiz([L],1) : # The size used by [L] variables
  SIZE2=clasiz([L],2) : # The size currently allocated for [L] variables
```

# Description

`clasiz` allows you to return the size used by a class available in the execution context (for example, table, local class, or global class). If the class is not available, the return is 0.  
  
The second argument can either be 1 or 2:   
\* If 1, the size currently used by the variables in the class is returned.   
\* If 2, the size allocated to the class is returned.

The result of the function is [Integer](4gl_integer.html).

# Associated errors

| Error | Description |
| --- | --- |
| 50 | The numeric argument is negative. |

# See also

[clalev](4gl_clalev.html), [clanam](4gl_clanam.html), [clanbs](4gl_clanbs.html), [clavar](4gl_clavar.html).

  

[Index](index.html)  [Home](getting-started_home.html)