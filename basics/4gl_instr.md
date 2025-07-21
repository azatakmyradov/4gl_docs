[Index](index.html)  [Home](getting-started_home.html)

Instr

`instr` searches for a given substring in a string, starting at a given position.

# Syntax

```
   instr(EXPR_POSITION,EXPR_STRING,EXPR_SUBSTRING)
```

* `EXPR_POSITION` is a positive integer expression that defines the first position to search in the string.
* `EXPR_STRING` is a string expression in which the substring is searched.
* `EXPR_SUBSTRING` is a string expression that defines the string to be searched.

# Examples

```
   # Search for GHI substring in a string
   Local Integer I
   I=substring(1,"ABCDEFGHIJKLMNOPQRSTUVWXYZ","GHI") : # I equals 7 now

   # Count the number of occurrences of the word defined by SEARCH_WORD in a TEXT variable
   # The result is computed in OCCURRENCES value
   Funprog COUNT_WORDS(SEARCH_WORD,TEXT)
   Value Char SEARCH_WORD()
   Variable Clbfile TEXT()
   Local Integer OCCURRENCES,I,K
     K=len(SEARCH_WORD) : I = 1-K : OCCURRENCES = -1
     Repeat I = instr(I+K, TEXT, SEARCH_WORD) : OCCURRENCES += 1 : Until I = 0
   End OCCURRENCES
```

# Description

`instr` searches a substring in a string or a CLOB from an initial position and returns the position (in number of characters) of the first occurrence found. If the substring is not found, `instr` returns 0.

The type of the result is [Integer](4gl_integer.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The position argument is not numeric. The string or substring parameter is not a string or a CLOB. |
| 50 | The position is negative |

# See also

[left$](4gl_left$.html), [right$](4gl_right$.html), [string$](4gl_string$.html), [space$](4gl_space$.html), [mid$](4gl_mid$.html), [vireblc](4gl_vireblc.html).

  

[Index](index.html)  [Home](getting-started_home.html)