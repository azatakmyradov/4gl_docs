[Index](index.html)  [Home](getting-started_home.html)

Ash

This function returns the inverse hyperbolic sine of a specified number.

# Syntax

```
ash(number)
```

# Examples

```
# Performs a sum of a list of calculated values
RESULT=ash(2) : # 1.4436355
```

# Comments

For real numbers, the hyperbolic sine definition is as follows:

```
ash(x)=ln(x+sqr(x^2+1))
```

  
where [ln](4gl_ln.html) is the natural logarithm and [sqr](4gl_sqr.html) the square root function.

The type of result is [Double](4gl_double.html).

# See also

[ach](4gl_ach.html), [ath](4gl_ath.html), [ch](4gl_ch.html), [sh](4gl_sh.html),[th](4gl_th.html), [ln](4gl_ln.html), [sqr](4gl_sqr.html).

  

[Index](index.html)  [Home](getting-started_home.html)