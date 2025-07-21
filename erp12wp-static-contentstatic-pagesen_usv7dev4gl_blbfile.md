[Index](index.html)  [Home](getting-started_home.html)

Blbfile

This keyword declares a binary large object (BLOB) variable.

# Syntax

```
Local    Blbfile NAME(LENGTH)
Local    Blbfile NAME(LENGTH)(DIMENSIONS)
Variable Blbfile NAME(LENGTH)(DIMENSIONS)
Value    Blbfile NAME(LENGTH)(DIMENSIONS)
Const    Blbfile NAME(LENGTH)(DIMENSIONS)
```

* `NAME` is the name of the variable declared.
* `LENGTH` is an integer value between 0 and 20.
* `DIMENSIONS` can be:
  + A single numeric value DIM (meaning that there is an array with an index range from 0 to DIM-1).
  + A range of numeric values INDEX1..INDEX2 (the index varies between INDEX1 and INDEX2).
  + Several indexes or index ranges separated by a comma (for multiple dimension arrays, up to four dimensions are possible)

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling sub-programs. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html), and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations state the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted wherever the parenthesis is present. The dimension and index ranges are defined by the calling program.

# Example

```
# Direct declarations
Local Blbfile MYPICTURE(2), A_PDF(4), EXCEL_DATA(5) : # Local Binary object variables
Local Blbfile MYPICTURE_ARRAY(2)(1..10) : # An array of 10 binary objects

# A sub-program sending pictures and returning a result
Funprog SEND_PICTURES(PICT)
Variable Blbfile PICT()(,) : # A 2 dimensions matrix of pictures is sent as references
...
End SEND_STATUS

# A sub-program storing pictures 
Subprog STORE_PICTURES(PICT)
Value Blbfile PICT()(1..3) : # An array of 3 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

The dimension given is used to size the variable per default. If a value exceeding this size is assigned, the execution engine will automatically re-size the variable.

The correspondence between the dimension and the default memory size allocated is provided in the following table:

| Dimension | Memory size |
| --- | --- |
| 0 | 1020 |
| 1 | 2044 |
| 2 | 4092 |
| 3 | 8188 |
| N | 1024\*2^N-4 |

There is still a global declaration variable that exists for variables that have to be seen in the scope of a process execution, but its use is strongly discouraged.

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Date](4gl_date.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)