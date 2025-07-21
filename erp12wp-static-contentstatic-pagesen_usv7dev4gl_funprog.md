[Index](index.html)  [Home](getting-started_home.html)

Funprog

Use `Funprog` to declare a function called by [func](4gl_func.html). This function can accept a list of arguments and has to return a result.

# Syntax

```
   Funprog FUNCTION_NAME
   Funprog FUNCTION_NAME ( ARGUMENT_LIST)
```

* `FUNCTION_NAME` is the name of the function. It must start with a letter, and can include letters, underscores, and digits. The letters are always uppercase.
* `ARGUMENT_LIST` is a list of `ARGUMENT` elements that can be empty. When more than one `ARGUMENT` is present, the separator used is the comma. All arguments must have different names.
* `ARGUMENT` is a variable name that is filled by the corresponding argument given to the `func` syntax.

# Examples

```
# Converts a string to another string, returns a status that can indicate that something got wrong
# The initial string can be sent as a computed expression or as a variable (a copy is done in an INITIAL local variable)
Funprog CONVERT(INITIAL,FINAL)
Value Char INITIAL()  
Variable Char FINAL()
 ...
End STATUS

# Receives a matrix as input (the matrix cannot be modified), returns a numeric value
Funprog COMPUTE_DETERMINANT(MATRIX)
Const Decimal MATRIX(1..,1..,1..)
Local Decimal DETERMINANT
 ...
End DETERMINANT

# Receives an array of bytes, returns a short integer.
# As the declaration is done, nothing prevents the code to modify BINARY_FIELD (which has been passed as reference)
Funprog CHECKSUM(BINARY_FIELD)
Variable BINARY_FIELD(1..)
Local Shortint CHECKSUM
...
End CHECKSUM

# Receives a field of variable type and converts it to string, returns a status if necessary
Funprog CONVERSION(FIELD,STRING_VALUE)
Variable STRING_VALUE()
 Case type(FIELD)
 ...
 Endcase
End STATUS

# No argument, returns the current date and time in LA
Funprog GET_TIME_IN_LA
Local Datetime COMPUTED_TIME
...
End COMPUTED_TIME

# Receives an array of strings, returns a clob
Funprog AGGREGATE(CHAR_ARRAY)
Const Char CHAR_ARRAY()(..)
Local Clbfile RESULT(2)
...
End RESULT

# Receives an array of integers, but will only consider the 10 first
# If the argument of the call was defined by Integer MYARRAY(-20..30),
# only MYARRAY(-20..-11) will be visible and mapped with INT_ARRAY(1..10)
Funprog COMPUTATION(INT_ARRAY)
Const Integer INT_ARRAY()(1..10)
Local Integer RESULT
...
End RESULT

# Receives an array of integers, with a shift in the index. The whole array is visible.
# If the argument of the call was defined by Integer MYARRAY(-20..30),
# MYARRAY(-20..30) will be visible and mapped with INT_ARRAY(1..51)
Funprog COMPUTATION(INT_ARRAY)
Const Integer INT_ARRAY()(1..)
Local Integer RESULT
...
End RESULT
```

The `Funprog` instruction is followed by the declaration of the argument present on the argument list. These declarations are not mandatory and allows you to receive an argument of variable type. However, if they are present, they must be placed just after the `Funprog` declaration (in any order).

**The declaration has the same syntax as usual variable declarations, except:**  
\* They have to be prefixed by one of the following keywords: [Variable](4gl_variable.html), [Const](4gl_const.html), or [Value](4gl_value.html).  
\* If arrays are declared, the dimensions can be omitted, and only commas define the number of dimensions. The initial value is by default 0. An initial index value can also be given with a syntax such as `2..` if the index starts at 2. This means that a shift in the index is automatically done. You can also limit the number of elements that are seen in the `Funprog` by giving an end range in the argument declaration.  
\* The declaration of type can be one of the usual ones ([Tinyint](4gl_tinyint.html), [Date](4gl_date.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Schar](4gl_schar.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), or [Instance](4gl_instance.html)).

