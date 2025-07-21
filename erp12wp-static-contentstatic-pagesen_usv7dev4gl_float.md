[Index](index.html)  [Home](getting-started_home.html)

Float

This keyword declares a floating value with a precision that may depend on the hardware. It is therefore **strongly recommended** not to use this keyword anymore, and to replace it with [Decimal](4gl_decimal.html) variables.

# Syntax

```
Local    Float NAME
Local    Float NAME(DIMENSIONS)
Variable Float NAME(DIMENSIONS)
Value    Float NAME(DIMENSIONS)
Const    Float NAME(DIMENSIONS)
```

* `NAME` is the name of the variable declared
* `DIMENSIONS` can be:
  + A single numeric value DIM, meaning that you have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX2, where the index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma. For multiple dimension arrays, up to four dimensions are possible.

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling subprograms. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html) and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations declare the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted when the parenthesis is present. The dimension and index ranges are defined by the calling program.

# Example

```
# Direct declarations
Local Float CURRENCY_RATE, EOF_RATE : # Local floating point variables
Local Float WEIGHTING_MEASURES(1..12) : # An array of 12 floating point values

# A sub-program computing a result from floating points values 
Funprog COMPUTE_VALUE(MEASURES)
Variable Float MEASURES(,) : # A 2 dimensions matrix of floating point variables is sent as reference
...
End SEND_STATUS

# A sub-program storing floating point values
Subprog STORE_VALUES(VOLTAGE_MEASURES)
Value Float VOLTAGE_MEASURES(1..20) : # An array of 20 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

There is still a Global declaration variable that exists for variables that must be seen in the scope of a process execution, but its use is strongly discouraged.

# Implicit data type conversion

The Float data type will implicitly convert [Tinyint](../4gl/tinyint.md), [Shortint](../4gl/shortint.md), [Integer](../4gl/integer.md), [Double](../4gl/double.md) and [Decimal](../4gl/decimal.md) to a Floating point.. Note that precision may be lost in the type conversion as shown in the example below.

```
# Declare Float and assign value
Local Float MY_FLOAT              
MY_FLOAT = 42949672951       # Value retrieved =  4.29497e+10
```

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)