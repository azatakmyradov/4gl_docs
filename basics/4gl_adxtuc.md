[Index](index.html)  [Home](getting-started_home.html)

Adxtuc

`adxtuc` is an array of 32 character strings (from 0 to 31) with a maximum length of 33. It allows you to define accepted characters in additional data types used for formatting data.

These types were previously used by the client to perform format control during input; however, they are now deprecated. The only time they are still use is for [format$](4gl_format$.html). If a dedicated data type defined by [adxtul](4gl_adxtul.html)(I) is used in a format, the format control checks whether the character corresponds to one of the data types defined in [adxtut](4gl_adxtut.html)(I) or one of the characters defined by `adxtuc`(I). If the format does not fit the string, it returns spaces instead of the formatted characters.

**Note that some values of `adxtuc`, [adxtul](4gl_adxtul.html), and [adxtut](4gl_adxtut.html) can be used by the standard Sage X3 software and therefore, may not be modifiable.**

# Example

```
  adxtul(0)="R"    : # R is a character that is not used in format yet
  adxtut(0)=""     : # No character from a predefined set
  adxtuc(0)="xyz"  : # One of the (x,y,z) characters

  adxtul(1)="S"    : # S is a character that is not used in format yet
  adxtul(1)"R#"    : # One of the character defined by R or a digit
  adxtuc(1)="!?/"  : # and also the (!?;) characters

  adxtul(2)="T"    : # T is a character that is not used in format yet
  adxtul(2)"AS"    : # Upper case character or one of the character defined by R or a digit
  adxtuc(2)="+-"  : # and also the (u,v,w) characters

# Formatting examples
  FORMAT1=format$("K:5R","xxyyzz") : # "xxyyz" (truncation)
  FORMAT2=format$("K:3R3S","xxy5;?") : # "xxy5/?" (x and y fit with R format, 5,!,/ with S format)
  FORMAT3=format$("K:3T","xxy") : # "XXY" (x and y fit with A format first and are transformed in upper case
  FORMAT4=format$("K:3R3T","+xa") : # "      " (+ does not fit with R format that allows only x,y,z)
```

# See also

[adxtut](4gl_adxtut.html), [adxtul](4gl_adxtul.html), [format$](4gl_format$.html).

  

[Index](index.html)  [Home](getting-started_home.html)