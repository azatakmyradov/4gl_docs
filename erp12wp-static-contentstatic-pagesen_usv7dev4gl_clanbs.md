[Index](index.html)  [Home](getting-started_home.html)

Clanbs

`clanbs` allows you to know the number of variables used by a class.

# Syntax

```
   clanbs(CLASS_DESCRIPTION,OPTION)
   clanbs(NUMERIC_EXPRESSION,OPTION)
```

* `CLASS_DESCRIPTION` is a class description with the `[ABBR]` syntax, where `ABBR` is the abbreviation of a class. Note, for classes of type file use `[F:ABBR]`
* `OPTION` is an integer expression returning 1 or 2.
* `NUMERIC_EXPRESSION` refers to the slot number for the class. This can be seen in the debugger, but should be considered internal.

# Examples

```
  # Check the number of variables used by the local variable class
  NUMBER1=clanbs([L],1) : # The number of variables currently present in [L] variable class.
  NUMBER2=clanbs([L],2) : # The number of variables slots currently allocated for [L] variables
```

# Description

`clanbs` allows you to return the number of variable slots used by a class available in the execution context (for example, table, local class, or global class). If the class is not available an [errn](4gl_errn.html)=10 (type not compatible) is returned.  
  
The second argument can either be 1 or 2:   
\* If 1, the number of variables currently used for variables in the class is returned.   
\* If 2, the size allocated to variable entries for the class is returned.

The result of the function is [Integer](4gl_integer.html).

# Associated errors

| Error | Description |
| --- | --- |
| 10 | Type incompatibility |
| 50 | The numeric argument is negative. |

# See also

[clalev](4gl_clalev.html), [clanam](4gl_clanam.html), [clasiz](4gl_clasiz.html), [clavar](4gl_clavar.html), [errn](4gl_errn.html), [onerrgo](4gl_onerrgo.html).

  

[Index](index.html)  [Home](getting-started_home.html)