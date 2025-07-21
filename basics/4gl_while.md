[Index](index.html)  [Home](getting-started_home.html)

While

`While` allows you to repeat a loop of instructions as long as a condition is true.

# Syntax

```
While EXPRESSION
INSTRUCTION_LIST
Wend
```

* `INSTRUCTION_LIST` is a list of instructions in a script.
* `EXPRESSION` is a numeric expression that is considered as true if it is not equal to 0.

# Examples

```

  # Example 1 : let's perform a computation with successive approximations
  VARIA=INIT_VALUE
  While abs(func COMPUTE(VARIA)-TARGET)>EXPECTED_PRECISION
    VARIA=func ITERATE(VARIA)
  Wend

  # Example 2 : let's wait until the database is updated or until a limit hour is reached
  TIMEOUT="22:00:00"
  While time$<TIMEOUT
    Sleep 1
    Break func DATABASE_UPDATED=1
 Wend
```

# Description

`While` allows to perform loops as long as the following occurs:

* A condition is true, that is the numeric expression returns a not null value.
* A [Break](4gl_break.html) instruction has not been executed to interrupt the loop.

If the condition is false at the beginning, no iteration is done, and the execution resumes after the [Wend](4gl_wend.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The expression given after Until is not numeric. |

# See also

[For](4gl_for.html), [To](4gl_to.html), [Next](4gl_next.html), [Step](4gl_step.html), [Break](4gl_break.html), [Repeat](4gl_repeat.html), [Until](4gl_until.html), [Wend](4gl_wend.html), [If](4gl_if.html), [Then](4gl_then.html), [Else](4gl_else.html), [Elsif](4gl_elsif.html), [Endif](4gl_endif.html).

  

[Index](index.html)  [Home](getting-started_home.html)