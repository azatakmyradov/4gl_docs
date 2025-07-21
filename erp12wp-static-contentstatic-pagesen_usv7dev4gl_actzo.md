[Index](index.html)  [Home](getting-started_home.html)

Actzo

`Actzo` activates all or part of the fields in a mask that were previously grayed.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Actzo [CLASS]
   Actzo [CLASS] FIELD_LIST
   Actzo FIELD_LIST
```

* `FIELD_LIST` is a list of FIELDS separated by commas.
* `FIELD` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX)`, where `INDEX` is an integer values that provides the indexes of the element in the array, or a rank (numeric value), or a range of fields with the syntax `VARIABLE_NAME` - `VARIABLE_NAME`, or a range of ranks with the syntax `RANK_1` - `RANK_2`, or a numeric or alphanumeric expression prefixed by `=`wich computation returns a rank or a field name.
* If no field is given, all the fields in the mask are activated.
* `[CLASS]` is the abbreviation that has been used for the mask. If omitted, it is the default mask.

# Examples

```
# Activate in the current mask the fields of rank 1, 15 to 30
# and of fields CHP1, VAR to FIN.
Actzo 1, 15-30, CHP1, VAR-FIN

# Activate in the abbreviation mask ABC the fields of rank 20 to 30
# and the field TOTO for index I+1.
Actzo [ABC]20-30, TOTO(I+1)

# Activate  all the fields of mask with the abbreviation ABC.
Actzo [ABC]
```

# Description

`Actzo` is used to display all or part of the fields in a mask further to a [Grizo](4gl_Grizo.html) or [Diszo](4gl_Diszo.html).

`Actzo` is used for fields declared as being enterable in the mask. These fields can be filled again and recover their contextual menu.

When fields are made availble again via `Actzo`, the order to remove the grayed elements always derives from the entry ranks and the position of the fields on the screen. As a consequence if this order to remove the grayed fields needs to be modified, it is necessary to use several `Actzo` statements.

Similarly, when giving an interval of the fields to be activated, it is the entry order that is considered to determine which are the fields in the interval.

A grid can be fully or only partially activated. The syntaxes are the same:

`Actzo [M]NBLIG` Where NBLIG is the grid bottom variable  
or `Actzo [M]xx` Where xx is the rank

`Actzo [M]FIELD` Where FIELD is a column name, activates the column  
 `Actzo [M]FIELD(nolign-1)` Where FIELD is a column name and `nolign`the line number, activates a cell.

# Notes

`Actzo` positions the screen as valid. The field checks will not be carried out. `Actzo` on rank(s) or field(s) does not modify the validity status of the mask.

# See also

[Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html).

  

[Index](index.html)  [Home](getting-started_home.html)