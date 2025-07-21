[Index](index.html)  [Home](getting-started_home.html)

Arr

`ar2` is a function that rounds a number to a specified increment. The method used is the method known as [half away from zero.](https://en.wikipedia.org/wiki/rounding#Tie-breaking)

# Syntax

```
  arr(NUMEXPR1, NUMEXPR2)
```

* `NUMEXPR1` is a numeric expression that represents the number to be rounded.
* `NUMEXPR2` is a numeric expression that represents the rounding increment.

# Examples

```
   # Rounding to an integer value
    RESULT = arr((11/7),1)

   # Rounding to one decimal
    RESULT = arr((11/7),0.1)

   # Swiss VAT computation (rounded to 5 centimes)
    AMT_TAXINCLUDED = arr( AMT_BASE * (1+TAX_RATE/100), 0.05 )

   # No rounding is done here
    PI_MAX_PREC=arr(pi,0)

   # Rounding to the integer for a negative value
    ROUNDED = arr(-40.5,1) : # ROUNDED is equal to -41
```

# Description

If Y is not equal to 0, `arr` (X,Y) returns a rounded value that can be also calculated by:  
\* [sgn](4gl_sgn.html)(X)*[int](4gl_int.html)([abs](4gl_abs.html)(X)/Y+0.5)/*Y  
\* `arr`(X/Y,1)\*Y

If Y is equal to 0, `arr`(X) returns X.

The type ID of the result is [Decimal](4gl_decimal.html).

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The type of argument is not numeric. |

# See also

[ar2](4gl_ar2.html), [sgn](4gl_sgn.html), [abs](4gl_abs.html), [int](4gl_int.html), [fix](4gl_fix.html), [abs](4gl_abs.html).

  

[Index](index.html)  [Home](getting-started_home.html)