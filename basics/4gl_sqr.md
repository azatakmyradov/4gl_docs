[Index](index.html)  [Home](getting-started_home.html)

Sqr

`sqr` returns the square root of a number.

# Syntax

```
   sqr(EXPR_NUM)
```

* `EXPR_NUM` is a numeric expression.

# Examples

```
   SQR_2=sqr(2)

   # Solves A*X^2+B*X+C=0 with real values
   DET=B*B-4*A*C
   If DET>0
     SOLUTION_1 = (-B +sqr(DET))/(2*A)
     SOLUTION_2 = (-B -sqr(DET))/(2*A)
   Endif
```

# Description

`sqr(X)` returns the positive number whose square is X.

The type of result is [Double](4gl_double.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |
| 11 | The argument is strictly negative. |

# See also

[log](4gl_log.html), [ln](4gl_ln.html).

  

[Index](index.html)  [Home](getting-started_home.html)