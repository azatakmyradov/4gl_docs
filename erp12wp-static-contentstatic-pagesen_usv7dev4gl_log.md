[Index](index.html)  [Home](getting-started_home.html)

Log

`log` returns the 10 based logarithm of its argument.

# Syntax

```
   log(NUMERIC_EXPR)
```

* `NUMERIC_EXPR` is an expression returning a numeric value. It must be strictly positive and smaller than 10^80.

# Examples

```
   Y = log(1000): # Returns 3
```

# Description

This function returns the decimal logarithm of its argument. The type of result is [Double](4gl_double.html). The reverse function of `log(x)` is the power of 10 : `10^x`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |
| 14 | The argument is negative. |
| 52 | The argument is null. |

# See also

[ln](4gl_ln.html), [exp](4gl_exp.html).

  

[Index](index.html)  [Home](getting-started_home.html)