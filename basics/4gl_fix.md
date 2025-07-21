[Index](index.html)  [Home](getting-started_home.html)

Fix

`fix` truncates the decimals of a number.

# Syntax

```
   fix(NUM_EXPR)
```

* `NUM_EXPR` is an expression that returns a numeric value.

# Examples

```
   X = fix(pi)) : # X value is 3
   X = fix(-pi) : # X value is -3
   X = int(pi)  : # X value is 3 
   X = int(-pi) : # X value is -4
```

# Description

`fix` returns the value of 'X' without the decimals.

The result has an [Integer](4gl_integer.html) or [Decimal](4gl_decimal.html) type depending whether the result is in the [-2^31, 2^31-1] range.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |

# See also

[int](4gl_int.html), [ar2](4gl_ar2.html), [arr](4gl_arr.html), [Integer](4gl_integer.html), [mod](4gl_mod.html).

  

[Index](index.html)  [Home](getting-started_home.html)