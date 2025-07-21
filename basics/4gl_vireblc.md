[Index](index.html)  [Home](getting-started_home.html)

Vireblc

`vireblc` allows you to suppress leading, trailing, or internal spaces of a string character or CLOB expression.

# Syntax

```
   vireblc(STRING_EXPR,INT_OPTION)
```

* `STRING_EXPR` is an expression returning a string or CLOB value.
* `INT_OPTION` is an integer expression that returns a value between 0 and 5.

# Examples

```
# Different options used
# I=0 will return "!Test    vireb !"
# I=1 will return "! Test    vireb!"
# I=2 will return "!Test    vireb!"
# I=3 will return "!Test!"
# I=4 will return "!Testvireb!"
# I=5 will return "! Test vireb !"
For I = 0 To 5
  RESULT(I)="!"+vireblc(" Test    vireb ", I)+"!"
Next I
```

# Description

`vireblc` suppresses spaces from a CLOB or a string according to the following options:

| Option | Effect |
| --- | --- |
| 0 | Suppresses the leading spaces. |
| 1 | Suppresses the trailing spaces. |
| 2 | Suppresses the leading spaces and the trailing spaces. |
| 3 | Suppresses the leading spaces, and cuts the string at the next space ("one word" cutting). |
| 4 | Suppresses all the spaces. |
| 5 | Suppresses consecutive spaces by a unique space. |

# Comments

The formatting options v0 to v5 for [format$](4gl_format$.html) function use the same values for suppressing the spaces when formatting a value.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The first argument is not a string, or the second argument is not an integer. |
| 50 | The second argument is not in [0,5] range. |

# See also

[Char](4gl_char.html), [format$](4gl_format$.html), [left$](4gl_left$.html), [mid$](4gl_mid$.html), [right$](4gl_right$.html), [seg$](4gl_seg$.html).

  

[Index](index.html)  [Home](getting-started_home.html)