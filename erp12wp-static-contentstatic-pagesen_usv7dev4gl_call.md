[Index](index.html)  [Home](getting-started_home.html)

Call

This instruction is used to call a subroutine executed with its own local variables class.  
No value is returned by this instruction. Parameters can be transmitted as values or as references; so that the parameters transmitted by reference can be modified by the subroutine.

# Syntax

```
Call SUBPROGRAM
Call SUBPROGRAM From LIBRARY
Call SUBPROGRAM(ARGUMENT_LIST)
Call SUBPROGRAM(ARGUMENT_LIST) From LIBRARY
Call SUBPROGRAM From =EXPRESSION_LIBRARY
Call SUBPROGRAM(ARGUMENT_LIST) From =EXPRESSION_LIBRARY
Call =EXPRESSION_CALL
Call =EXPRESSION_CALL From LIBRARY
Call =EXPRESSION_CALL With (ARGUMENT_LIST)
Call =EXPRESSION_CALL With (ARGUMENT_LIST) From LIBRARY
Call =EXPRESSION_CALL With (ARGUMENT_LIST) From =EXPRESSION_LIBRARY
Call =EXPRESSION_CALL With (ARGUMENT_LIST) From =EXPRESSION_LIBRARY
```

* `SUBPROGRAM` is the name of the routine declared by the [Subprog](4gl_subprog.html) keyword.
* `LIBRARY` is the name of the script that contains the code of the routine called.
* `ARGUMENT_LIST` is a list of expressions, variables, or subarrays that can be empty. The elements are separated by commas.
* `EXPRESSION_LIBRARY` is an alphanumeric expression whose evaluation returns the script name that contains the code of the routine called.
* `EXPRESSION_CALL` is an alphanumeric expression whose evaluation returns the name of the routine called.

# Examples

```
  # Call of a routine that increments a value
  Local Integer I
  I=314 : Call ADD_ONE(I)
  I=314 : Call TRY_TO_ADD_ONE(I)
  I=315 : Call FAIL_TO_ADD_ONE(I)
  # The value of I found here depends on how the parameter has been declared in the routine
  # After the first call, I=315
  # After the second call, I=314
  # The third call will raise an error
  ...

  # Case 1 : the argument is declared as a reference
  Subprog ADD_ONE(J)
  Variable Integer J
    J+=1  : # J is equal to 315, but J is a reference to I in the calling script, so I is equal to 315
    I=316 : # I is a local variable that does not refer to the I variable in the calling script
  End

  # Case 2 : the argument is declared as a value
  Subprog TRY_TO_ADD_ONE(J)
  Value Integer J
    J+=1 : # J is equal to 315, but J is a local copy of I that is not sent back, so I remains equal to 314
  End

  # Case 3 : the argument is declared as a constant reference
  Subprog FAIL_TO_ADD_ONE(J)
  Value Integer J
    J+=1  : # Raises an error : J is read-only
  End


  # Call of a subroutine with parameters in another process
  Local Integer MATRIX(1..10,1..20,1..30)
  ...
  # Only a subarray is transmitted (even if it is sent as a reference)
  Call COMPUTE_SUM(MATRIX(5..6,2..4,1..20),RESULT) FROM MATRIX_LIBRARY
  ...
  # In the MATRIX_LIBRARY script, the arguments are
  Subprog COMPUTE_SUM(MATRIX,RESULT)
  Const Integer MATRIX(,,)
  Variable Integer RESULT
    RESULT=sum(MATRIX)
  End

  # A subprogram that returns the data type of the argument
  Subprog RETURN_TYPE(ARGUMENT,DATA_TYPE)
  Variable Integer DATA_TYPE
    DATA_TYPE=type(ARGUMENT)
  End


  # Example of sub-program with a variable type of argument
  Local Integer DATA_TYPE
  Local Char MY_STRING(20),TEXT(10)
  MY_STRING="abcdefghijklmnopqrst"

  Call RETURN_TYPE(pi,DATA_TYPE,TEXT)          : # Will return 7 (decimal) and "3.14159265"
  Call RETURN_TYPE([1/1/2013],DATA_TYPE,TEXT)  : # Will return 3 (date) and "01/01/2013"
  Call RETURN_TYPE(100,DATA_TYPE,TEXT)         : # Will return 4 (integer) and "100"
  Call RETURN_TYPE("text sent",DATA_TYPE,TEXT) : # Will return 523 (clob) and "text sent"
  Call RETURN_TYPE(MY_STRING,DATA_TYPE,TEXT)   : # Will return 20 (string 10) and "abcdefghij"
  End

  # ARGUMENT has not be declared because it has a variable type
  Subprog RETURN_TYPE(ARGUMENT,DATA_TYPE,TEXT)
  Variable Integer DATA_TYPE
  Variable Char TEXT()
    DATA_TYPE=type(ARGUMENT) : # returns the data type of the argument
    TEXT=num$(ARGUMENT)      : # returns a string representation of the argument regardless of its type
  End
```

