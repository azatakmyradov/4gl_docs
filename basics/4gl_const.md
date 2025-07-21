[Index](index.html)  [Home](getting-started_home.html)

Const

`Const` is a keyword used after a [Subprog](4gl_subprog.html) or a [Func](4gl_func.html) declaration to define the type of arguments transmitted to the called code.

The declaration of the arguments is not mandatory and allows you to transmit parameters with a variable type to subprograms. If they are present, the declarations must be placed just after the [Subprog](4gl_subprog.html) or [Func](4gl_func.html) declaration.

`Const` arguments are transmitted through pointers, but modifications of the variable are not allowed as they are in read-only mode. The consequence of the pointer transmission is that no constants or expressions are allowed in the corresponding [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html): it would create an error at execution time.

# Syntax

```
Const DECLARATION1 NAME(DIMENSIONS)
Const DECLARATION2 NAME(SIZE)(DIMENSIONS)
Const Instance NAME Using CLASS
Const Instance NAME(DIMENSIONS) Using CLASS
```

* `DECLARATION1` may be one of the following keywords: [Tinyint](4gl_tinyint.html), [Libelle](4gl_libelle.html), [Date](4gl_date.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Datetime](4gl_datetime.html), or [Uuident](4gl_uuident.html).
* `DECLARATION2` may be one of the following keywords: [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), or [Blbfile](4gl_blbfile.html).
* `NAME` is the name of the declared variable.
* `LENGTH` is an integer value between 0 and 20.
* `DIMENSIONS` can be:
  + A single numeric value DIM (meaning that there is an array with an index range from 0 to DIM-1).
  + A range of numeric values INDEX1..INDEX2 (the index varies between INDEX1 and INDEX2).
  + Several indexes or index ranges separated by a comma (for multiple dimension arrays, up to four dimensions are possible).
* `CLASS` is a class code (refers to the [class](workbench-reference_class-management.html) or [representation](workbench-reference_representation-management.html) dictionary).

The dimensions and the index ranges can be omitted wherever the parenthesis is present. The dimension and index ranges are defined by the calling program. Additionally, the first range of an index can be given alone, and the total number of values is defined by the calling program.

# Examples

```
# Example of declarations
Subprog STORE_VALUES(KEYS,VALUES,IDENTIFIER,GLOBAL_STATUS)
Const Char KEYS(20)(1..) : # Array of 20 characters starting at index 1
Const Decimal VALUES(,) : # 2 dimensions matrix of decimals
Const Char IDENTIFIER()
Const Integer GLOBAL_STATUS : # Integer

# First example that brings to an error
Call MY_ERROR(123) : # Generates an error : constants or expressions are not allowed
....
End
Subprog MY_ERROR(MYVALUE)
Const Decimal MYVALUE
...
End

# Second example that brings to an error
Local Decimal PRICE
PRICE=123
Call OTHER_ERROR(PRICE)
....
End
Subprog OTHER_ERROR(MYVALUE)
Const Decimal MYVALUE
...
MYVALUE=124 : # Generates an error : the variable is read-only
...
End
```

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Tinyint](4gl_tinyint.html), [Libelle](4gl_libelle.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)