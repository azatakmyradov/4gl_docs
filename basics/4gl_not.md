[Index](index.html)  [Home](getting-started_home.html)

Not

`not` corresponds to the unary boolean 'not' operator that can also be abbreviated by `!`.

# Syntax

```
    not EXPR_LOG
    ! EXPR_LOG
```

* `EXPR_LOG` is an expression that returns a numeric value (considered as false if zero; otherwise, true).

# Examples

```
   # Is I different from 1?
    If not(I = 1)
       # Here, I is not equal to 1
    Endif
```

# Description

`not` returns a boolean value (1=true, 0=false) depending on an expression that has a true (not zero) value or false (zero value) depending on the corresponding table:

| EXPR\_LOG value | not(EXPR\_LOG) value |
| --- | --- |
| false (0) | true (1) |
| true (not equal to 0) | false (0) |

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a number. |

# See also

[and](4gl_and.html), [or](4gl_or.html), [xor](4gl_xor.html).

  

[Index](index.html)  [Home](getting-started_home.html)