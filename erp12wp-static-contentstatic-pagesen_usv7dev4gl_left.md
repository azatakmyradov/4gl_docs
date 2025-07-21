[Index](index.html)  [Home](getting-started_home.html)

Left$

`left$` extracts a sub-string of a string starting from the beginning (the left side).

# Syntax

```
   left$(EXPR_STRING,EXPR_LEN)
```

* `EXPR_STRING` is an expression that gives the string from which the substring is extracted.
* `EXPR_LEN` gives the number of characters to be extracted.

# Examples

```
   # Extraction of the first 5 letter of the latin alphabet
    ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    FIRST_FIVE=left$(ALPHABET, 5) : # Returns "ABCDE"

   # Computes the length of a string
   # It would be preferable to use len!!!
   STRING_LEN = 0
   While left$(MY_STRING,STRING_LEN) <> MY_STRING : STRING_LEN+=1 : Wend

   # Truncates a string to a maximum length of 32
   # the string remains unchanged if its length was smaller than 32
   MY_STRING=left$(MY_STRING,32)

   # Truncates a clob to a maximum length of 800
   # the clob remains unchanged if its length was smaller than 800
   MY_CLOB=left$(MY_CLOB,800)
```

# Description

The function `left$` extracts the first `EXPR_LEN` characters of a string or a CLOB. According to `EXPR_LEN`, the type of the result is [Char](4gl_char.html) or [Clbfile](4gl_clbfile.html).

# Comments

* If `EXPR_LEN` is equal to 0, the empty string `""` is returned.
* If `EXPR_LEN` is greater than the length of the string, the string is returned.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The first argument is not a string, or the second argument is not numeric. |
| 50 | The second argument is negative. |

# See also

[mid$](4gl_mid$.html), [right$](4gl_right$.html), [seg$](4gl_seg$.html), [len](4gl_len.html).

  

[Index](index.html)  [Home](getting-started_home.html)