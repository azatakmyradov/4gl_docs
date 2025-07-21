[Index](index.html)  [Home](getting-started_home.html)

And

`and` performs a logical 'and' between two boolean values.

# Syntax

```
  EXP_NUM1 and EXP_NUM2
  EXP_NUM1 & EXP_NUM2
```

* `EXP_NUM1` and `EXP_NUM2` are two numeric values. Any value that is not null is considered as true, while any null value is considered as false.

# Examples

```
CODECODE CODE 
   # Test : does I=1 and J=2 ?
   If I = 1 and J = 2
     CONDITION_RESULT="the condition is true"
   Else
     CONDITION_RESULT="the condition is false"
   Endif

  # Loop as long as integers I and J are non-null, avoiding an infinite loop.
   If I < 0 and J < 0
       Return
   Else
     While I and J
       I -= 1 : J -= 1          :# Decrement I and J
     Wend
   Endif
```

# Description and comments

`and` returns a boolean result that is 0 or 1, 0 being the value `false` and 1 to value `true`.  
The result depends on the value of the following decision table:

| Value of EXP\_NUM1 | Value of EXP\_NUM2 | Value of (EXP\_NUM1 and EXP\_NUM2) |
| --- | --- | --- |
| false (0) | false (0) | 0 (false) |
| false (0) | true (not equal to 0) | 0 (false) |
| true (not equal to 0) | false (0) | 0 (false) |
| true (not equal to 0) | true (not equal to 0) | 1 (true) |

# Comments:

* `and` can be abbreviated as `&`.
* When an expression is made with several sub-expressions associated with an `and`, the first expression is evaluated first; if false, the next expression is not evaluated, and the result returns immediately as an error. This allows writing code such as the following example:

```
  # Verifies if a formula returns a not null numeric value. Returns 1 if it is the case and 0 in all the other cases
  # If FORMULA is empty, the other elements of the condition are not computed and 0 is returned
  # If FORMULA is not empty, and if parse returns a not null value, MY_FORMULA is not valid and therefore not evaluated
  Funprog IS_FORMULA_NUMERIC(MY_FORMULA)
  Value Char MY_FORMULA()

  If MY_FORMULA<>"" & parse(MY_FORMULA)=0 & val(num$(evalue(MY_FORMULA)))<>0
    End 1
  Endif

End 0
```

# Associated errors

| Error | Description |
| --- | --- |
| 10 | Arguments are not numeric. |

# See also

[or](4gl_or.html), [xor](4gl_xor.html), [not](4gl_not.html).

  

[Index](index.html)  [Home](getting-started_home.html)