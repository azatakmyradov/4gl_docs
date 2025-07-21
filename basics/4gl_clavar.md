[Index](index.html)  [Home](getting-started_home.html)

Clavar

`clavar` returns the name of the variables present in a class.

# Syntax

```
   clavar(CLASS_DESCRIPTION,RANK)
   clavar(NUMERIC_EXPRESSION,RANK)
```

* `CLASS_DESCRIPTION` is a class description with the `[ABBR]` syntax, where `ABBR` is the abbreviation of a class. Note, of a class of type table use `[F:ABBR]`
* `RANK` is an index of the column in 'clavar'. The column names are listed in alphabetical order.
* `NUMERIC_EXPRESSION` refers to the slot number for the class. This can be seen in the debugger, but should be considered internal.

# Examples

```
  # Example 1
  # Get the name of the first local variable
    VARNAME=clavar([L],1)

  # Example 2
  # List the global variables available in a given class. Classname is in the form [F:ABBR], for example.
  Subprog VARLIST(CLASSNAME,NUMBER, VARNAME, VARTYPE)
  Value Char CLASSNAME()
  Variable Integer NUMBER
  Variable Char VARNAME()(1..)
  Variable Integer VARTYPE(1..)

  Local Integer I,J,MAXCLASS

    MAXCLASS=200

  # Search if the class exists
    For I=1 to MAXCLASS
      Break (clanam(I)=CLASSNAME) : # End the loop if the class name is found
    Next I

  # If I is greater than MAXCLASS, the class was not found
    If I>MAXCLASS
      NUMBER=0
      End
    Endif

  # Otherwise, get all the variable names, and compute their type
    NUMBER=clanbs(I,1)
    For J=1 to min(dim(VARNAME),dim(VARTYPE),NUMBER) : # To prevent an out of index
      VARNAME(J)=clavar(I,J)
      VARTYPE(J)=evalue("type("+CLASSNAME+VARNAME(J)+")")
    Next J

  End
```

# Description

`clavar(classname,N)` returns variable name of the Nth variable in a class. If the variable name does not exist in the class for the Nth variable the return is an empty string. If the classname is not available in the clavar then [errn](4gl_errn.html)=10 is returned (Type incompatible)

The result of the function is [Char](4gl_char.html).

# Associated errors

| Error | Description |
| --- | --- |
| 10 | Type incompatible |
| 50 | The numeric argument is negative. |

# See also

[clalev](4gl_clalev.html), [clanam](4gl_clanam.html), [clanbs](4gl_clanbs.html), [clasiz](4gl_clasiz.html), [errn](4gl_errn.html), [onerrgo](4gl_onerrgo.html)

  

[Index](index.html)  [Home](getting-started_home.html)