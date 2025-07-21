[Index](index.html)  [Home](getting-started_home.html)

Num$

`num$` transforms any data type (except BLOBs, CLOBs, and instance pointers) into a string that contains the representation of the data.

# Syntax

```
   num$(EXPR)
```

* `EXPR` is an expression.

# Examples

```
  Local Char MY_STRING1(50),MY_STRING2(50),MY_STRING3(50),MY_STRING4(50),MY_STRING5(50),MY_STRING6(50)
  MY_STRING1=num$(pi) : # Returns "3.14159265358979323846264338328"
  MY_STRING2=num$([25/12/2013]) : # Returns "25/12/2013"
  MY_STRING3=num$(getuuid) : # Returns UUID canonical representation , for instance "9646a691-47b8-45e2-b02d-2146093ba371"
  MY_STRING4=num$(datetime$): # Returns date time canonical representation, for instance "2013-12-16T10:37:17Z"
  MY_STRING5=num$("This is already a string") : # Returns "This is already a string"
  MY_STRING6=num$(10^37) : # Returns "1e37"
```

# Description

`num$` returns a string containing:  
\* The decimal representation of a number, without leading and trailing spaces.  
\* A representation in a DD/MM/YYYY date format.  
\* A canonical representation of an UUID or a date time value.  
\* The string itself if the parameter is a string.

If the argument of a numeric value exceeds 10^36, the scientific notation is used.

The type of the result is [Char](4gl_char.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is a BLOB, CLOB, or an instance pointer. |

# See also

[val](4gl_val.html), [format$](4gl_format$.html).

  

[Index](index.html)  [Home](getting-started_home.html)