[Index](index.html)  [Home](getting-started_home.html)

String$

`string$` returns a string containing a string repeated a given number of times.

# Syntax

```
   string$(EXP_NB,EXP_STRING)
   string$(EXP_NB,EXP_CAR)
```

* `EXP_NB` is an integer expression that returns the number of time the string must be repeated.
* `EXP_STRING` is a string expression that is the string to be repeated.
* `EXP_CAR` is an integer expression that corresponds to the code of the character to be repeated.

# Examples

```
   # Returns the string "abc abc abc"
   MY_STRING=string$(3,"abc ")

   # Returns the string "AAAAA"
   MY_STRING=string$(5,65)

   # string$ returns a string (limited to 255 characters)
   # This statement does not trigger an error, but the result returned is 255
   MAXLEN=len(string$(500,45))
```

# Description

`string$(EXP_NB,EXP_STRING)` returns a string containing `EXP_NB` times the string `EXP_STRING`.  
`string$(EXP_NB,EXP_CAR)` returns a string containing `EXP_NB` times the character of code `EXP_CAR`.  
 This function is equivalent to `string$(EXP_NB,chr$(EXP_CAR))`.

The type of result is [Char](4gl_char.html).

# Comments

When `EXP_NB` is 0, `EXP_CAR` is 0, or `EXP_STRING` is `""`, the result is always the null string `""`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The first argument is not numeric, or the second argument has another type than numeric or string. |
| 50 | The first argument is negative. |

# See also

[space$](4gl_space$.html), [ascii](4gl_ascii.html), [chr$](4gl_chr$.html), [vireblc](4gl_vireblc.html).

  

[Index](index.html)  [Home](getting-started_home.html)