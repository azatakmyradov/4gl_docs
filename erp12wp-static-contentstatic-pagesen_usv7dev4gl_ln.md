[Index](index.html)  [Home](getting-started_home.html)

Ln

`ln` returns the natural logarithm of its argument (natural means e based, where e=2.718261826459045...).

# Syntax

```
   ln(NUMERIC_EXPR)
```

* `NUMERIC_EXPR` is an expression returning a numeric value, which must be strictly positive and smaller than 10^80.

# Example

```
   Y = ln(exp(2)): # Returns 2
```

# Description

This function returns the natural logarithm of its argument. The type of result is [Double](4gl_double.html). The reverse function of `log(x)` is the exponential function: [exp](4gl_exp.html)(x).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |
| 14 | The argument is negative. |
| 52 | The argument is null. |

# See also

[log](4gl_log.html), [exp](4gl_exp.html).

  

[Index](index.html)  [Home](getting-started_home.html)