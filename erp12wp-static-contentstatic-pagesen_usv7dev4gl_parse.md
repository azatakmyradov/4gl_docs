[Index](index.html)  [Home](getting-started_home.html)

Parse

`parse` parses a formula contained in a character string and returns an error value if the formula is not syntactically correct.

# Syntax

```
   parse(STRING_EXPR)
```

* `STRING_EXPR` is a string expression or a variable that returns the expression to be parsed.

# Examples

```
# First simple example
  Local Integer FIELD1
  IF_OK=parse("1+1") : # FIELD1 contains now 0 (ok)
  IF_OK=parse("1+")  : # FIELD1 contains now 5 (illegal character)

# Second example: check first if the formula is syntactically valid, then manage the error
# Returns the result of the evaluation in a string
# If an error occurs, ERROR_CODE is not null and the result is an empty string
Subprog EVALUE(FORMULA,RESULT,ERROR_CODE)
  Value Char FORMULA()
  Variable Char RESULT
  Variable Integer ERROR_CODE

# Is the formula correct?
  ERROR_CODE=parse(FORMULA)
  If ERROR_CODE<>0 : RESULT="" : End : Endif

# Handle the errors
  Onerrgo ERR_EVALUE
  RESULT=num$(evalue(FORMULA))
  ERROR_CODE=0
End

# Error handling
$ERR_EVALUE
  RESULT=""
  ERROR_CODE=errn
End
```

# Description

`parse` parses the content of a character string as a formula and returns 0 if the syntax is OK. Otherwise, it returns an error code (usually 5: incorrect character).

If the argument of `parse` is a string array, the different lines in the array are concatenated and the result is parsed.

# Comment

A second argument can be given for `parse`, but this syntax is deprecated and must not be used.

# Associated errors

| Error code | Description. |
| --- | --- |
| 10 | The argument is not a string. |

# See also

[evalue](4gl_evalue.html).

  

[Index](index.html)  [Home](getting-started_home.html)