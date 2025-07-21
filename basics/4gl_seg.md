[Index](index.html)  [Home](getting-started_home.html)

Seg$

`seg$` extracts a substring defined by the starting position and the ending position out of a CLOB or a string.

# Syntax

```
   seg$(EXP_STRING,EXP_POS1,EXP_POS2)
```

* `EXP_STRING` is an expression returning a CLOB or string value.
* `EXP_POS1` is an expression returning an integer value that is the position of the first character to be extracted.
* `EXP_POS2` is an expression returning an integer value that is the position of the last character to be extracted.

# Examples

```
   # Extraction Of 3 characters from latin alphabet
   Local Char ALPHABET(26), DEF(20), WXYZ(20)
   ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
   DEF=seg$(ALPHABET,4,6) : # DEF contains "DEF"
   WXYZ=mid$(ALPHABET,23,26) : # DEF contains "WXYZ"

   # inserts a space between every character in a string
   MY_TITLE="WELCOME"
   MY_TITLE=sigma(I=1,len(MY_TITRE),mid$(TITRE,I,I)+" ")
   # Now MY_TITLE contains "W E L C O M E "
```

# Description

The function `seg$(EXP_STRING,EXP_POS,EXP_NB)` extracts characters from the `EXP_STRING` string starting at the position `EXP_POS1` until the position `EXP_POS2`.

The type of result is [Char](4gl_char.html).

# Comments

* If `EXP_POS1` is greater than the length of the string, `seg$(EXP_STRING,EXP_POS1,EXP_POS2)` returns the null string `""`.
* If `EXP_POS2` is greater than the length of the string, only the remaining characters will be extracted, and the length of the result will be smaller than `EXP_POS2-EXP_POS1+1`.
* If `EXP_POS2` is smaller than `EXP_POS1`, `seg$(EXP_STRING,EXP_POS1,EXP_POS2)` returns the null string `""`.
* `seg$(EXP_STRING,EXP_POS1,EXP_POS2)` is equivalent to `mid$(EXP_STRING,EXP_POS1,EXP_POS2-EXP_POS1+1)`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The type of argument is not correct. |
| 50 | At least one of the positions is negative. |

# See also

[right$](4gl_right$.html), [left$](4gl_left$.html), [mid$](4gl_mid$.html), [len](4gl_len.html).

  

[Index](index.html)  [Home](getting-started_home.html)