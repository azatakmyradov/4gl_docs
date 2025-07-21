[Index](index.html)  [Home](getting-started_home.html)

Space$

`space$` returns a string containing a number of spaces given by its argument.

# Syntax

```
   space$(EXP_NB)
```

* `EXP_NB` is an integer expression that returns the number of spaces in the returned string.

# Examples

```
   # Format a string on 35 characters (left aligned, right aligned)
   MY_STRING="This is a string"
   If len(MY_STRING)<=35
     LEFT_ALIGNED=MY_STRING+space$(35-len(MY_STRING))
     RIGHT_ALIGNED=space$(35-len(MY_STRING))+MY_STRING
   Endif

   # space$ returns a string (limited to 255 characters)
   # This statement does not trigger an error, but the result returned is 255
   MAXLEN=len(space$(500))
```

# Description

`space$(EXP_NB)` returns a space containing `EXP_NB` spaces. This function is equivalent to `string$(EXP_NB,32)` or `string$(EXP_NB," ")`.

The type of result is [Char](4gl_char.html).

# Comments

`space$(0)` returns the null string `""`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |
| 50 | The argument is negative. |

# See also

[string$](4gl_string$.html), [ascii](4gl_ascii.html), [chr$](4gl_chr$.html), [vireblc](4gl_vireblc.html).

  

[Index](index.html)  [Home](getting-started_home.html)