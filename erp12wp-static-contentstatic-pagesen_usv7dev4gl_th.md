[Index](index.html)  [Home](getting-started_home.html)

Th

This function returns the hyperbolic tangent of a specified number.

# Syntax

```
th(number)
```

# Examples

```
RESULT=th(0.5) : # 0.4621172
```

# Comments

This function can be calculated by the following formula:

```
th(x)=(exp(2*x)+1)/(exp(2*x)-1)/2
```

  
Where [exp](4gl_exp.html) is the exponential function.

The type of result is [Double](4gl_double.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 13 | Calculation overflow (x is too big). |

# See also

[ach](4gl_ach.html), [ash](4gl_ash.html), [ath](4gl_ath.html), [ch](4gl_ch.html),[sh](4gl_sh.html), [ln](4gl_ln.html), [sqr](4gl_sqr.html).

  

[Index](index.html)  [Home](getting-started_home.html)