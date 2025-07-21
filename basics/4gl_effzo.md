[Index](index.html)  [Home](getting-started_home.html)

Effzo

`Effzo` grays out all or part of the fields in a mask that were previously activated.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Effzo [CLASS]
   Effzo [CLASS] FIELD_LIST
   Effzo FIELD_LIST
```

* `FIELD_LIST` is a list of FIELDS separated by commas.
* `FIELD` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX)`, where `INDEX` is an integer values that provides the indexes of the element in the array, or a rank (numeric value), or a range of fields with the syntax `VARIABLE_NAME` - `VARIABLE_NAME`, or a range of ranks with the syntax `RANK_1` - `RANK_2`, or a numeric or alphanumeric expression prefixed by `=`wich computation returns a rank or a field name.
* If no field is given, all the fields in the mask are grayed out.
* `[CLASS]` is the abbreviation that has been used for the mask. If omitted, it is the default mask.

# Examples

```
# Deletion in the current mask of the fields of the rank 1, 15 Ã  30,
# and of the fields CHP1, VAR to END.
Effzo 1, 15-30, CHP1, VAR-END

# Deletion in the current mask of all the fields
Effzo

# Deletion in the mask ABC, of the fields of the rank 20, 15 Ã  30,
# and of the TOTO field for the I+1 index
Effzo [ABC]20-30, TOTO(I+1)

# Deletion of all the fields of the mask FACT
Effzo [FACT]

# Deletion of fields FIRST and LAST. The deletion order is
# the ranks order and not the Effzo declaration order
Effzo LAST, FIRST
```

# Description

`Effzo` is used to delete all or part of the fields of a screen mask. Blanks are then displayed in the screen where these fields would be displayed whatever the format. The variables corresponding to the mask are then 'reset to zero' (that is to say the empty chain "" for the Char type variables, the null date for the date variables and the zero value for the numeric variables).

When fields are deleted via `Effzo`, the deletion order used always derives from the entry ranks and the position of the fields on the screen. As a consequence, in order to change this deletion order, it is necessary to use several `Effzo` instructions.

Warning! `Effzo` does not work with a non displayed mask, a mask used to group work variables for example. The `Raz` instruction will then be used.

# Notes

`Effzo` instruction is not equivalent to a `Raz` followed by a display by `Affzo`. Indeed, `Effzo` operates a `Raz` but is, on top of that, followed by a display of blanks.

The phase of blanks display reset to zero the entire formatting string, including potential comments.

`Effzo` will position the screen as being valid. The field checks will be carried out.

# See also

[Actzo](4gl_Actzo.html), [Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html).

  

[Index](index.html)  [Home](getting-started_home.html)