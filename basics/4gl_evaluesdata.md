[Index](index.html)  [Home](getting-started_home.html)

Evaluesdata

This function defines a filtering condition on a database query. The condition is expressed in [SData *where* syntax](https://sage.github.io/SData-2.0/pages/core/0212/).

This function is only valid inside a *Where* clause of a database instruction (`For`, `Filter`, `File`, `Link`).

# Syntax

```
Where evalueSData(EXPRESSION, VARIABLES, COLUMNS)
```

* `EXPRESSION` is a filter expressed in *SData where syntax*.
* `VARIABLES` is an array containing the variable names used in the filter.
* `COLUMNS` is an array containing the database columns referenced by the variable names.

# Example

```
Local File MYTABLE [MYT]
Local Char VARS(20)(1..3), COLS(20)(1..3)
VARS(1)="country" : VARS(2)="city" : VARS(3)="total"
COLS(1)="[MYT]COUNTRYCODE" : COLS(2)="[MYT]CITYNAME" : COLS(3)="[MYT]AMOUNT"

# The condition
Filter [MYT] Where evalueSData(
&            "(city in 'London','Paris') and (total between 1 and 10) and country ne 'BE'"
&            , VARS, COLS)
# is equivalent to
Filter [MYT] Where find(CITYNAME,'London','Paris') and (AMOUNT>=1 and AMOUNT<=100) and COUNTRYCODE<>"BE"
```

# Comments

This function only supports the following subset of the SData Query language:

* String, numeric, date and datetime literals (for example, 'Hello "World"',"I'm tired", 3.14, @1959-05-29@, @2008-05-19T16:41:00Z@).
* Parentheses
* The following operators and functions:

| Keyword | Description | Example |
| --- | --- | --- |
| lt | less than | amount lt 5000 |
| gt | greather than | amount gt 3000 |
| le | less or equal | amount le 4500 |
| ge | greater or equal | amount ge 7800 |
| eq | equal | amount eq 3000 |
| ne | not equal | amount ne 3000 |
| between ... and... | between two values | amount between 20 and 30 |
| in | contained in a list of values | amount in (3,14,15,9,26) |
| like | matches a string pattern | name like '%PONT%' |
| and | logical and | amount ne 300 and amount ne 500 |
| or | logical or | amount eq 300 or amount eq 500 |
| abs | absolute value | abs(amount) eq 6 |
| ascii | ASCII code of first character | ascii(countrycode) eq 32 |
| char | single char from ASCII code | countrycode eq char(32) |
| div | division | amount div 2 eq 3 |
| left(str,len) | leftmost `len` characters from str; `str` if less than `len` characters | left(name,3)="Doe" |
| lower(str) | converts str to lower case | lower(name)="doe" |
| upper(str) | converts str to upper case | lower(name)="DOE" |
| mod | modulus | number mod 2 eq 0 |
| mul | multiplication | amount mul 3 eq 15 |
| not | negation | not (amount eq 3) |
| pow | power | amount pow 3 eq 125 |
| right(str,len) | rightmost `len` characters from `str`; `str` if less than `len` characters | right(name,2)='oe' |
| substring(str,index,len) | substring starting at `start` and containing `len` characters; start is 1-based | substring(name,4,5)='ti' |

# See also

[ExecSql](4gl_execsql.html)

  

[Index](index.html)  [Home](getting-started_home.html)