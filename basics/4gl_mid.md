[Index](index.html)  [Home](getting-started_home.html)

Mid$

`mid$` extracts a sub-string defined by the position and a number of characters out of a CLOB or a string.

# Syntax

```
   mid$(EXP_STRING,EXP_POS,EXP_NB)
```

* `EXP_STRING` is an expression returning a CLOB or string value.
* `EXP_POS` is an expression returning an integer value that is the position of the first character to be extracted.
* `EXP_NB` is an expression returning an integer value that defines the number of characters to be extracted.

# Examples

```
   # Extraction Of 3 characters from latin alphabet
   Local Char ALPHABET(26), DEF(20), WXYZ(20)
   ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
   DEF=mid$(ALPHABET,4,3) : # DEF contains "DEF"
   WXYZ=mid$(ALPHABET,23,10) : # DEF contains "WXYZ"

   # inserts a space between every character in a string
   MY_TITLE="WELCOME"
   MY_TITLE=sigma(I=1,len(MY_TITRE),mid$(TITRE,I,1)+" ")
   # Now MY_TITLE contains "W E L C O M E "
```

# Description

The function `mid$(EXP_STRING,EXP_POS,EXP_NB)` extracts up to `EXP_NB` characters from the `EXP_STRING` string starting at the position `EXP_POS`.

The type of result is [Char](4gl_char.html).

# Comments

* If `EXP_POS` is greater than the length of the string, `mid$(EXP_STRING,EXP_POS,EXP_NB)` returns the null string `""`.
* If `EXP_NB` is greater than the number of remaining characters, only the remaining characters will be extracted, and the length of the result is smaller than `EXP_NB`.
* `mid$(EXP_STRING,EXP_POS,EXP_NB)` is equivalent to `seg$(EXP_STRING,EXP_POS+EXP_NB-1)`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The arguments type are not correct. |
| 50 | The position or the length is negative. |

# See also

[right$](4gl_right$.html), [left$](4gl_left$.html), [seg$](4gl_seg$.html), [len](4gl_len.html).

  

[Index](index.html)  [Home](getting-started_home.html)