# Comments

* `Call` executes a subroutine with possible parameters. The calling code will end its execution when an [End](4gl_end.html) instruction is encountered. The calling process will then resume the execution with the instruction located after the `call` instruction.
* The local variables and all the resources opened with Local keyword in the subroutine are lost after the execution of the call.
* A `call` performed without specifying a script is done on the same script.
* The number of parameters transmitted in the "call" must correspond to the number of parameters declared in the [Subprog](4gl_subprog.html) instruction.
* The parameters of the [Subprog](4gl_subprog.html) can be declared by using a data type prefixed by [Variable](4gl_variable.html), [Value](4gl_value.html), or [Const](4gl_const.html). They must be declared just after prefixing the data type that must be the same as the one sent in the Call.
* **The parameter can be transmitted as:**

  + **References**: Modifications in the [Subprog](4gl_subprog.html) are performed on the calling arguments. This is done when the arguments are declared with the [Variable](4gl_variable.html) keyword.
  + **Values**: A copy of the arguments is performed on local variables. Modifications done in the [Subprog](4gl_subprog.html) do not change the value of the parameter in the calling script. This is done when the arguments are declared with the [Value](4gl_value.html) keyword.
  + **References to constants**: This process avoids to perform a copy of the arguments. The argument is read only and any modification attempt will create an error. This is done when the arguments are declared with the [Const](4gl_const.html) keyword.
* The declaration of the parameters is not mandatory, and allows you to send parameters of variable types. Make sure that they are transmitted as references on read-only values (exactly as if they would have been declared with [Const](4gl_const.html)).
* The parameters may be variables or expressions. If a parameter is an expression, it can only be transferred by value; the [Subprog](4gl_subprog.html) parameter cannot be defined with dimensions.
* A variable passed in parameters can be declared with dimensions. The number of dimensions must be the same. A subarray can be transmitted as shown in one of the previous examples.
* **During a "call", the following information is saved:**

  + Local Variables.
  + The tables declared with the current values of the corresponding [F] and [G] classes.
  + The group of the default class lists (outside of any local class).
* **The following information is lost:**

  + The tables reopened with the same abbreviation in the subroutine.
  + The label associated with [Onerrgo](4gl_onerrgo.html) is not saved when passing to a subroutine even if this is performed in the same process.
* When executing a "call", a class of local variables is created with the subroutine, abbreviated [L]. This local class becomes the default class since the local class with the calling process is no longer accessible. When you return to the process, you will find the default local class which existed before the call.
* A "call" can be called recursively and the number of embedded "calls" is not limited. Nevertheless, pay close attention to the available memory as the number of opened table in [Local](4gl_local.html) mode for each call nested is viewed independently.

# Associated Errors

| Error code | Description |
| --- | --- |
| 10 | The expression giving the script name does not return a string value. |
| 20 | The process does not exist. |
| 39 | The label does not exist. |
| 55 | Number of dimensions invalid. |
| 69 | Number of parameters does not correspond. |
| 70 | Transmission mode incompatible. |

  

[Index](index.html)  [Home](getting-started_home.html)