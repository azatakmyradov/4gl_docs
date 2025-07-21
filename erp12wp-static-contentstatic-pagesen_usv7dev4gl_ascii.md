[Index](index.html)  [Home](getting-started_home.html)

Ascii

`ascii` returns the code of the first character of a string.

# Syntax

```
   ascii(STRING_EXPR)
```

* `STRING_EXPR` is an expression that returns a character string result.

# Examples

```
  Local Integer I
  Local Char MYSTRING(20)
  I = ascii(MYSTRING) : # the value of I is 0
  MYSTRING="ABCDEFG"
  I = ascii(MYSTRING) : # the value of I is now 65
```

# Description

`ascii` returns an integer value that is the code of the first character of a string. For a character that belongs to the latin character set, the value returned is in the range [32,127]; for special characters, it is in the range [1,31]; latin accentuated characters are usually in the range [128,255]. Additional characters such as chinese characters are in the range [256,65565].

The character set used internally by the engine in memory is UCS2, and the `ascii` value corresponds to this encoding. When reading or writing data on a file, UTF8 encoding can be used; however, this is never the case for character strings used by the Sage X3 engine. The translation from UCS2 to UTF8 and the reverse is done by setting the variable [adxium](4gl_adxium.html) to the right value.

The reverse function of `ascii` is [chr$](4gl_chr$.html), which allows you to create a one-character string by giving its UCS2 code as an argument.

When the string is empty, `ascii` returns 0.

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The argument is not a string. |

# See also

[chr$](4gl_chr$.html), [string$](4gl_string$.html), [adxium](4gl_adxium.html), [Iomode](4gl_iomode.html).

  

[Index](index.html)  [Home](getting-started_home.html)