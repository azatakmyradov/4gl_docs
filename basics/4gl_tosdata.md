[Index](index.html)  [Home](getting-started_home.html)

Tosdata

This function returns a string value containing an [SData *where* syntax](https://sage.github.io/SData-2.0/pages/core/0212/) corresponding to a Sage X3 valid condition.

## Syntax

```
STRING=toSData(VARIABLES, SDATA_VAR, EXPRESSION)
```

* `VARIABLES` is an array containing the variable names used in the condition.
* `SDATA_VAR` is an array containing the corresponding variable names used in the SData where resulting condition.
* `EXPRESSION` is a Sage X3 valid condition expressed in *X3 syntax*.

## Example

```
Local Char VARS(20)(1..3), COLS(20)(1..3), MY_EXPRESSION(200),SDATA_EXPRESSION(200)
VARS(1)="country" : VARS(2)="city" : VARS(3)="total"
COLS(1)="COUNTRYCODE" : COLS(2)="CITYNAME" : COLS(3)="AMOUNT"

# Transform the expression
MY_EXPRESSION="find(CITYNAME,'London','Paris')<>0 and (AMOUNT>=1 and AMOUNT<=100) and COUNTRYCODE<>'BE'"
SDATA_EXPRESSION=toSData(COLS,VARS,MY_EXPRESSION)

# The contents of SDATA_EXPRESSION is now:
#  "(city in 'London','Paris') and (total between 1 and 10) and country ne 'BE'"
```

## Comments

This function only supports the following subset of the Sage X3 syntax:

* String, numeric, date, and datetime literals. For example, 'Hello "World"',"I'm tired", 3.14, @1959-05-29@, @2008-05-19T16:41:00Z@
* Parentheses
* The following operators: +, -, !, \*, /, >, >=, <, =, <=, =, and, or
* The following functions: `find`, `pat`, `mod`, `left$`, `right$`, `mid$`, `seg$`, `tolower`, `toupper`, `ascii`, `chr$`, `abs`, `arr`, `year`, `day`, `month`

Expressions that are not based on unary expressions are not accepted and trigger an error. The following table provides incorrect syntaxes and the correct equivalent syntaxes:

| Incorrect syntax | Correct syntax |
| --- | --- |
| pat(NAME,"\*A\*") | pat(NAME,"\*A\*")<>0 |
| find(NAME,"A","B","C") | find(NAME,"A","B","C")<>0 |
| AMOUNT | AMOUNT<>0 |

### See also

[evalueSData](4gl_evaluesdata.html)

  

[Index](index.html)  [Home](getting-started_home.html)