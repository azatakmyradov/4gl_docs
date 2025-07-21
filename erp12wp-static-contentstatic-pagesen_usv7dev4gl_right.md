[Index](index.html)  [Home](getting-started_home.html)

Right$

`right$` extracts a substring of a string starting from a given position (the right side).

# Syntax

```
   right$(EXPR_STRING,EXPR_POS)
```

* `EXPR_STRING` is an expression that gives the string from which the substring is extracted.
* `EXPR_POS` gives the position where the extraction starts.

# Examples

```
   # Extraction of the letters starting from 12th position of the latin alphabet
    ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    AFTER_TWELVE=right$(ALPHABET, 12) : # Returns "LMNOPQRSTUVWXYZ"

   # Computes the length of a string
   # It would be preferable to use len!!!
   STRING_LEN = 0
   While right$(MY_STRING,STRING_LEN+1) <> "" : STRING_LEN+=1 : Wend

   # Extracts the character from a string starting at position 32
   # the result string will become an empty string if its original length was smaller than 32
   MY_STRING=right$(MY_STRING,32)

   # Extracts the characters from a clob starting at position 800
   # the clob will become an empty string if its original length was smaller than 800
   MY_CLOB=right$(MY_CLOB,800)
```

# Description

The function `right$` extracts the characters of a string, starting at `EXPR_POS` position. Based on the length of the result, the type of the result is [Char](4gl_char.html) or [Clbfile](4gl_clbfile.html).

# Comments

* If `EXPR_POS` is equal to 0 or 1, the whole string is returned.
* If `EXPR_POS` is greater than the length of the string, the null string `""` is returned.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The first argument is not a string, or the second argument is not numeric. |
| 50 | The second argument is negative. |

# See also

[mid$](4gl_mid$.html), [left$](4gl_left$.html), [seg$](4gl_seg$.html), [len](4gl_len.html).

  

[Index](index.html)  [Home](getting-started_home.html)