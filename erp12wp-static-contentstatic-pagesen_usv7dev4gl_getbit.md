[Index](index.html)  [Home](getting-started_home.html)

Getbit

`getbit` returns the bit value of a bit from an integer. The result is an integer that can have a value of 0 or 1.

# Syntax

```
  getBit( INT_VALUE, BIT_TO_GET)
```

* `INT_VALUE` Integer to get the bit from. (TinyInt, ShortInt, Integer)
* `BIT_TO_GET` Number of the bit to return. Bit numbers start at 1.

# Syntax

```
  getbit(E,N)
```

# Example

```
 Local Integer INT_VALUE,RESULT
 INT_VALUE=8
 RESULT = getBit(INT_VALUE,4)    # RESULT = 1. Note Bit numbers start at 1, not 0. That  is 2^(4-1)=8
```

# See also

[setbit](4gl_setbit.html).

  

[Index](index.html)  [Home](getting-started_home.html)