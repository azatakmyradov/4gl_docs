[Index](index.html)  [Home](getting-started_home.html)

Fac

`fac` returns the factorial of an integer value.

# Syntax

```
   fac(INTEGER_EXPR)
```

* `INTEGER_EXPR` is an expression returning an integer value.
  0 <= `INTEGER_EXPR` <= 58

# Examples

```
   VALUE=fac(6) : # returns 720
   SIXTEEN = fac(16) / fac(15)
   ARRANGEMENT = fac(N) / (fac(P) * fac(N-P))
```

# Description

`fac(N)` returns N*(N-1)*(N-2)\* ... *2*1

By convention, `fac(0)` equals 1.

The type of result is [Integer](4gl_integer.html) or [Decimal](4gl_decimal.html) depending on whether the result is greater or smaller than 2^31-1.

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |
| 13 | Calculation overflow (x is too big, greater than 58). |
| 58 | The argument is not an integer. |

# See also

[cnp](4gl_cnp.html), [anp](4gl_anp.html).

  

[Index](index.html)  [Home](getting-started_home.html)