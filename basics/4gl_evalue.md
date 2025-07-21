[Index](index.html)  [Home](getting-started_home.html)

Evalue

`evalue` evaluates a formula contained in a character string.

# Syntax

```
evalue(STRING_EXPR)
```

* `STRING_EXPR` is a string expression or a variable that returns the expression to be evaluated.

# Examples

```
# First simple example
  Local Integer FIELD1
  FIELD1=evalue("1+1") : # FIELD1 contains now 2

# Second example with an array of formulas
  Local Char FORMULA(100)(1..3)
  FORMULA(1)="1+2+3+4"
  FORMULA(2)="1+10+20"
  FORMULA(3)="5+4"
  FIELD1=evalue(FORMULA) : # FIELD1 contains now the result of "1+2+3+41+10+205+4" that gives 266

# Third example: check first if the formula is syntactically valid, then manage the error
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

# Fourth complex example with several evaluations (on meta data)
# Dump of the elements in a table (given by [G:abv]adxfname(i))
# The file is written in JSON
  Local File MYTABLE [MYT]
  Local Integer I,J,K,L,T
  Local Clbfile STRINGVAL(0)
  Openo filpath("TRA","MYTABLE","dmp"),0 Using [DMP]
  Wrseq '{ "MYTABLE" : [' Using [DMP]
  For [MYT]
    I+=1
    Wrseq string$(I>1,",")+ '{ "record_number" : '+num$(I)+"," Using [DMP]
    For J=1 to [G:MYT]nbzon-1 : # We skip the first element (Updtick)
      Wrseq string$(J>1,","); Using [DMP]
      # evaluate the dimension of the field
      K=evalue("dim([F:MYT]"+[G:MYT]adxfname(J)+")")
      # evaluate the type of the field
      T=evalue("type([F:MYT]"+[G:MYT]adxfname(J)+")")
      Wrseq '"'+[G:MYT]adxfname(J)+'" : ' Using [DMP]
      If K>1 : Wrseq '[' Using [DMP] : Endif
      For L=0 To K-1
        Wrseq string$(L>0,","); Using [DMP] : # Separator between the members of a collection 
        If find(T,1,2,4,5,6,7,8) : # Type that can be transformed by num$
          # evaluate the value of the column
          Wrseq num$(evalue("[F:MYT]"+[G:MYT]adxfname(J)+"("+num$(L)+")")) Using [DMP]
        Elsif find(T,522,523,524)
          Wrseq '"(Object)"' Using [DMP]
        Elsif T=3
          # evaluate the value of the column (date type)
          Wrseq '"'+format$("D:4Y[-]MM[-]DD",evalue("[F:MYT]"+[G:MYT]adxfname(J)+"("+num$(L)+")"))+'"' Using [DMP]
        Else
          # evaluate the value of the column (string or datetime)
          # In strings, the double quotes are replaced by spaces in order to avoid incorrect strings
          STRINGVAL=num$(evalue("[F:MYT]"+[G:MYT]adxfname(J)+"("+num$(L)+")"))
          Wrseq '"'+ctrans(STRINGVAL,'"',' ')+'"' Using [DMP]
        Endif
      Next L
      If K>1 : Wrseq ']' Using [DMP] : Endif
    Next J
    Wrseq "}" using [DMP]
  Next
  Wrseq "]}" using [DMP]
  Openo Using [DMP]
```

# Description

`evalue` evaluates the content of a character string as a formula and returns the result of the evaluation.

If the argument of `evalue` is a string array, the different lines in the array are concatenated and the result is evaluated.

# Comment

A second argument can be given for `evalue`, but this syntax is deprecated and must not be used.

# Associated errors

`evalue` contains a formula that is evaluated, and any error raised by the functions in the formula can occur. There is also the following error list:

| Error code | Description |
| --- | --- |
| 5 | Syntax error (the argument is not a valid formula). |
| 10 | The argument is not a string. |

# See also

[parse](4gl_parse.html).

  

[Index](index.html)  [Home](getting-started_home.html)