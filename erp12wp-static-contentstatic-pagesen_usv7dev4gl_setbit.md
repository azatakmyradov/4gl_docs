[Index](index.html)  [Home](getting-started_home.html)

Setbit

`setbit` set a bit of an integer to 0 or 1. The result is an integer.

# Syntax

```
  setbit( INT_VALUE, BIT_TO_SET, BIT_VALUE)
```

* `INT_VALUE` Integer to set the bit on. (TinyInt, ShortInt, Integer)
* `BIT_TO_SET` Number of the bit to set. Bit numbers start at 1.
* `BIT_VALUE` 0 or 1

# Example

```
Local Integer INT_VALUE, RESULT
INT_VALUE = 0
RESULT = setBit(INT_VALUE,4,1)    # Result equals 2^(4-1) = 8, bit numbers start at 1, not 0.
```

# See also

[getbit](4gl_getbit.html).

  

[Index](index.html)  [Home](getting-started_home.html)