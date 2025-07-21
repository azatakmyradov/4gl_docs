[Index](index.html)  [Home](getting-started_home.html)

Mod

`mod` returns the remainder of the division of one number by another.

# Syntax

```
   mod(EXP_NUM1,EXP_NUM2)
```

# Examples

```
   # Is the Integer MY_INTEGER even or odd?
   If mod(MY_INTEGER,2)=0
     # MY_INTEGER is even
   Else
     # MY_INTEGER is odd
   Endif

   # Mod can be used with decimal values
   Y = mod(1.1, 0.3)
   Y = 0.2
```

# Description

`mod(X,Y)` returns:

* **mod(X,0) = X** for Y=0 in mod(X,Y)
* **mod(X,Y) = X-Y\*fix(X/Y)** for all non-zero values of X,Y

The type of the result is determined by the type of the assignment variable.

```
   Local Decimal MY_DECIMAL 
   MY_DECIMAL = mod(3.7,2)    # Type assigned is decimal and value = 1.7

   Local Integer MY_INTEGER
   MY_INTEGER = mod(3.7,2)    # Type assigned is integer and value = 1
```

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | At least one of the arguments is not numeric. |

# See also

[fix](4gl_fix.html).

  

[Index](index.html)  [Home](getting-started_home.html)