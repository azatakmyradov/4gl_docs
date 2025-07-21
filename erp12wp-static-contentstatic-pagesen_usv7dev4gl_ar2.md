[Index](index.html)  [Home](getting-started_home.html)

Ar2

`ar2` is a function that rounds a number to two digits. The method used is the method known as [Round half away from zero](https://en.wikipedia.org/wiki/Rounding#Round_half_away_from_zero)

# Syntax

```
  ar2(NUMEXPR)
```

* `NUMEXPR` is an expression returning a numeric value.

# Examples

```
Local Decimal AMOUNT1, AMOUNT2, ROUNDED1, ROUNDED2, ROUNDED3

  AMOUNT1=3.14159265 : ROUNDED1=ar2(AMOUNT1) : # ROUNDED1 is equal to 3.14

  AMOUNT1=40.055 : AMOUNT2=-AMOUNT1
  ROUNDED1=ar2(AMOUNT1) : ROUNDED2=ar2(AMOUNT2)
  ROUNDED3=-ROUNDED1
  # The value found are now
  # ROUNDED1=40.06, ROUNDED2=-40.06, ROUNDED3=-40.06
```

# Description

`ar2(X)` can also be calculated by one of the following formulas:  
\* [sgn](4gl_sgn.html)(X)*[int](4gl_int.html)(100*[abs](4gl_abs.html)(X)+0.5)/100  
\* [arr](4gl_arr.html)(X\*100,1)/100  
\* [arr](4gl_arr.html)(X,0.01)

The type of result is the same as the type of its argument.

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The type of argument is not numeric. |

# See also

[arr](4gl_arr.html), [int](4gl_int.html), [fix](4gl_fix.html), [abs](4gl_abs.html).

  

[Index](index.html)  [Home](getting-started_home.html)