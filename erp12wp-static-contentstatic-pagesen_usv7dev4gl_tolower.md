[Index](index.html)  [Home](getting-started_home.html)

Tolower

`tolower` transforms the upper case letters in a string into lower case letters. The other characters remain unchanged.

# Syntax

```
   tolower(STRING_EXPR)
```

* `STRING_EXPR` is an expression returning a string or a CLOB variable.

# Examples

```
   # Let's transform lowercase to uppercase
   SOFT_MESSAGE=tolower("PLEASE BE QUIET!") : # Returns "please be quiet!"

   # Let's compare strings independently from the case
    If tolower(NAME_1) = tolower(NAME_2)
       # The two names are identical
    Endif

   # Let's compare strings independently from the case and the accents
    If tolower(ctrans(NAME_1)) = tolower(ctrans(NAME_2))
       # The two names are identical
    Endif

   # Let's do it with a (French) accentuated message
   SOFT_MESSAGE=tolower("S'IL VOUS PLAÃT, ARRÃTEZ CE BRUIT Ã COMBIEN INSENSÃ")
   # returns "s'il vous plaÃ®t, arrÃªtez ce bruit Ã´ combien insensÃ©"
```

# Description

`tolower` transforms the upper case characters, including the accentuated letters, in the corresponding lower case characters without changing the other characters.

The function [ctrans](4gl_ctrans.html) can be used if you want to suppress the accents prior to using the [tolower](4gl_tolower.html) function.

The type of result is a [Char](4gl_char.html) or [Clbfile](4gl_clbfile.html) depending on the length of the string.

# Comments

The [format$](4gl_format$.html) used with a format that contains only "a", will also perform a `tolower` transformation, with the following differences:  
\* The length of the resulting string will be constant and can include trailing spaces.  
\* If characters that are not letters are present, the formatting will globally replace the string by a string filled with spaces. This will also be the case for accentuated character that are refused by "a" format.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a string or a CLOB. |

# See also

[toupper](4gl_toupper.html), [format$](4gl_format$.html), [ctrans](4gl_ctrans.html).

  

[Index](index.html)  [Home](getting-started_home.html)