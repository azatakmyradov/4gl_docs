[Index](index.html)  [Home](getting-started_home.html)

Resume

`Resume` allows you to end the execution of an error handling routine and resume the execution at the line that follows the line where the error was thrown.

# Syntax

```
   Resume
```

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

# Comments

`Resume` is only usable if an error routing defined by `Onerrgo` has been set and if an error was thrown.

The instruction where the execution resumes is the following:

* If the error was encountered in an [If](4gl_if.html), the execution resumes after the [Endif](4gl_endif.html).
* If the error was encountered in a [For](4gl_for.html), the execution resumes after the [Next](4gl_next.html).
* If the error was encountered in a [While](4gl_while.html), the execution resumes after the [Wend](4gl_wend.html).
* If the error was encountered in an [Until](4gl_until.html), the execution resumes after the [Until](4gl_until.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 32 | No error routing was done prior to the Resume execution. |

# See also

[Onerrgo](4gl_onerrgo.html), [End](4gl_end.html), [errn](4gl_errn.html), [errl](4gl_errl.html), [errp](4gl_errp.html), [errmes$](4gl_errmes$.html).

  

[Index](index.html)  [Home](getting-started_home.html)