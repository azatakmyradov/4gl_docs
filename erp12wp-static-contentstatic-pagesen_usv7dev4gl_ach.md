[Index](index.html)  [Home](getting-started_home.html)

Ach

This function returns the inverse hyperbolic cosine of a specified number.

# Syntax

```
ach(number)
```

# Examples

```
RESULT=ach(2) : # 1.3169579
```

# Comments

For real positive numbers, the hyperbolic cosine definition is as follows:

```
ach(x)=ln(x+sqr(x^2-1))
```

  
where [ln](4gl_ln.html) is the natural logarithm and [sqr](4gl_sqr.html) the square root function.

The type of result is [Double](4gl_double.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 15 | Hyperbolic function error: the value given is in the range ]-1,1[ |

# See also

[ash](4gl_ash.html), [ath](4gl_ath.html), [ch](4gl_ch.html), [sh](4gl_sh.html),[th](4gl_th.html), [ln](4gl_ln.html), [sqr](4gl_sqr.html).

  

[Index](index.html)  [Home](getting-started_home.html)