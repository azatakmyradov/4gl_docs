[Index](index.html)  [Home](getting-started_home.html)

Until

`Until` ends a [Repeat](4gl_repeat.html) loop.

# Syntax

```
Repeat
INSTRUCTION_LIST
Until EXPRESSION
```

* `INSTRUCTION_LIST` is a list of instructions in a script.
* `EXPRESSION` is a numeric expression that is considered as true if it is not equal to 0.

# Examples

```

  # Example 1 : let's perform a computation with successive approximations
  VARIA=INIT_VALUE
  Repeat
    VARIA=func ITERATE(VARIA)
  Until abs(func COMPUTE(VARIA)-TARGET)<EXPECTED_PRECISION


  # Example 2 : let's wait until the database is updated or until a limit hour is reached
  TIMEOUT="22:00:00"
  Repeat
    Sleep 1
    Break func DATABASE_UPDATED=1
 Until time$>=TIMEOUT
```

# Description

`Until` ends a [Repeat](4gl_repeat.html) loop if:

* A condition becomes true, that is the numeric expression returns a not null value.
* A break instruction is performed to interrupt the loop.

At least one iteration is done on the `Repeat`..`Until` loop, even if the condition is true when the loop starts. This is because the condition is evaluated only at `Until` statement.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The expression given after Until is not numeric. |

# See also

[For](4gl_for.html), [To](4gl_to.html), [Next](4gl_next.html), [Step](4gl_step.html), [Break](4gl_break.html), [Repeat](4gl_repeat.html), [While](4gl_while.html), [Wend](4gl_wend.html), [If](4gl_if.html), [Then](4gl_then.html), [Else](4gl_else.html), [Elsif](4gl_elsif.html), [Endif](4gl_endif.html).

  

[Index](index.html)  [Home](getting-started_home.html)