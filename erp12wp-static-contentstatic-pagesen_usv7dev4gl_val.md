[Index](index.html)  [Home](getting-started_home.html)

Val

`val` transforms a string or a CLOB value that contains a decimal representation of a number to this number.

# Syntax

```
   val(STRING_EXPR)
```

* `STRING_EXPR` is a string expression.

# Examples

```
  Local Char MY_STRING1(50),MY_STRING2(50), MY_STRING3(50), MY_STRING4(50), MY_STRING5(50)
  Local Decimal MY_PI, MY_HUGE, MY_SMALL
  Local Integer MY_HUNDRED
  Local Shortint MY_NEGATIVE
  Local TinyInt MY_FOUR
  Local Double MY_ZERO
  Local Float MY_VALUE

  MY_STRING1="3.14159265358979323846264338328"
  MY_PI=val(MY_STRING1) : # An approximation of pi

  MY_STRING1="3.14159.2653"
  MY_PI=val(MY_STRING1) : # Another approximation of pi (3.14159, transformation stops at the second '.')

  MY_STRING2=" 100"
  MY_HUNDRED=val(MY_STRING2) : # 100

  MY_STRING3="-99"
  MY_NEGATIVE=val(MY_STRING3) : # -99

  MY_STRING4="4A"
  MY_FOUR=val(MY_STRING4) : # 4

  MY_STRING5="A4"
  MY_ZERO=val(MY_STRING4) : # 0 (the first character is not a digit or a leading space)

  MY_STRING5="- 4"
  MY_ZERO=val(MY_STRING5) : # 0 (a space cannot be inserted between the sign and the digits)

  MY_STRING5="1 E40"
  MY_VALUE=val(MY_STRING5) : # 1 (a space cannot be inserted between the digits and the "E")

  MY_STRING6="10000000000000000000000000000000000000000"
  MY_HUGE=val(MY_STRING6) : # 10^40

  MY_STRING6="1e-40"
  MY_SMALL=val(MY_STRING6) : # 10^-40
```

# Description

`val` returns a numeric value from a decimal representation of a number. Leading spaces are permitted, and the string is cut at the first character that is not a digit or the first dot (except if there is an exponent part with the format `digits`E`exponent`).

The type of the result depends on the number returned. It can be [TinyInt](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), or [Decimal](4gl_decimal.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a string. |

# See also

[num$](4gl_num$.html), [format$](4gl_format$.html).

  

[Index](index.html)  [Home](getting-started_home.html)