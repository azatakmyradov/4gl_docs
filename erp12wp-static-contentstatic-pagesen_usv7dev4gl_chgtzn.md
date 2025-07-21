[Index](index.html)  [Home](getting-started_home.html)

Chgtzn

`Chgtzn` changes the title of a field associated in a mask.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Chgtzn [CLASS] With TITLE
   Chgtzn [CLASS] FIELD_LIST With TITLE
   Chgtzn FIELD_LIST With TITLE
```

* `FIELD_LIST` is a list of FIELDS separated by commas.
* `FIELD` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX)`, where `INDEX` is an integer values that provides the indexes of the element in the array, or a rank (numeric value), or a range of fields with the syntax `VARIABLE_NAME` - `VARIABLE_NAME`, or a range of ranks with the syntax `RANK_1` - `RANK_2`, or a numeric or alphanumeric expression prefixed by `=`wich computation returns a rank or a field name.
* If no field is given, all the fields in the mask are concerned.
* `[CLASS]` is the abbreviation that has been used for the mask. If omitted, it is the default mask.
* `TITLE` is a string expression that provides a title.

# Examples

```
# Change to the title of the AMTVAL1 field in the TXM1 screen
Chgtzn [M:TXM1]AMTVAL1 With "new text"
```

# Description

`Chgtzn` is used to change the current title of a field or a list of fields in a mask.

# See also

[Chgfmt](4gl_Chgfmt.html),[Chgstl](4gl_Chgstl.html),[Chgtbk](4gl_Chgtbk.html), [Chgtfd](4gl_Chgtfd.html).

  

[Index](index.html)  [Home](getting-started_home.html)