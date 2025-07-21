[Index](index.html)  [Home](getting-started_home.html)

Toupper

`toupper` converts the lower case letters in a string into upper case letters. Other characters remain unchanged.

# Syntax

```
   toupper(STRING_EXPR)
```

* `STRING_EXPR` is an expression returning a string or a CLOB variable.

# Examples

```
   # Let's convert lowercase to uppercase
   IRRITATED_MESSAGE=toupper("please be quiet!") : # Returns "PLEASE BE QUIET!"

   # Let's compare strings independently from the case
    If toupper(NAME_1) = toupper(NAME_2)
       # The two names are identical
    Endif

   # Let's compare strings independently from the case and the accents
    If toupper(ctrans(NAME_1)) = toupper(ctrans(NAME_2))
       # The two names are identical
    Endif

   # Let's do it with a (French) accentuated message
   IRRITATED_MESSAGE=toupper("s'il vous plaÃ®t, arrÃªtez ce bruit Ã´ combien insensÃ©")
   # returns "S'IL VOUS PLAÃT, ARRÃTEZ CE BRUIT Ã COMBIEN INSENSÃ"
```

# Description

`toupper` converts the lower case characters (including the accentuated letters) in the corresponding upper case characters, without changing other characters.

The function [ctrans](4gl_ctrans.html) can be used to suppress the accents prior to using the [toupper](4gl_toupper.html) function.

The type of result is [Char](4gl_char.html) or [Clbfile](4gl_clbfile.html), depending on the length of the string.

# Comments

The [format$](4gl_format$.html) used with a format that contains only "A", will also perform a `toupper` conversion, with the following differences:  
\* The length of the resulting string will be constant and can include trailing spaces.  
\* If characters that are not letters are present, the formatting will globally replace the string by a string filled with spaces. This will happen for accentuated characters that are refused by the "A" format.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a string or CLOB. |

# See also

[tolower](4gl_tolower.html), [format$](4gl_format$.html), [ctrans](4gl_ctrans.html).

  

[Index](index.html)  [Home](getting-started_home.html)