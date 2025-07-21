[Index](index.html)  [Home](getting-started_home.html)

Schar

This keyword declares a character string with character coded on 1 byte (with a size limited to a value that cannot exceed 255 characters). It is strongly recommended to use [Char](4gl_char.html) declaration to avoid issues when dealing with texts that can contains Unicode characters.

# Syntax

```
Local    Schar NAME(LENGTH)
Local    Schar NAME(LENGTH)(DIMENSIONS)
Variable Schar NAME(LENGTH)(DIMENSIONS)
Value    Schar NAME(LENGTH)(DIMENSIONS)
Const    Schar NAME(LENGTH)(DIMENSIONS)
```

* `NAME` is the name of the variable declared.
* `LENGTH` is an integer value between 1 and 255 that defines the maximum length of the string.
* `DIMENSIONS` can be:
  + A single numeric value DIM, meaning that you have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX, where the index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma. For multiple dimension arrays, up to four dimensions are possible.

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling subprograms. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html) and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations state the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted whenever the parenthesis is present. The dimension and index ranges are defined by the calling program.

# Example

```
# Direct declarations
Local Schar MYTEXT(250) : # 250 max character string
Local Schar KEY_ARRAY(20)(1..10) : # An array of 10 character keys of 20 characters maximum.

# A sub-program sending a text and returning a result
Funprog SEND_TEXT(TEXT)
Variable Schar TEXT()(,) : # A 2 dimensions matrix of character strings is sent as references
...
End SEND_STATUS

# A sub-program storing texts
Subprog STORE_TEXTS(TEXT)
Value Schar TEXT()(1..3) : # An array of 3 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

The given dimension is the limit of the length allowed for the variable. Any attempt to assign a longer string, or to append characters over the limit defined by the length truncates the variable to the given dimension.

There is still a Global declaration variable that exists for variables that have to be seen in the scope of a process execution, but its use is strongly discouraged.

# See also

[Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Date](4gl_date.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)