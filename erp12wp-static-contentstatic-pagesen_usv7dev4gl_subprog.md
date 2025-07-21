[Index](index.html)  [Home](getting-started_home.html)

Subprog

`Subprog` is used to declare a routine that will be called by [Call](4gl_call.html). This function can accept a list of argument, and does not return a result.

# Syntax

```
   Subprog ROUTINE_NAME
   Subprog ROUTINE_NAME ( ARGUMENT_LIST)
```

* `ROUTINE_NAME` is the name of the routine. It must start with a letter, and can include letters, underscores, and digits. The letter is always uppercase.
* `ARGUMENT_LIST` is a list of `ARGUMENT` elements that can be empty. When more than one `ARGUMENT` is present, the separator used is the comma. All arguments must have different names.
* `ARGUMENT` is a variable name that will be filled by the corresponding argument given to the `func` syntax.

# Examples

```
# Converts a string to another string
# The initial string can be sent as a computed expression or as a variable (a copy is done in an INITIAL local variable)
Subprog CONVERT(INITIAL,FINAL)
Value Char INITIAL()  
Variable Char FINAL()
 ...
End

# Receives a matrix as input (the matrix cannot be modified), returns a numeric value
Subprog COMPUTE_DETERMINANT(MATRIX,DETERMINANT)
Const Decimal MATRIX(1..,1..,1..)
Variable Decimal DETERMINANT
 ...
End

# Receives an array of bytes, returns a short integer.
# As the declaration is done, nothing prevents the code to modify BINARY_FIELD (which has been passed as reference)
Funprog CHECKSUM(BINARY_FIELD,CHECKS)
Variable BINARY_FIELD(1..)
Variable Shortint CHECKS
...
End

# Receives a field of variable type and converts it to string
Funprog CONVERSION(FIELD,STRING_VALUE)
Variable STRING_VALUE()
 Case type(FIELD)
 ...
 Endcase
End

# Receives an array of strings, returns a clob
Funprog AGGREGATE(CHAR_ARRAY,RESULT)
Const Char CHAR_ARRAY()(..)
Variable Clbfile RESULT(2)
...
End

# Receives an array of integers, but will only consider the 10 first
# If the argument of the call was defined by Integer MYARRAY(-20..30),
# only MYARRAY(-20..-11) will be visible and mapped with INT_ARRAY(1..10)
Funprog COMPUTATION(INT_ARRAY,RESULT)
Const Integer INT_ARRAY()(1..10)
Variable Integer RESULT
...
End

# Receives an array of integers, with a shift in the index. The whole array is visible.
# If the argument of the call was defined by Integer MYARRAY(-20..30),
# MYARRAY(-20..30) will be visible and mapped with INT_ARRAY(1..51)
Funprog COMPUTATION(INT_ARRAY,RESULT)
Const Integer INT_ARRAY()(1..)
Variable Integer RESULT
...
End
```

The `Subprog` instruction is followed by the declaration of the argument in the argument list. These declarations are not mandatory (this allows to receive an argument of variable type). If they are present, they must be placed just after the `Subprog` declaration (in any order).

The declaration has the same syntax as usual variable declarations, except that:  
\* They have to be prefixed by one of the following keywords : [Variable](4gl_variable.html), [Const](4gl_const.html), or [Value](4gl_value.html).  
\* If arrays are declared, the dimensions can be omitted, and only commas will define the number of dimensions. The initial value will be by default 0. An initial index value can also be given with a syntax such as `2..` (if the index starts at 2). This means that a shift in the index will automatically be done. It is also possible to limit the number of elements that are seen in the `Funprog` by giving an end range in the argument declaration.  
\* The declaration type can be one of the following: ([Tinyint](4gl_tinyint.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), or [Instance](4gl_instance.html)).

The arguments declared are seen by the code of the `Subprog` as local variables. A `Subprog` ends with the following instruction: [End](4gl_end.html). No return value can be sent. The arguments sent in the call can be modified by the call.

The keyword used for the declaration of the argument defines how the argument is managed:  
\* [Value](4gl_value.html) means that the argument is copied in a local variable. Any modification made in the `Subprog` will not be sent back. This is the only possible mode if the argument is a computed expression. Transmitting large arrays with this method will consume time and memory.  
\* [Variable](4gl_variable.html) means that the argument is sent as a reference. A local variable that points on the argument is created. Any modification done changes the value of the calling argument.  
\* [Const](4gl_const.html) means that the argument is transmitted as a reference, with a read-only constraint. Any modification attempt in the `Subprog` will raise an error, which means that the argument cannot be modified in the function. This is the mode used when no type declaration has been made for an argument.

An argument sent in [Call](4gl_call.html) can have one of the following formats:  
 \* Any expression (this assumes that the argument is declared as a [Value](4gl_value.html)).  
 \* A single variable given by its name. If this variable is a multi-dimensional array, all the dimensions are transmitted by default. This is possible for arguments declared as [Const](4gl_const.html), [Variable](4gl_variable.html) or [Value](4gl_value.html).  
 \* A subrange of an array where ranges are given with the `RANGE_START`..`RANGE_END` syntax. This is also possible for arguments declared as [Const](4gl_const.html), [Variable](4gl_variable.html) or [Value](4gl_value.html).

The maximum length of the [Schar](4gl_schar.html), [Char](4gl_char.html), [Blbfile](4gl_blbfile.html), [Clbfile](4gl_clbfile.html) arguments does not have to be given. You just need to follow the name of the argument by `()` (before the dimension if you have any).

If the data type of an argument is not given, it will be considered by default as an [Integer](4gl_integer.html) when the calling argument is of type [TinyInt](4gl_tinyint.html), [Shortint](4gl_shortint.html), or [Integer](4gl_integer.html). For all the other types, the type remains the calling type.

For more information, see [Call](4gl_call.html).

# Comments

At execution time:

* The following information is inherited from the calling context:

  + The system variables and the global variables.
  + The opened tables.
  + The opened sequential files.
  + The default class lists.
  + The arguments transmitted.
* The [Local](4gl_local.html) [File](4gl_file.html) resources can be declared regardless of the declarations that have been done in the calling script (the [F] class will be insulated). If not re-declared, the class is inherited from the calling script.
* A function that creates a database transaction by [Trbegin](4gl_trbegin.html) must end it by [Commit](4gl_commit.html) or [Rollback](4gl_rollback.html) at the same level of [Call](4gl_call.html) nesting. An [End](4gl_end.html) without a proper transaction termination will trigger a [Rollback](4gl_rollback.html).
* If the calling script opens a database transaction, it is not possible to open a new transaction in the [Call](4gl_call.html), but every database operation done in the [Call](4gl_call.html) will be included in the transaction. Use [adxlog](4gl_adxlog.html) to detect if a transaction is already in progress.
* The following information is not transmitted:
  + The local class of the calling context.
  + The label associated with the [Onerrgo](4gl_onerrgo.html) error handling.

# Associated errors

| Error code | Description |
| --- | --- |
| 32 | Transaction started in another function/call nesting level. |
| 55 | The number of dimensions does not fit the parameter sent. |
| 61 | Already existing variable (two arguments have the same name). |

# See also

[Funprog](4gl_funprog.html), [func](4gl_func.html), [Value](4gl_value.html), [Variable](4gl_variable.html), [Const](4gl_const.html), [Call](4gl_call.html), [End](4gl_end.html).

  

[Index](index.html)  [Home](getting-started_home.html)