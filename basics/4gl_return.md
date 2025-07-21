[Index](index.html)  [Home](getting-started_home.html)

Return

`Return` ends a script called by [Gosub](4gl_gosub.html) and resumes the execution to the instruction that follows the [Gosub](4gl_gosub.html).

# Syntax

```
  Return
```

# Examples

```
# Call several labels by Gosub. These labels have a common return.

$ TEST_GOSUB
  Local Integer I
    Gosub INCREMENT
    Gosub INCREMENT_TWICE
    Gosub INCREMENT_THREE_TIMES
    # Here, the value of I is 6
Return

$INCREMENT_THREE_TIMES : I+=1
$INCREMENT_TWICE       : I+=1
$INCREMENT             : I+=1
Return
```

# Description

`Return` returns the execution to the statement that follows the [Gosub](4gl_gosub.html) statement, as indicated by the following schema:

| Execution order | Instruction |
| --- | --- |
| 1 | Gosub MY\_LABEL |
| 2 | $MY\_LABEL |
| 3 | ... instructions following MY\_LABEL |
| 4 | Return |
| 5 | ... instructions after Gosub |
| 6 | End |

# Comments

A script called by [Call](4gl_call.html), [fmet](4gl_fmet.html), or [func](4gl_func.html) cannot end by a `Return` but only by an [End](4gl_end.html) statement.

# Associated errors

| Execution order | Instruction |
| --- | --- |
| 32 | Return encountered without preliminary Gosub. |

# See also

[Gosub](4gl_gosub.html), [Call](4gl_call.html), [func](4gl_func.html), [fmet](4gl_fmet.html), [Subprog](4gl_subprog.html), [Funprog](4gl_funprog.html).

  

[Index](index.html)  [Home](getting-started_home.html)