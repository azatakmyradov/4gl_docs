[Index](index.html)  [Home](getting-started_home.html)

Pat

`pat` allows you to check the conformity of a string according to a pattern.

# Syntax

```
   pat(EXPR_STR,EXPR_PAT)
```

* `EXPR_STR` is a string or CLOB expression that contains the string to be tested.
* `EXPR_PAT` is a string or CLOB expression that contains the pattern used for the verification.

# Examples

```
   # Does the string MY_STRING contain the word SAGE ?
    If pat(MY_STRING, "*SAGE*")
       # SAGE is contained in the MY_STRING value
    Endif

   # Verify that MY_STRING starts with a letter, followed by exactly 3 characters and a digit
    If pat(MY_STRING, "!???#")<>0
       # pattern verified
    Endif

   # Use a "like" clause on the database
   Local File BPCUSTOMER Where pat(BPCNAM,"*SAGE*")<>0 : # Where BPCNAM like '%SAGE%'

   # If <>0 is not given, the result is the same, but the filter is not transmitted to the database
   # abnd is performed by the engine, which is less efficient
   Local File BPCUSTOMER Where pat(BPCNAM,"*SAGE*") : # X3 engine filter
```

# Description

`pat` allows you to verify that a string corresponds to a pattern. A pattern is a set of characters including meta characters.

Any character that is not a meta character must correspond to the character found in the string. The meta characters are the following:

* `*` represents any number of characters (possibly no character).
* `?` represents exactly one character.
* `#` represents a digit.
* `!` represents a letter.

`pat` returns an [Integer](4gl_integer.html) value that can be 1 (if the string is conform), or 0 (if the string does not correspond to the pattern).

In a [where](4gl_where.html) clause used on [File](4gl_file.html) or [Filter](4gl_filter.html), the result of the function [pat](4gl_pat.html) must be followed by `=0` or `<>0` to send to the database a "like" or a "not like" condition.

# Comment

The function [format$](4gl_format$.html) can also be used in complex cases to check the validity of a string against a format. The result of the formatting will be a blank string if the format does not work.

For example, if you need to check that a string has three uppercase letters followed by 2 digits, the corresponding test can be written:

```
  If format$("KA:3A3#",MY_STRING)=space$(6)
    # MY_STRING is not conform to the format
  Endif
```

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | At least one of the arguments is not a string. |

# See also

[format$](4gl_format$.html).

  

[Index](index.html)  [Home](getting-started_home.html)