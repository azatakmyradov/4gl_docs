[Index](index.html)  [Home](getting-started_home.html)

Ch

This function returns the hyperbolic cosine of a specified number.

# Syntax

```
ch(EXP_NUM)
```

* `EXP_NUM` is an expression that returns a numeric value.

# Examples

```
RESULT=ch(0.5) : # 1.127626
```

# Comments

This function can be calculated by the following formula:

```
ch(x)=(exp(x)+exp(-x))/2
```

  
Where [exp](4gl_exp.html) is the exponential function.

The type of result is [Double](4gl_double.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |
| 13 | Calculation overflow (x is too large). |

# See also

[ach](4gl_ach.html), [ash](4gl_ash.html), [ath](4gl_ath.html), [sh](4gl_sh.html),[th](4gl_th.html), [ln](4gl_ln.html), [sqr](4gl_sqr.html).

  

[Index](index.html)  [Home](getting-started_home.html)