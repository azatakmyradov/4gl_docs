[Index](index.html)  [Home](getting-started_home.html)

Cnp

`cnp` calculates the number of arrangements of 'p' objects taken from 'n'.

# Syntax

```
   cnp(N,P)
```

\* 'N' and 'P' are integer expressions. 'P' must be in the [0,N] range.

# Examples

```
   Local Integer I,J, NB_ARR
   I=10
   J=8
   NB_PERM=cnp(I,J) : # Returns 45
```

# Description

`cnp(N,P)` returns `fac(N)/ (fac(P)*fac(N-P))`.

To avoid loosing precision, the calculation algorithm does not use the factorial function. If 'N' and 'P' are not integer values, they are truncated.

The type of result is `Integer` or `Decimal` depending if the value is smaller or greater than 2^31-1.

# Associated errors

| Error | Description |
| --- | --- |
| 10 | Not a numeric argument. |
| 13 | Out of range calculation. |
| 50 | Domain error. |

# See also

[fac](4gl_fac.html), [anp](4gl_anp.html).

  

[Index](index.html)  [Home](getting-started_home.html)