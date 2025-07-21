[Index](index.html)  [Home](getting-started_home.html)

Ctrans

`ctrans` transforms the characters of a string with an 8-byte code into a 7-byte code depending on a conversion table. By default, it suppresses the accents on accentuated characters. But it is also possible to define the conversion table by additional arguments.

# Syntax

```
CODECODE CODE 
   ctrans (STRING_EXPR)
   ctrans (STRING_EXPR,STRING_IN,STRING_OUT)
```

* `STRING_EXPR`, `STRING_IN`, `STRING_OUT` are expressions returning strings.

# Examples

```
  # A French sentence has usually accents, let's suppress them
  SENTENCE=            "Un Ã©lÃ¨ve travaille Ã  faÃ§on des pÃ¢tes de NoÃ«l Ã  son goÃ»t"
  NOACCENTS=ctrans(SENTENCE)
  # NOACCENTS contains "Un eleve travaille a facon des pates de Noel Ã  son gout"

  # Let's now replace some characters
  FOO=ctrans("bar","abr","ofo") : # FOO contains now "foo"

  # Let's replace all the vowels ans spaces in a string
  RESULT = ctrans("this is an unusual yellow box","..... ","")
  # now RESULT is "th.s-.s-.n-.n.s..l-..ll.w-b.x" 

  # Let's suppress all the vowels in a string
  RESULT = ctrans("this is an unusual yellow box","aeiouy","")
  # now RESULT is "ths s n nsl llw bx" 

  # Let's suppress from a sentence all the characters except upper and lower letters and spaces
  Local Char CH1(255),CH2(255) 
  For I=1 to 255
    If (I>=65 and I<=90) or (I>=97 and I<=122) or I=32
      CH1+=chr$(I)
    Else
      CH2+=chr$(I)
    Endif
  Next I
  FILTERED=ctrans(SENTENCE,CH1+CH2,CH1)
```

# Description

`ctrans` used with one argument transforms the characters in a string coded on 8 bytes by an equivalent on 7 bits.   
It replaces the following:   
\* The accentuated characters by the equivalent character without accent.   
\* The non-printable characters by a space.   
\* The semigraphic characters used for arrays by "!", "+", or "-".

`ctrans`, used with three arguments, transforms a character string by replacing the character at the Nth in the second argument by the character at the same Nth position in the third argument. All the characters not in the second argument string remain the same. If the third string length (L3) is smaller than the second string length (L2), the characters that are located after the position L3 in the second string are suppressed.

The type of result is [Char](4gl_char.html).

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The argument is not a string. |

# See also

[toupper](4gl_toupper.html), [tolower](4gl_tolower.html), [chr$](4gl_chr$.html), [ascii](4gl_ascii.html).

  

[Index](index.html)  [Home](getting-started_home.html)