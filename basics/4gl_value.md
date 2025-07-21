[Index](index.html)  [Home](getting-started_home.html)

Value

`Value` is a keyword used after a [Subprog](4gl_subprog.html) or a [Func](4gl_func.html) declaration, to define the type of arguments transmitted to the called code.

The declaration of the arguments is not mandatory. This allows to transmit parameters with a variable type to subprograms. If they are present, the declarations must be placed just after the [Subprog](4gl_subprog.html) or [Func](4gl_func.html) declaration.

`Value` arguments as copied in the local variable class are associated with the call level nesting. Any modification done on the arguments is not transmitted to the variable transmitted in the call.

# Syntax

```
Value DECLARATION1 NAME(DIMENSIONS)
Value DECLARATION2 NAME(SIZE)(DIMENSIONS)
Value Instance NAME Using CLASS
Value Instance NAME(DIMENSIONS) Using CLASS
```

* `DECLARATION1` can be one of the following keywords: [Tinyint](4gl_tinyint.html), [Libelle](4gl_libelle.html), [Date](4gl_date.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Datetime](4gl_datetime.html), or [Uuident](4gl_uuident.html).
* `DECLARATION2` can be one of the following keywords: [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), or [Blbfile](4gl_blbfile.html).
* `NAME` is the name of the variable declared.
* `LENGTH` is an integer value between 0 and 20.
* `DIMENSIONS` can be:
  + A single numeric value DIM, meaning that you have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX2, where the index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma. For multiple dimension arrays, up to four dimensions are possible.
* `CLASS` is a class code , which refers to the [class](workbench-reference_class-management.html) or [representation](workbench-reference_representation-management.html) dictionary.

The dimensions and the index ranges can be omitted wherever the parenthesis is present. The dimension and index ranges are defined by the calling program. Also, the first range of an index can only be given. The total number of values is defined by the calling program.

# Examples

```
Subprog STORE_VALUES(KEYS,VALUES,IDENTIFIER,GLOBAL_STATUS)
Value Char KEYS(20)(1..) : # Array of 20 characters starting at index 1
Value Decimal VALUES(,) : # 2 dimensions matrix of decimals
Value Char IDENTIFIER()
Value Integer GLOBAL_STATUS : # Integer
```

# Comments

Transmitting large variables declared with [Value](4gl_value.html) can be harmful in terms of performance. If the values transmitted must be protected from modifications, it is also possible to use [Const](4gl_const.html) for the declarations. The variables transmitted will then be in read-only mode.

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Libelle](4gl_libelle.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)