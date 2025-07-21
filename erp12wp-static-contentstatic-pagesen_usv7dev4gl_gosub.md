[Index](index.html)  [Home](getting-started_home.html)

Gosub

`Gosub` is used to call a subroutine at a given label. This subroutine ends with [Return](4gl_return.html) and shares all the local context with the calling script. There is no parameters that can be passed and no data insulation between the script that calls and the subroutine.

# Syntax

```
 Gosub LABEL
 Gosub LABEL From SCRIPT
 Gosub LABEL FROM =STRING_EXPR
```

* `LABEL` is a label that is declared with `$LABEL` or `LABEL` in the script that is called (the current one per default). A label must start with a letter, can include letters, underscores, and digits. The letter is always uppercase.
* `SCRIPT` is the script name when the script is constant.
* `STRING_EXPRESSION` is an expression that returns the script name (used when the script is a variable).

The script can be prefixed by the folder code followed by a dot when it is only an evaluated script. If not, the script is searched in the folder. If the script is not found in the folder, then the search is carried out in the hierarchy of folders given by the [adxmother](4gl_adxmother.html) variable in ascending order.

# Examples

```
# Example 1: The final value returned here for I will be 6
Subprog GET_VALUE(I)
Variable Integer I

  I=0
  Gosub LABEL1 : # I value is 3 after the Gosub
  Gosub LABEL2 : # I value is 5 after the Gosub
  Gosub LABEL3 : # I value is 6 after the Gosub
  End

LABEL1  : I+=1
$LABEL2 : I+=1
LABEL3
  I+=1
  Return

# Example 2: use computed subprogs to get execute an action : EVENT_CODE describes an event
# If EVENT_CODE is equal to END, the second Gosub will call an ACTION label in a script called EVENT_END
$HANDLE_EVENT
 Gosub ASSIGN_HANDLER From ="X3.DECODING_TOOLS" : # Must be called in X3 folder even if a more local script exists
 Gosub ACTION From =EVENT_HANDLER
Return

# In DECODING_TOOL script
Local Char EVENT_HANDLER(40)
EVENT_HANDLER="EVENT_"+EVENT_CODE
Return
```

# Description and comments

The `Gosub` calls a section of code that ends with a [Return](4gl_return.html).

All the context is shared, especially:  
\* The local variable class.  
\* The default class list of values.  
\* The tables and joins opened.  
\* The transaction in progress. In a script called by [Gosub](4gl_gosub.html), you can commit a transaction that has been opened in the calling script, which is not the case if the script is called by [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html).  
\* The error handler set by [Onerrgo](4gl_onerrgo.html).

# Comments

No control of nesting on the `Gosub` / `Return` is done at compilation time (a return can be common to several labels). If a local label is called in a script, the existing label is verified at compilation time.

A given label must be unique in a given script (this is also checked at compilation time).

A label called by `Gosub` must end with a [Return](4gl_return.html) and not with an [End](4gl_end.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 31 | No more memory available (can happen if a recursive not ending Gosub is executed). |
| 32 | Return that does not correspond to a Gosub (arrives when a Return is encountered and an End is expected). |
| 20 | Script does not exist or cannot be accessed (Gosub ... From syntax), or label does not exist in the corresponding script. |

# See also

[Goto](4gl_goto.html), [Return](4gl_return.html), [Call](4gl_call.html), [Subprog](4gl_subprog.html), [Funprog](4gl_funprog.html), [func](4gl_func.html), [fmet](4gl_fmet.html).

  

[Index](index.html)  [Home](getting-started_home.html)