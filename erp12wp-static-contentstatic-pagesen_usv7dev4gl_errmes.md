[Index](index.html)  [Home](getting-started_home.html)

Errmes$

`errmes$` returns the message associated with a numeric error code available when an error occurs. It is frequently used when the error code [errn](4gl_errn.html) is used, in the error handling routine set by [Onerrgo](4gl_onerrgo.html).

# Syntax

```
   errmes$(INT_EXPR)
```

* `INT_EXPR` is an expression returning an integer value.

# Examples

```

   # Example 1 : What does error 10 mean ?
   Local Char ERROR_10(200)
   ERROR_10=errmes$(10) : # if connected in English, contains "Incompatibility of Type"

   # Example 2 : Let's trigger an error (division by zero)
   Funprog DIV_BY_ZERO
   Local Integer ZERO, ONE, RESULT
   Local Char ERROR_MESSAGE(250)
   ONE=1 : ZERO=0

    Onerrgo ERR_HANDLE
    RESULT = ONE / ZERO

    End ERROR_MESSAGE

$ERR_HANDLE
    ERROR_MESSAGE="Error"-num$(errn)-"raised on line"-num$(errl)-"in script"-errp-"Message:"-errmes$(errn)
&                -"Additional details:"-errm
    Resume
```

# Description

`errmess$` returns the description associated with an error code that is assigned when an error occurs on a script. The result type is [Char](4gl_char.html). The message returned depends on the connection language.

As `errn` only has a significant value in the error handling routine, `errmes$` should be primarily used in error handling routines.

In the different script glossary documentations, the **Associated errors** chapter provides the value of the errors that can occur for each instruction or function. The message can be retrieved by using `errmes$` with the given error values, even directly from the calculator.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |
| 50 | Negative argument. |

# See also

[errl](4gl_errl.html), [errp](4gl_errp.html), [Onerrgo](4gl_onerrgo.html), [errn](4gl_errn.html), [errm](4gl_errm.html).

  

[Index](index.html)  [Home](getting-started_home.html)