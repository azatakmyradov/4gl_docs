[Index](index.html)  [Home](getting-started_home.html)

Uuident

This keyword declares a [UUID](4gl_glossary-uuid.html) variable.

# Syntax

```
Local    Uuident NAME
Local    Uuident NAME(DIMENSIONS)
Variable Uuident NAME(DIMENSIONS)
Value    Uuident NAME(DIMENSIONS)
Const    Uuident NAME(DIMENSIONS)
```

* `NAME` is the name of the variable declared
* `LENGTH` is an integer value between 0 and 20.
* `DIMENSIONS` can be:
  + a single numeric value 'DIM' (meaning that we have an array with an index range from '0' to 'DIM-1')
  + a range of numeric values 'INDEX1'..'INDEX2' (the index varies between 'INDEX1' and 'INDEX2')
  + several indexes or index ranges separated by a comma (for multiple dimension arrays, up to 4 dimensions are possible).

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling sub-programs. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html), [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html) and [Value](4gl_value.html) declarations state the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted as soon as the parenthesis are present (the dimension and index ranges are defined by the calling program).

# Example

```
# Direct declarations
Local Uuident MYUUID, USERUUID, ITEMUUID : # Local UUID variables
Local Uuident MYUUID_ARRAY(1..10) : # An array of 10 UUIDs

# A sub-program sending UUID and returning a result
Funprog SEND_PICTURES(MYUUID)
Variable Uuident MYUUID(,) : # A 2 dimensions matrix of UUID is sent as references
...
End SEND_STATUS

# A sub-program storing UUID
Subprog STORE_UUIDS(UUID)
Value Uuident UUID(1..3) : # An array of 3 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

There is still a [Global](4gl_global.html) declaration variable that exists for variables that have to be seen in the scope of a process execution, but its use is strongly discouraged.

"UUID" class properties are declared with the `AUUID` data type. A default "UUID" property, called `AUUID`, is automatically added to the class description when a class is created. `Uuident` declarations are rarely used.

# Implicit data type conversion

There are no implicit type conversions for Uuident. All type conversions must be explicitly specified in the script.

# See also

[UUID](4gl_glossary-uuid.html), [Nulluuid](4gl_nulluuid.html), [Touuid](4gl_touuid.html), [Getuuid](4gl_getuuid.html), [Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Date](4gl_date.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)