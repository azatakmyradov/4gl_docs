[Index](index.html)  [Home](getting-started_home.html)

Global

Global variables are variables that have a global visibility and duration scope in a Sage X3 process.

They are created in the [V] class. Once created, they will persist during the entire life of the Sage X3 process, unless they are destroyed by the [Kill](4gl_kill.html) instruction.

It is recommended to avoid using this declaration and to replace it with a [Local](4gl_local.html) declaration because this variable is a barrier used to produce reentry code.

In previous versions of Sage X3, global variables were used to access optimization buffers for parameters. This has been replaced by the [context structure](developer-guide_context.html) even if a default context global pointer still exists (`[V]GACTX`).

The global variable is still used to define [constants](developer-guide_constants.html) in order to avoid using literal or numeric constants in the code (for example, status values sent back by some instruction).

# Syntax

```
Global DECLARATION1 VARIABLE(DIMENSIONS)
Global DECLARATION2 VARIABLE(SIZE)(DIMENSIONS)
Global Instance VARIABLE Using CLASS
Global Instance VARIABLE(DIMENSIONS) Using CLASS
Default Global
```

* `DECLARATION1` may be one of the following keywords: [Tinyint](4gl_tinyint.html), [Libelle](4gl_libelle.html), [Date](4gl_date.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Datetime](4gl_datetime.html), or [Uuident](4gl_uuident.html).
* `DECLARATION2` may be one of the following keywords: [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), or [Blbfile](4gl_blbfile.html).
* `SIZE` is a numeric value.
* `DIMENSIONS` can be:
  + A single numeric value 'DIM' (where there is an array with an index range from 0 to DIM-1).
  + A range of numeric values INDEX1..INDEX2 (the index varies between INDEX1 and INDEX2).
  + Several indexes or index ranges separated by a comma (for multiple dimension arrays, up to four dimensions are possible).
* `CLASS` is a class code (refers to the [class](workbench-reference_class-management.html) or [representation](workbench-reference_representation-management.html) dictionary).

'Default Global' establishes that a declaration without a `Global` or `Local` keyword will be considered global. This type of syntax should also be avoided because it makes the scope of the created variable ambiguous.

# Examples

```
Global Char CONSTANT_STRING(100)
Global Instance MYCONTEXT Using C_MYGLOBCLASS
Global TinyInt STATUS_ARRAY(1..20)
```

# See also

[Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Libelle](4gl_libelle.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)