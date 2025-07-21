[Index](index.html)  [Home](getting-started_home.html)

Ath

This function returns the inverse hyperbolic tangent of a specified number.

# Syntax

```
ath(number)
```

# Examples

```
RESULT=ath(0.5) : # 0.5493061
```

# Comments

This function is only defined in the range ]-1,1[ and it can be calculated by using the following formula:

```
ath(x)=ln(sqr((1+x)/(1-x)))
```

  
where [ln](4gl_ln.html) is the natural logarithm and [sqr](4gl_sqr.html) the square root function.

The type of result is [Double](4gl_double.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 15 | Hyperbolic function error: the value given is not in the range ]-1,1[ |

# See also

[ach](4gl_ach.html), [ash](4gl_ash.html), [ch](4gl_ch.html), [sh](4gl_sh.html),[th](4gl_th.html), [ln](4gl_ln.html), [sqr](4gl_sqr.html).

  

[Index](index.html)  [Home](getting-started_home.html)