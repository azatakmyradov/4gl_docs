[Index](index.html)  [Home](getting-started_home.html)

Local

This keyword is used as a prefix to declare local variables. Local variables have a duration and visibility scope limited to a [Call](4gl_call.html), [fmet](4gl_fmet.html), and [func](4gl_func.html) call.

A local variable is created in the [L] class. Once created, it will persist until the [End](4gl_end.html) instruction is encountered, or if it is destroyed by the use of the [Kill](4gl_kill.html) instruction. The local variables are shared with code that is called by a [Gosub](4gl_gosub.html) instruction.

# Syntax

```
Local DECLARATION1 VARIABLE(DIMENSIONS)
Local DECLARATION2 VARIABLE(SIZE)(DIMENSIONS)
Local Instance VARIABLE Using CLASS
Local Instance VARIABLE(DIMENSIONS) Using CLASS
Default Local
```

* `DECLARATION1` may be one of the following keywords: [Tinyint](4gl_tinyint.html), [Libelle](4gl_libelle.html), [Date](4gl_date.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Datetime](4gl_datetime.html), or [Uuident](4gl_uuident.html).
* `DECLARATION2` may be one of the following keywords: [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), or [Blbfile](4gl_blbfile.html).
* `SIZE` is a numeric value.
* `DIMENSIONS` can be:
  + A single numeric value DIM, meaning that we have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX2, where the index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma. For multiple dimension arrays, up to 4 dimensions are possible.
* `CLASS` is a class code, which refers to the [class](workbench-reference_class-management.html) or [representation](workbench-reference_representation-management.html) dictionary.

Default `Local` is a declaration that sets up the fact that a declaration without [Global](4gl_global.html) or Local Keyword will be considered as global. This type of syntax should also be avoided because it makes ambiguous the scope of the created variable.

# Examples

```
Local Char TEMPORARY_STRING(100)
Local Instance MYORDER Using C_ORDER
Local TinyInt BYTES_BUFFER(1..1024)
```

# See also

[Global](4gl_global.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Libelle](4gl_libelle.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)