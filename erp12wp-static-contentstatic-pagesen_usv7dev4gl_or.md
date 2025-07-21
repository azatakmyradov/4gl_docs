[Index](index.html)  [Home](getting-started_home.html)

Or

`or` performs a logical 'or' between two boolean values.

# Syntax

```
  EXP_NUM1 or EXP_NUM2
  EXP_NUM1 | EXP_NUM2
```

* `EXP_NUM1` and `EXP_NUM2` are two numeric values. Any value that is not null is considered as true, while any null value is considered as false.

# Examples

```
CODECODE CODE 
   # Test : does I=1 or J=2 ?
   If I = 1 or J = 2
     CONDITION_RESULT="the condition is true"
   Else
     CONDITION_RESULT="the condition is false"
   Endif

  # Loop as long as integers I or J are non-null, avoiding an infinite loop.
   If I < 0 or J < 0
       Return
   Else
     While I and J
       I -= 1 : J -= 1          :# Decrement I and J
     Wend
   Endif
```

# Description and comments

`or` returns a boolean result that is 0 or 1, 0 being the value `false` and 1 to value `true`.  
The result depends on the value of the following table:

| Value of EXP\_NUM1 | Value of EXP\_NUM2 | Value of (EXP\_NUM1 or EXP\_NUM2) |
| --- | --- | --- |
| false (0) | false (0) | 0 (false). |
| false (0) | true (not equal to 0) | 1 (true). |
| true (not equal to 0) | false (0) | 1 (true). |
| true (not equal to 0) | true (not equal to 0) | 1 (true). |

# Comments:

* `or` can be abbreviated as `|`.
* When an expression is made with several subexpressions associated with an `and`, the first expression is evaluated first; if true, the next expression is not evaluated, and the result returns immediately true. This allows writing code such as the following example:

```
  # Returns 1 if a not zero default value is given, otherwise evaluate a formula to verify a not zero value
  Funprog GET_VALUE(MY_FORMULA,DEFAULT_VALUE)
  Value Char MY_FORMULA()
  Value Integer DEFAULT_VALUE

  If DEFAULT_VALUE<>0 or evalue(MY_FORMULA)))<>0
    End 1
  Endif
End 0
```

# Associated errors

| Error | Description |
| --- | --- |
| 10 | Arguments are not numeric. |

# See also

[and](4gl_and.html), [xor](4gl_xor.html), [not](4gl_not.html).

  

[Index](index.html)  [Home](getting-started_home.html)