[Index](index.html)  [Home](getting-started_home.html)

Goto

`Goto` performs an unconditional branch from a script to another label.

# Syntax

```
 Goto LABEL
 Goto LABEL From SCRIPT
 Goto LABEL FROM =STRING_EXPR
```

* `LABEL` is a label that is declared with `$LABEL` or `LABEL` in the script that is called (the current one per default). A label must start with a letter, can include letters, underscores, and digits. The letter is always in uppercase.
* `SCRIPT` is the script name when the script is constant.
* `STRING_EXPRESSION` is an expression that returns the script name (used when the script is a variable).

The script can be prefixed by the folder code followed by a dot when it is only an evaluated script. If not, the script is searched in the folder. If the script is not found in the folder then the search is carried out in the hierarchy of folders given by the [adxmother](4gl_adxmother.html) variable in ascending order.

# Examples

```
# Example 1: The first label is called by a Gosub an returns a value for I depending on J
# The resulting values for I will be:
# If J=0, I=6; If J=1, I=6; If J=1, I=5; If J=3 to 99, I=3, If J is negative or over 100, I=10
# J=0 : I=6
# J=0 : I=6
$GET_VALUE
Local Integer I
  I=0
  If J=0      : Goto J0
  Elsif J=1   : Goto J1
  Elsif J=2   : Goto J2
  Elsif J<100 : Goto J3
  Endif
  I+=4
$J0
$J1 : I+=1
J2  : I+=2
J3  : I+=3
Return

# If a fatal error happens, perform some actions in another script with no return
# The script name is ERROR_HANDLER_ followed by the error value
If ERROR_STATUS>FATAL_ERROR
  Goto ERROR From ="ERROR_HANDLER_"+num$(ERROR_STATUS)
Endif
```

# Description and comments

The `Goto` instruction performs an unconditional jump. It breaks the execution order of a script that will execute the line in sequential order.

All the context is shared, especially:  
\* The local variable class.  
\* The default class list of values.  
\* The tables and joins opened.  
\* The transaction in progress. In a script where a branch has been done by [Goto](4gl_goto.html), you can commit a transaction that has been opened in the calling script, which is not the case if the script is called by [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html).  
\* The error handler set by [Onerrgo](4gl_onerrgo.html).

# Comments

As a lot of code nesting instructions exist ([If](4gl_if.html)..[Elsif](4gl_elsif.html)..[Else](4gl_else.html)..[Endif](4gl_endif.html), [While](4gl_while.html)..[Wend](4gl_wend.html), [Repeat](4gl_repeat.html)..[Until](4gl_until.html), [Case](4gl_case.html).. [When](4gl_when.html).. [When](4gl_when.html) [Default](4gl_default.html).. [Endcase](4gl_endcase.html), [For](4gl_for.html).. [Next](4gl_next.html), [Break](4gl_break.html)), using [Goto](4gl_goto.html) is the outdated method of writing code and difficult to read. It should therefore be avoided.

A given label must be unique in a given script (this is also checked at compilation time).

# Associated errors

| Error code | Description |
| --- | --- |
| 20 | Script does not exist or cannot be accessed (Goto ... From syntax), or label does not exist in the corresponding script. |

# See also

[Gosub](4gl_gosub.html), [Return](4gl_return.html), [Call](4gl_call.html), [Subprog](4gl_subprog.html), [Funprog](4gl_funprog.html), [func](4gl_func.html), [fmet](4gl_fmet.html).

  

[Index](index.html)  [Home](getting-started_home.html)