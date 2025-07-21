[Index](index.html)  [Home](getting-started_home.html)

Grizo

`Grizo` grays out all or part of the fields in a mask that were previously activated.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Grizo [CLASS]
   Grizo [CLASS] FIELD_LIST
   Grizo FIELD_LIST
```

* `FIELD_LIST` is a list of FIELDS separated by commas.
* `FIELD` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX)`, where `INDEX` is an integer values that provides the indexes of the element in the array, or a rank (numeric value), or a range of fields with the syntax `VARIABLE_NAME` - `VARIABLE_NAME`, or a range of ranks with the syntax `RANK_1` - `RANK_2`, or a numeric or alphanumeric expression prefixed by `=`wich computation returns a rank or a field name.
* If no field is given, all the fields in the mask are grayed out.
* `[CLASS]` is the abbreviation that has been used for the mask. If omitted, it is the default mask.

# Examples

```
# Gray out in the current mask the fields of rank 1, 15 to 30
# and of fields CHP1, VAR to FIN.
Grizo 1, 15-30, CHP1, VAR-FIN

# Gray out in the abbreviation mask ABC the fields of rank 20 to 30
# and the field TOTO for index I+1.
Grizo [ABC]20-30, TOTO(I+1)

# Gray out  all the fields of mask with the abbreviation ABC.
Grizo [ABC]
```

# Description

`Grizo` is used to gray out all or part of the fields in a mask, for example further to a [Actzo](4gl_Actzo.html).

`Grizo` is used for fields declared as being enterable in the mask. These fields can no more be entered.

When fields are made unavailable again via `Grizo`, the order to gray the elements always derives from the entry ranks and the position of the fields on the screen. As a consequence if this order to gray out fields needs to be modified, it is necessary to use several `Grizo` statements.

Similarly, when giving an interval of the fields to be grayed out, it is the entry order that is considered to determine which are the fields in the interval.

A grid can be fully or only partially grayed out. The syntaxes are the same:

`Grizo [M]NBLIG` Where NBLIG is the grid bottom variable

or `Grizo [M]xx` Where xx is the rank

`Grizo [M]FIELD` Where FIELD is a column name, grays outs the column

`Grizo [M]FIELD(nolign-1)` Where FIELD is a column name and `nolign`the line number, grays out a cell.

In a grid, a grayed-out field appears in a grey font. If the field has a color attribute via pcolor, its color is kept. On fields other than the grid bottom variable, the Grizo doe not enables the on focus nor the contextual menu.

# Notes

`Grizo` positions the screen as valid. The field checks will not be carried out. `Grizo` on rank(s) or field(s) does not modify the validity status of the mask.

# See also

[Actzo](4gl_Actzo.html), [Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html).

  

[Index](index.html)  [Home](getting-started_home.html)