[Index](index.html)  [Home](getting-started_home.html)

Sh

This function returns the hyperbolic sine of a specified number.

# Syntax

```
sh(number)
```

# Examples

```
RESULT=ch(0.5) : # 0.5210953
```

# Comments

This function can be calculated by the following formula:

```
ch(x)=(exp(x)-exp(-x))/2
```

  
Where [exp](4gl_exp.html) is the exponential function.

The type of result is [Double](4gl_double.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 13 | Calculation overflow (x is too big). |

# See also

[ach](4gl_ach.html), [ash](4gl_ash.html), [ath](4gl_ath.html), [ch](4gl_ch.html),[th](4gl_th.html), [ln](4gl_ln.html), [sqr](4gl_sqr.html).

  

[Index](index.html)  [Home](getting-started_home.html)