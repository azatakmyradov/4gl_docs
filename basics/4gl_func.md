[Index](index.html)  [Home](getting-started_home.html)

Func

Use this function to [Call](4gl_call.html) a subroutine executed with its own local variables class that returns a value. Parameters can be transmitted as values or as references; so that the parameters transmitted by reference can be modified by the subroutine.

# Syntax

```
func SUBPROGRAM
func LIBRARY.SUBPROGRAM
func SUBPROGRAM(ARGUMENT_LIST)
func LIBRARY.SUBPROGRAM(ARGUMENT_LIST)
func =EXPRESSION_SUBPROGRAM
func =EXPRESSION_SUBPROGRAM with(ARGUMENT_LIST)
```

* `SUBPROGRAM` is the name of the routine declared by the [Funprog](4gl_funprog.html) keyword.
* `LIBRARY` is the name of the script that contains the code of the routine called.
* `ARGUMENT_LIST` is a list of expressions, variables, or subarrays that can be empty. The elements are separated by commas.
* `EXPRESSION_SUBPROGRAM` is an alphanumeric expression whose evaluation returns the code of the routine called. The routine can be preceded by the library name with the nformat `LIBRARY.SUBPROGRAM`.

# Examples

```
  # Call of a routine that increments a value
  Local Integer I
  I=314 : I=func ADD_ONE(I) : # I contains now 315
  ...

  Funprog ADD_ONE(J)
  Variable Integer J : # Can be value, variable, or constant
  End J+1


  # Call of a function with parameters in another process
  Local Integer MATRIX(1..10,1..20,1..30)
  ...
  # Only a sub-array is transmitted (even if it is sent as a reference)
  RESULT = func MATRIC_LIBRARY.COMPUTE_SUM(MATRIX(5..6,2..4,1..20))
  ...
  # In the MATRIX_LIBRARY script, the arguments are
  Funprog COMPUTE_SUM(MATRIX,RESULT)
  Const Integer MATRIX(,,)
  End sum(MATRIX)

  # Example of subprogram with a variable type of argument
  Local Char MY_STRING(20),TEXT(10)
  MY_STRING="abcdefghijklmnopqrst"

  I = func RETURN_TYPE(pi,TEXT)          : # Will return 7 (decimal) and "3.14159265"
  I = func RETURN_TYPE([1/1/2013],TEXT)  : # Will return 3 (date) and "01/01/2013"
  I = func RETURN_TYPE(100,TEXT)         : # Will return 4 (integer) and "100"
  I = func RETURN_TYPE("text sent",TEXT) : # Will return 523 (clob) and "text sent"
  I = func RETURN_TYPE(MY_STRING,TEXT)   : # Will return 20 (string 10) and "abcdefghij"
  End

  # A subprogram that returns the data type of the argument
  Funprog RETURN_TYPE(ARGUMENT,TEXT)
  Variable Char TEXT()
  TEXT=num$(ARGUMENT)
  End type(ARGUMENT)
```

# Description

`func` executes a subroutine with possible parameters. The calling code ends its execution when an [End](4gl_end.html) instruction is encountered. The result of `func` is used in the calling instruction and the execution continues in sequence.

A `func` performed without specifying a script is done in the same script.

# Comments

## Variable scope

**During a `func`, the following information is saved:**  
\* Local Variables.  
\* The tables declared with the current values of the corresponding [F] and [G] classes.  
\* The group of the default class lists (outside of any local class).

**During a `func`, the following information is lost:**  
\* The tables reopened with the same abbreviation in the subroutine.  
\* The label associated with [Onerrgo](4gl_onerrgo.html) is not saved when passing to a subroutine even if this is performed in the same process.

When executing a `func`, a class of local variables is created with the subroutine, abbreviated [L]. This local class becomes the default class because the local class with the calling process is no longer accessible. When you return to the process, you will find the default local class which existed before the call.

The local variables and all the resources opened with [Local](4gl_local.html) keyword in the subroutine are lost after the execution of the call.

## Parameters

The number of parameters transmitted in the `func` must correspond to the number of parameters declared in the [Funprog](4gl_funprog.html) instruction.

The parameters of the [Funprog](4gl_funprog.html) can be declared by using a data type prefixed by [Variable](4gl_variable.html), [Value](4gl_value.html), or [Const](4gl_const.html). They must be declared just after prefixing the data type that must be the same as the one sent in the `func`.

**The parameters can be transmitted as:**

* **References:** Modifications in the [Funprog](4gl_funprog.html) are done on the calling arguments. This is done when the arguments are declared with the [Variable](4gl_variable.html) keyword.
* **Values:** A copy of the arguments is done on local variables. Modifications done in the [Funprog](4gl_funprog.html) do not change the value of the parameter in the calling script. This is done when the arguments are declared with the [Value](4gl_value.html) keyword.
* **References to constants:** This prevents performing a copy of the arguments; however, the argument is read only and any modification attempt creates an error. This is done when the arguments are declared with the [Const](4gl_const.html) keyword.

The declaration of the parameters is not mandatory, and this allows you to send parameters of variable types. Make sure that they are transmitted as references on read-only values, exactly as if they would have been declared with [Const](4gl_const.html).

The parameters can be variables or expressions. If a parameter is an expression, it can only be transferred by value; the [Funprog](4gl_funprog.html) parameter cannot be defined with dimensions.

A variable passed in parameters can be declared with dimensions. The number of dimensions must be the same. A sub-array can be transmitted as shown in one of the previous examples.

## Miscellaneous

A `func` can be called recursively and the number of embedded `func` is not limited. Nevertheless you have to pay attention to the available memory as the number of opened table in [Local](4gl_local.html) mode for each call nested is viewed independently.

The execution of a `func` must return a value. [End](4gl_end.html) without value triggers an error if executed in a [Funprog](4gl_funprog.html).

A `func` cannot be used in a condition of a [Where](4gl_where.html) sentence used in [File](4gl_file.html), [Filter](4gl_filter.html), or [For](4gl_for.html)statements. It cannot be transmitted to the database.

# Associated Errors

| Error code | Description |
| --- | --- |
| 10 | The expression giving the script name does not return a string value. |
| 20 | The process does not exist. |
| 39 | The label does not exist. |
| 55 | Number of dimensions invalid. |
| 69 | Number of parameters does not correspond. |
| 70 | Transmission mode incompatible. |

# See also

[Funprog](4gl_funprog.html), [Call](4gl_call.html), [Subprog](4gl_subprog.html), [End](4gl_end.html).

  

[Index](index.html)  [Home](getting-started_home.html)