The arguments declared are seen by the code of the `Funprog` as local variables. A `Funprog` ends with the following instruction: [End](4gl_end.html) `RETURN_VALUE`, where `RETURN_VALUE` is the expression of the value returned (it can be of any type).

**The keyword used for the declaration of the argument defines how the argument is managed:**  
\* [Value](4gl_value.html) means that the argument is copied in a local variable. Any modification made in the `Funprog` are not sent back. This is the only possible mode if the argument is a calculated expression. Transmitting large arrays with this method will consume time and memory.  
\* [Variable](4gl_variable.html) means that the argument is sent as a reference. A local variable that points on the argument is created. Any modification done changes the value of the calling argument.  
\* [Const](4gl_const.html) means that the argument is transmitted as a reference, with a read-only constraint. Any modification attempt in the `Funprog` will create an error, which means that the argument cannot be modified in the function. This is the mode used when no type declaration is made for an argument.

**An argument sent in [func](4gl_func.html) can have one of the following formats:**  
 \* Any expression, which assumes that the argument is declared as [Value](4gl_value.html).  
 \* A single variable given by its name. If this variable is a multidimensional array, all the dimensions are transmitted by default. This is possible for arguments declared as [Const](4gl_const.html), [Variable](4gl_variable.html), or [Value](4gl_value.html).  
 \* A subrange of an array where ranges are given with the `RANGE_START`..`RANGE_END` syntax. This is also possible for arguments declared as [Const](4gl_const.html), [Variable](4gl_variable.html), or [Value](4gl_value.html).

The maximum length of the [Schar](4gl_schar.html), [Char](4gl_char.html), [Blbfile](4gl_blbfile.html), and [Clbfile](4gl_clbfile.html) arguments are not given. You just need to follow the name of the argument by `()` (before the dimension, if you have some).

If the data type of an argument is not given, it is considered by default as an [Integer](4gl_integer.html) if the calling argument is of type [TinyInt](4gl_tinyint.html), [Shortint](4gl_shortint.html), or [Integer](4gl_integer.html). For all other types, the type remains the calling type.

For more information, see the [func](4gl_func.html) documentation.

# Comments

At execution time:

* The following information is inherited from a calling context:
  + The system variables and the global variables.
  + The opened tables.
  + The opened sequential files.
  + The default class lists.
  + The arguments transmitted.
* The [Local](4gl_local.html) [File](4gl_file.html) resources can be declared regardless of the declarations that have been done in the calling script (the [F] class is insulated). If not redeclared, the class is inherited from a calling script.
* A function that creates a database transaction by [Trbegin](4gl_trbegin.html) must end it by [Commit](4gl_commit.html) or [Rollback](4gl_rollback.html) at the same level of [func](4gl_func.html) nesting. An [End](4gl_end.html) without a proper transaction termination triggers a [Rollback](4gl_rollback.html).
* If the calling script has opened a database transaction, it is not possible to open a new transaction in the [func](4gl_func.html), but every database operation done in the [func](4gl_func.html) is included in the transaction. Use [adxlog](4gl_adxlog.html) to detect if a transaction is already in progress.
* The following information is not transmitted:
  + The local class of the calling context.
  + The label associated with the [Onerrgo](4gl_onerrgo.html) error handling.

# Associated errors

| Error code | Description |
| --- | --- |
| 32 | Transaction started in another func/call nesting level. |
| 55 | The number of dimensions does not fit the parameter sent. |
| 61 | Already an existing variable (two arguments have the same name). |

# See also

[func](4gl_func.html), [Value](4gl_value.html), [Variable](4gl_variable.html), [Const](4gl_const.html), [Call](4gl_call.html), [End](4gl_end.html).

  

[Index](index.html)  [Home](getting-started_home.html)