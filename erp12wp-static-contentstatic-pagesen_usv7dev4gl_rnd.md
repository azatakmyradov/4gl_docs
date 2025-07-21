[Index](index.html)  [Home](getting-started_home.html)

Rnd

`rnd(x)` returns a random number between '0' and 'x' (x excluded).

# Syntax

```
   rnd(EXP_NUM)
```

* `EXP_NUM` is an expression returning a numeric value.

# Examples

```
   # Let's simulate a dice throw
    DICE_VALUE = int(rnd(6)) + 1

   # Let's create a random string of 1 to 20 characters containing random Latin alphabetic letter
    CH_HASARD = sigma(1, 1+int(rnd(20)), chr$(int(rnd(25))+ascii("A")))
```

# Description

`rnd(X)` uses the usual random function (on Unix, it is drand48()).  
The method uses the series calculated by `X(N+1)=A*X(N)+C (modulo M)` with M=2^48, A=25214903917, C=11. The initial value depends on the current time when the process starts.

The numbers returned have a uniform distribution on the interval. If integers are required, the functions [int](4gl_int.html), [fix](4gl_fix.html), or [arr](4gl_arr.html) can be used.

The type of result is [Double](4gl_double.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |

# See also

[int](4gl_int.html), [arr](4gl_arr.html), [fix](4gl_fix.html).

  

[Index](index.html)  [Home](getting-started_home.html)