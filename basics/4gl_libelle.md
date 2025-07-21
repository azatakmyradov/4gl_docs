[Index](index.html)  [Home](getting-started_home.html)

Libelle

This keyword declares an integer variable where the value is within the range from 0 to 255.  
This declaration is deprecated and should be replaced by [Tinyint](4gl_tinyint.html).

# Syntax

```
Local    Libelle NAME(LENGTH)
Local    Libelle NAME(LENGTH)(DIMENSIONS)
Variable Libelle NAME(LENGTH)(DIMENSIONS)
Value    Libelle NAME(LENGTH)(DIMENSIONS)
Const    Libelle NAME(LENGTH)(DIMENSIONS)
```

* `NAME` is the name of the variable declared.
* `LENGTH` is an integer value between 0 and 20.
* `DIMENSIONS` can be:
  + A single numeric value DIM, meaning that we have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX2, where the index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma. For multiple dimension arrays, up to four dimensions are possible.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling subprograms. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html) and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations state the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted when the parenthesis is present. The dimension and index ranges are defined by the calling program.

# Example

```
# Direct declarations
Local Libelle MYCHOICE : # Local tiny integer variable
Local Libelle BYTES_ARRAY(1..1024) : # An array of 1024 byte values

# A sub-program sending tiny integers and returning a result
Funprog SEND_BYTES(MYCHOICE)
Variable Libelle MYCHOICE()(,) : # A 2 dimensions matrix of tiny integers is sent as references
...
End SEND_STATUS

# A sub-program storing tiny integers
Subprog STORE_BYTES(MYCHOICE)
Value Libelle MYCHOICE()(1..3) : # An array of 3 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

There is still a [Global](4gl_global.html) declaration variable that exists for variables that have to be seen in the scope of a process execution, but its use is strongly discouraged.

`Libelle` class properties are declared with the `L` data type associated with local menus (this handles enumerations).

# See also

[Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Date](4gl_date.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)