[Index](index.html)  [Home](getting-started_home.html)

Dim

`dim` returns the dimensions of a variable.

# Syntax

```
   dim(VARIABLE_NAME)
   dim(VARIABLE_NAME,INTEGER_EXPR)
```

* `VARIABLE_NAME` is the name of a variable that can include a class description.
* `INTEGER_EXPRESSION` is an expression that returns an integer value.

# Examples

```

  # Checks if a column exists
  Local File MY_TABLE [MYT]
  If dim([MYT]CREDATTIM)>0
    [MYT]CREDATTIM=gdatetime$
  Endif

  # Let's declare a multi-dimensional array of strings
  Local Char STRING_ARRAYS(8) (5..16,3,1..4)
  Local Integer I, NBDIM,DIMENSIONS(1..3),FIRST_INDEX(1..3)
  NBDIM=dim(STRING_ARRAYS,0) : # Returns 3
  For I=1 to NBDIM
    DIMENSIONS(I)=dim(STRING_ARRAYS,I)
    FIRST_INDEX(I)=dim(STRING_ARRAYS,-I)
  Next I

  # DIMENSIONS will have the following values:  12, 3, 4
  # FIRST_INDEX will have the following values: 5,  0, 1
```

# Description

If only a parameter is given, `dim` returns the first dimension of a variable (for example, the number of elements of a single array, or the number of rows in a double dimension array).

If the variable does not exist, `dim` returns -1.

If a second parameter `INTEGER_EXPR` is given, the result depends on the value given:  
\* If 0, it returns the number of dimensions.  
\* If `N` positive (`N` between 1 and 4), `dim` returns the number of elements of the Nth dimension of the variable.  
\* If `N` is negative `N` between -4 and -1), `dim` returns the value of the first index for the given dimension.

The type of the result is [Integer](4gl_integer.html).

# Comments

If the variable corresponds to an unlimited array, the value returned is always 32767. It is therefore better to use [maxtab](4gl_maxtab.html) to limit the index values on such an array.

See the following example:

```
 Local Instance MY_ORDER With C_SALESORDER
 ...
 # Assign the quantity to 1 for all the lines of the sales order
 For I=1 to maxtab(MY_ORDER.LINES)
   If MYORDER.LINES(I)<>null
     MYORDER.LINES(I).QTY=1
   Endif
 Next I
```

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The second argument is not numeric. |
| 50 | The first argument is not a variable name, or the second argument is not in the range [-4,4]. |

# See also

[type](4gl_type.html), [maxtab](4gl_maxtab.html).

  

[Index](index.html)  [Home](getting-started_home.html)