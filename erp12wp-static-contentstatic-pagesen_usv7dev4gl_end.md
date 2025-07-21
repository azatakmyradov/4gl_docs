[Index](index.html)  [Home](getting-started_home.html)

End

Use `End` to end execution of a routine or subprogram called by [Call](4gl_call.html), [Onerrgo](4gl_onerrgo.html), [func](4gl_func.html), or [fmet](4gl_fmet.html) instruction.

# Syntax

```
End
End EXPRESSION
```

* `EXPRESSION` is an expression that is evaluated to return a value (only if End terminates the execution of code called by [func](4gl_func.html) or [fmet](4gl_fmet.html)).

Examples

```
# Example 1: A subprogram is called
  Call COMPUTE(ARRAY(1..20),RESULT)
  ...

Subprog COMPUTE(ARRAY,RESULT)
Const Integer ARRAY()
Variable Decimal RESULT
  RESULT=avg(ARRAY)/1+abs(max(ARRAY))
End : # Returns to the calling routine

# Example 2: A func is called
  RESULT=func CLEVER_COMPUTE(ARRAY(1..20))
  ...

Funprog CLEVER_COMPUTE(ARRAY)
Const Integer ARRAY()
End avg(ARRAY)/1+abs(max(ARRAY))

# Example 3: Error handling routine
Onerrgo ERROR_MANAGEMENT
  ...
# The code that executes here might be interrupted by an error
  ...

# ERROR_LIST is supposed to be an array containing the errors code that are considered as minor in the context
$ERROR_MANAGEMENT
If find(errnum,MINOR_ERROR_LIST)
  MINOR_ERROR=1
  Resume : # Returns to the instruction following the execution that threw an error, MINOR_ERROR is set
Endif
End
```

# Description and comments

* `End` ends the execution of a script, returning to its caller, which can be a script using [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html) instructions.
* At the first level of execution, the process ends. An End of this type is normally only executed in supervisor code.
* When `End` ends a handling error routine called by [Onerrgo](4gl_onerrgo.html), the procedure in which the error was thrown is ended.
* If a transaction was started by [Trbegin](4gl_trbegin.html) and not ended by [Commit](4gl_commit.html) in the script that ends with the `End` instruction, a [Rollback](4gl_rollback.html) is automatically performed. This does not happen if the transaction was initiated by the calling routine.

# Associated errors

No associated errors.

# See also

[Call](4gl_call.html), [Subprog](4gl_subprog.html), [Funprog](4gl_funprog.html), [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html), [Onerrgo](4gl_onerrgo.html), [fmet](4gl_fmet.html), [func](4gl_func.html).

  

[Index](index.html)  [Home](getting-started_home.html)