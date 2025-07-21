[Index](index.html)  [Home](getting-started_home.html)

Len

`len` returns the length (in number of characters) of a string, BLOB, or CLOB value.

# Syntax

```
   len(STRING_EXPR)
```

* `STRING_EXPR` is an expression returning a string or CLOB value, or a BLOB variable.

# Examples

```
   # Add spaces to a string to bring it to 25 characters
   # If the length is over 25 characters, the string remains unchanged
   If len(MY_STRING)<25
      MY_STRING += space$(25_len(MY_STRING))
   Endif

   # Select the lines in a blob table where the blob are defined
    Local File ABLOB [ABB]
    For [ABB] Where len(BLOB)<>0
      # In the loop, the blobs are defined
    Next

   # Let's return the value given by DEFAULT_STRING if VALUE_STRING is empty
    VALUE_STRING+=string$(len(VALUE_STRING)=0,DEFAULT_STRING)
```

# Description

`len` returns the length of a character string, of a CLOB or of a BLOB. The type of result is [Integer](4gl_integer.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not string, CLOB, or BLOB. |

# See also

[string$](4gl_string$.html), [space$](4gl_space$.html), [left$](4gl_left$.html), [right$](4gl_right$.html), [mid$](4gl_mid$.html), [instr](4gl_instr.html), [seg$](4gl_seg$.html).

  

[Index](index.html)  [Home](getting-started_home.html)