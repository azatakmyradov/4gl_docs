[Index](index.html)  [Home](getting-started_home.html)

Errp

`errp` returns the name of the script where an error occurred. It can be used in the error handling routine set by [Onerrgo](4gl_onerrgo.html).

# Syntax

```
   errp
```

# Examples

```
   # Let's trigger an error (division by zero)
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

`errp` returns a script name. The result type is [Char](4gl_char.html).  
 `errp` has only a significant value in the error handling routine.

# See also

[errn](4gl_errn.html), [errl](4gl_errl.html), [Onerrgo](4gl_onerrgo.html), [errmes$](4gl_errmes$.html), [errm](4gl_errm.html).

  

[Index](index.html)  [Home](getting-started_home.html)