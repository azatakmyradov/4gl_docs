[Index](index.html)  [Home](getting-started_home.html)

Datetime

This keyword declares a DateTime variable.

# Syntax

```
Local    Datetime NAME
Local    Datetime NAME(DIMENSIONS)
Variable Datetime NAME(DIMENSIONS)
Value    Datetime NAME(DIMENSIONS)
Const    Datetime NAME(DIMENSIONS)
```

* NAME is the name of the variable declared
* LENGTH is an integer value between 0 and 20.
* DIMENSIONS can be:
  + a single numeric value DIM (meaning that we have an array with an index range from 0 to DIM-1)
  + a range of numeric values INDEX1..INDEX2 (the index varies between INDEX1 and INDEX2)
  + several indexes or index ranges separated by a comma (for multiple dimension arrays, up to 4 dimensions are possible)

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling sub-programs. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html), [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html) and [Value](4gl_value.html) declarations declare the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted as soon as the parenthesis are present (the dimension and index ranges are defined by the calling program).

# Example

```
# Direct declarations
Local Datetime NOW : # Local datetime variable
Local Datetime EVENTS_TIME(1..60), CURRENT_DATETILE : # An array of 60 datetime values and another variable

# A sub-program sending date times and returning a result
Funprog SEND_TIMING(MYDATETIME)
Variable Datetime MYDATETIME(,) : # A 2 dimensions matrix of datetime values is sent as reference
...
End SEND_STATUS

# A sub-program storing dates
Subprog STORE_VALUES(EVENT_DATETIME)
Value Datetime EVENT_DATETIME(1..5) : # An array of 5 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

There is still a Global declaration variable that exists for variables that have to be seen in the scope of a process execution, but its use is strongly discouraged.

Datetime properties are declared with the `ADATIM` data type in the data dictionary.

Every table has `CREDATTIM` and `UPDDATTIM` system columns. These columns are automatically added when the table is created and they are automatically filled by the framework when records are created and updated. Therefore, `DateTime` declarations are rarely used.

# Implicit data type conversion

There are no implicit type conversions for datetime. All type conversions must be explicitly specified in the script.

# See also

[Datetime](4gl_glossary-datetime.html), [datetime$](4gl_datetime$.html), [gdatetime$](4gl_gdatetime$.html) [Global](4gl_global.html) [Local](4gl_local.html) [Variable](4gl_variable.html) [Value](4gl_value.html) [Const](4gl_const.html) [Tinyint](4gl_tinyint.html) [Shortint](4gl_shortint.html) [Date](4gl_date.html) [Integer](4gl_integer.html) [Float](4gl_float.html) [Double](4gl_double.html) [Decimal](4gl_decimal.html) [Char](4gl_char.html) [Clbfile](4gl_clbfile.html) [Blbfile](4gl_blbfile.html) [Uuident](4gl_uuident.html) [Instance](4gl_instance.html)

  

[Index](index.html)  [Home](getting-started_home.html)