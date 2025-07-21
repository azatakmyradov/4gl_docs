[Index](index.html)  [Home](getting-started_home.html)

Exp

`exp` returns the exponential function of its argument.

# Syntax

```
   exp(NUMERIC_EXPR)
```

* `NUMERIC_EXPR` is an expression returning a numeric value.

# Examples

```
   Y = exp(0) : # Returns 1
   Y = exp(pi): # Returns 23.06926...
```

# Description

This function returns the exponential (power of e) of its argument.

[ln](4gl_ln.html) is the reverse function of `exp`.  
The type of result is [Double](4gl_double.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | the argument is not numeric. |
| 13 | Calculation overflow (x is too big - over 184,89995462). |

# See also

[ln](4gl_ln.html), [log](4gl_log.html).

  

[Index](index.html)  [Home](getting-started_home.html)