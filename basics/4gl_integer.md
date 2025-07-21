[Index](index.html)  [Home](getting-started_home.html)

Integer

This keyword declares an integer variable where the value is within the range from -2^31 to 2^31-1.

# Syntax

```
Local    Integer NAME
Local    Integer NAME(DIMENSIONS)
Variable Integer NAME(DIMENSIONS)
Value    Integer NAME(DIMENSIONS)
Const    Integer NAME(DIMENSIONS)
```

* `NAME` is the name of the variable declared.
* `DIMENSIONS` can be:
  + A single numeric value DIM, meaning that you have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX2 where the index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma for multiple dimension arrays, and up to four dimensions.

You can do several variable declarations on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling subprograms. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html) and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations state the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, you can omit the dimensions and the index ranges when the parenthesis are present. The calling program defines the dimension and index ranges.

# Example

```
# Direct declarations
Local Integer MYDISTANCE, MYAGE : # Local integer variables
Local Integer VALUES(1..1024) : # An array of 1024 integer values

# A sub-program sending integers and returning a result
Funprog SEND_INTEGERS(MYINT)
Variable Integer MYINT(,) : # A 2 dimensions matrix of integers is sent as reference
...
End SEND_STATUS

# A sub-program storing integers
Subprog STORE_VALUES(LEVEL)
Value Integer LEVEL(1..20) : # An array of 20 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

There is still a Global declaration variable that exists for variables that must be seen in the scope of a process execution, but its use is strongly discouraged.

# Implicit data type conversion

The Integer data type will implicitly convert [Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Float](4gl_float.html), [Double](4gl_double.html) and [Decimal](4gl_decimal.html) to an Integer. For Decimal, Float and Double precision numbers the decimal portion of the number is truncated then the integer portion is assigned to the Integer under the constraints that the integer portion of Integer is limited to -2^31 to 2^31-1.

...

```
  
Local Integer MY_INTEGER         # Declare Integer  
MY_INTEGER = 78956.23            # Float, Double or Decimal conversion - MY_INTEGER = 78956  

```

  
...

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)