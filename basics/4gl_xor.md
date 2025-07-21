[Index](index.html)  [Home](getting-started_home.html)

Xor

`xor` performs an exclusive logical 'or' between two boolean values.

# Syntax

```
  EXP_NUM1 xor EXP_NUM2
  EXP_NUM1 ? EXP_NUM2
```

* `EXP_NUM1` and `EXP_NUM2` are two numeric values. Any value that is not null is considered as true, while any null value is considered as false.

# Examples

```
CODECODE CODE 
   # Test : does I=1 and J<>2, or I<>1 and J=2 ?
   If I = 1 xor J = 2
     CONDITION_RESULT="the condition is true"
   Else
     CONDITION_RESULT="the condition is false"
   Endif
```

# Description and comments

`xor` returns a boolean result that is 0 or 1, 0 being the value `false` and 1 to value `true`.  
The result depends on the value of the following decision table:

| Value of EXP\_NUM1 | Value of EXP\_NUM2 | Value of (EXP\_NUM1 or EXP\_NUM2) |
| --- | --- | --- |
| false (0) | false (0) | 0 (false) |
| false (0) | true (not equal to 0) | 1 (true) |
| true (not equal to 0) | false (0) | 1 (true) |
| true (not equal to 0) | true (not equal to 0) | 0 (false) |

# Comments:

`or` can be abbreviated as `?`.

# Associated errors

| Error | Description |
| --- | --- |
| 10 | Arguments are not numeric. |

# See also

[and](4gl_and.html), [or](4gl_or.html), [not](4gl_not.html).

  

[Index](index.html)  [Home](getting-started_home.html)