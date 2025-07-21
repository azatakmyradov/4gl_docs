[Index](index.html)  [Home](getting-started_home.html)

Onerrgo

Use `Onerrgo` to set up a branch label used if an error is thrown.

# Syntax

```
   Onerrgo
   Onerrgo LABEL
   Onerggo LABEL From SCRIPT
```

* `LABEL` is a label defined in the current script by default.
* `SCRIPT` is the name of a script in which the label is defined. It can also be given with the syntax = `EXPR`.
* `EXPR` is a string expression that returns the name of the script in which the label is defined.

# Examples

```
   # Open a file, and handle the error
    ERROR_FLAG=0
    # OPEN_ERROR is the label used if the file cannot be opened (in a dedicated script ERRMGT)
    Onerrgo OPEN_ERR From ERRMGT
    # Let's open the file
    Openi filpath("TXT","TEST","txt")
    If ERROR_FLAG
      End
    Endif
    # No more error management here
    Onerrgo
    ...
End


# Extract of the ERRMGT script
$OPEN_ERROR
  ERROR_FLAG=errn
  ERROR_MSG=errmes$(errn)
Resume
```

# Description

`Onerrgo` allows you to define a label where a branch is done when an error is thrown by the engine. When an error happens, the script lines following the label are executed. In this script:

* The [errn](4gl_errn.html) function returns an error number, defined in the Error section of the documentation.
* The [errp](4gl_errp.html) function returns the name of the script where the error was triggered.
* The [errl](4gl_errl.html) function returns the line number in the script where the error was triggered.
* The [errmes$](4gl_errmes$.html)(N) function returns the message associated with the error number N.

If a new error is thrown in the error handling script, no error rerouting is executed again to avoid infinite loops.

The error routine can terminate by using one of the following statements:

* [Resume](4gl_resume.html) will resume the execution in the calling script on the line that follows the line where the error was thrown.
* [End](4gl_end.html) will end the execution of the script.

`Onerrgo`, without label, disables the routing on error. After this instruction, an error interrupts the script and displays the error.

# Comment

When a transaction started by [Trbegin](4gl_trbegin.html) provokes an error while in progress, the error handling script cannot [Commit](4gl_commit.html) or [Rollback](4gl_rollback.html) the transaction. This must be done in the original program. However, if the error handling script reaches an [End](4gl_end.html) statement, an automatic [Rollback](4gl_rollback.html) of the transaction is performed.

An `Onerrgo` declaration in a script remains valid until the script ends or another `Onerrgo` statement is encountered. The execution of the error routing causes the suspension of an `Onerrgo` effect until the [Resume](4gl_resume.html) instruction is encountered.

When a script invokes a routine by [Call](4gl_call.html) where no `Onerrgo` instruction is required, an error encountered during the call stops the script execution while the error script takes over as if the error was encountered on the [Call](4gl_call.html) line. If the errors have to be handled in the nested call, it is important to use `Onerrgo` in the called script.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The expression that gives the script name does not return a string value. |
| 20 | The script does not exist. |
| 39 | The label does not exist. This happens only at execution time if the label is located in another script; otherwise, it is detected at script compilation. |

# See also

[End](4gl_end.html), [Resume](4gl_resume.html), [errn](4gl_errn.html), [errl](4gl_errl.html), [errp](4gl_errp.html), [errmes$](4gl_errmes$.html), [errm](4gl_errm.html), [Call](4gl_call.html).

  

[Index](index.html)  [Home](getting-started_home.html)