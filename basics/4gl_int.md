[Index](index.html)  [Home](getting-started_home.html)

Int

`int` returns the integer part of a number.

# Syntax

```
   int(NUMERIC_EXPR)
```

* `NUMERIC_EXPR` is an expression returning a numeric value.

# Examples

```
   FRAC_PI=pi-int(pi)  :# returns 0.14159265358...
   X = int(-pi)        :# X = -4
   Y = int(-5)         :# Y = -5
```

# Description

`int(X)` returns:

* [fix](4gl_fix.html)(X) : if 'X' is positive, null or integer;
* [fix](4gl_fix.html)(X)-1 : if 'X' is strictly negative and not integer.

The type of result is [Integer](4gl_integer.html) or [Decimal](4gl_decimal.html) depending whether the result is in the [ -2^31, 2^31-1 ] range.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |

# See also

[fix](4gl_fix.html), [ar2](4gl_ar2.html), [arr](4gl_arr.html), [Integer](4gl_integer.html), [mod](4gl_mod.html).

  

[Index](index.html)  [Home](getting-started_home.html)