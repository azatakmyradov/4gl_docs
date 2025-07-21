[Index](index.html)  [Home](getting-started_home.html)

Shortint

This keyword declares an integer variable where the value is within the range from -32768 to 32767.

# Syntax

```
Local    Shortint NAME
Local    Shortint NAME(DIMENSIONS)
Variable Shortint NAME(DIMENSIONS)
Value    Shortint NAME(DIMENSIONS)
Const    Shortint NAME(DIMENSIONS)
```

* `NAME` is the name of the variable declared.
* `DIMENSIONS` can be:
  + A single numeric value DIM, meaning that we have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX2, where the index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma. For multiple dimension arrays, up to four dimensions are possible.

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling subprograms. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html) and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations state the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted when the parenthesis is present. The dimension and index ranges are defined by the calling program.

# Example

```
# Direct declarations
Local Shortint MYCHOICE : # Local short integer variable
Local Shortint VALUES(1..1024), CURRENT_VAL : # An array of 1024 short integer values and another variable

# A sub-program sending short integers and returning a result
Funprog SEND_PICTURES(MYINT)
Variable Shortint MYINT(,) : # A 2 dimensions matrix of short integers is sent as references
...
End SEND_STATUS

# A sub-program storing short integers
Subprog STORE_VALUES(LEVEL)
Value Shortint LEVEL(1..20) : # An array of 20 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

There is still a Global declaration variable that exists for variables that must be seen in the scope of a process execution, but its use is strongly discouraged.

# Implicit data type conversion

The Shortint data type will implicitly convert [Tinyint](4gl_tinyint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html) and [Decimal](4gl_decimal.html) to a Shortint. For Decimal, Float and Double precision numbers the decimal portion of the number is truncated then the integer portion is assigned to the Shortint under the constraints that the integer portion of Shortint is limited to -32768 to 32767   
...

```
  
Local Shortint MY_SHORTINT        # Declare Shortint   
MY_SHORTINT = 2000.7             # Float, Double or Decimal conversion - MY_SHORTINT = 2000  

```

  
...

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Date](4gl_date.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)