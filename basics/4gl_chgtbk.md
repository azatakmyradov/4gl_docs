[Index](index.html)  [Home](getting-started_home.html)

Chgtbk

`Chgtbk` changes the title of a block in a screen mask.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Chgtbk [CLASS] RANK With TITLE
```

* `RANK` is an integer values that provides the ank of the block.
* `[CLASS]` is the abbreviation that has been used for the mask. If omitted, it is the default mask.
* `TITLE` is a string expression that provides a title.

# Examples

```
# Change to the section title for rank 15
# with the text for chapter 2355
Chgtbk [M:MFC1]15 With mess([F:MFC]MFCTYP,2355,1)
```

# Description

`Chgtbk` is used to change the current title a block in a mask.

# See also

[Chgfmt](4gl_Chgfmt.html),[Chgstl](4gl_Chgstl.html),[Chgtfd](4gl_Chgtfd.html), [Chgtzn](4gl_Chgtzn.html).

  

[Index](index.html)  [Home](getting-started_home.html)