[Index](index.html)  [Home](getting-started_home.html)

Double

This keyword declares a double precision floating value with a precision that may depend on the hardware. It is therefore **strongly recommended** not to use this keyword anymore, and to replace it by [Decimal](4gl_decimal.html) variables.

# Syntax

```
Local    Double NAME
Local    Double NAME(DIMENSIONS)
Variable Double NAME(DIMENSIONS)
Value    Double NAME(DIMENSIONS)
Const    Double NAME(DIMENSIONS)
```

* `NAME` is the name of the variable declared.
* `DIMENSIONS` can be:
  + A single numeric value DIM, meaning that you have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX2, where the index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma. For multiple dimension arrays, up to four dimensions are possible.

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling subprograms. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html) and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations state the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted wherever the parenthesis is present. The dimension and index ranges are defined by the calling program.

# Example

```
# Direct declarations
Local Double CURRENCY_RATE, EOM_RATE : # Local double precision variables
Local Double WEIGHTING_MEASURES(1..12) : # An array of 12 double precision values

# A sub-program computing a result from double precision values 
Funprog COMPUTE_VALUE(MEASURES)
Variable Double MEASURES(,) : # A 2 dimensions matrix of double precision variables is sent as reference
...
End SEND_STATUS

# A sub-program storing floating point values
Subprog STORE_VALUES(VOLTAGE_MEASURES)
Value Float VOLTAGE_MEASURES(1..20) : # An array of 20 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

There is still a Global declaration variable that exists for variables that have to be seen in the scope of a process execution, but its use is strongly discouraged.

# Implicit data type conversion

The Double data type will implicitly convert [Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html) and [Decimal](4gl_decimal.html) to a Double precision value. Note that precision may be lost in the type conversion as shown in the example below.  
...

```
  
Local Double MY_DOUBLE             # Declare Double  
MY_DOUBLE = 42949672951            # MY_DOUBLE= 4.294967295e+10  

```

  
...

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)