[Index](index.html)  [Home](getting-started_home.html)

Sgn

`sgn` returns the sign (-1, 0 or +1) of a numeric value.

# Syntax

```
   sgn(EXP_NUM)
```

* `EXP_NUM` is an expression returning a numeric value.

# Examples

```
   CUBIC_ROOT = sgn(X) * abs(X) ^ (1/3)
```

# Description

`sgn(X)` returns:  
\* **+1** if X is strictly positive.  
\* **0** if X is zero.  
\* **-1** if X is strictly negative.

The type of result is [Integer](4gl_integer.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |

# See also

[abs](4gl_abs.html).

  

[Index](index.html)  [Home](getting-started_home.html)