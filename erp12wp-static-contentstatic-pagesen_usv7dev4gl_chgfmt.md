[Index](index.html)  [Home](getting-started_home.html)

Chgfmt

`Chgfmt` changes the format of a field in a screen mask.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Chgfmt [CLASS] FIELD With FORMAT
```

* `FIELD` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX)`, where `INDEX` is an integer values that provides the indexes of the element in the array.
* `[CLASS]` is the abbreviation that has been used for the mask. If omitted, it is the default mask.
* `FORMAT` is a string expression that provides a valid X3 format.

# Examples

```
# Format change for the AMTVAL1 field in the TXM1 screen
# to right justify an amount displayed in an alpha field
Chgfmt [M:TXM1]AMTVAL1 With "K>:18"
```

# Description

`Chgfmt` is used to change the current format of a field in a mask. The possible formats are described in [format$](4gl_format$.html) function.

# See also

[format$](4gl_format$.html), [Chgstl](4gl_Chgstl.html), [Chgtbk](4gl_Chgtbk.html), [Chgtfd](4gl_Chgtfd.html), [Chgtzn](4gl_Chgtzn.html).

  

[Index](index.html)  [Home](getting-started_home.html)