[Index](index.html)  [Home](getting-started_home.html)

Affzo

`Affzo` displays all or part of the fields in a mask.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Affzo [CLASS]
   Affzo [CLASS] FIELD_LIST
   Affzo FIELD_LIST
```

* `FIELD_LIST` is a list of FIELDS separated by commas.
* `FIELD` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX)`, where `INDEX` is an integer values that provides the indexes of the element in the array, or a rank (numeric value), or a range of fields with the syntax `VARIABLE_NAME` - `VARIABLE_NAME`, or a range of ranks with the syntax `RANK_1` - `RANK_2`, or a numeric or alphanumeric expression prefixed by `=`wich computation returns a rank or a field name.
* If no field is given, all the fields in the mask are activated.
* `[CLASS]` is the abbreviation that has been used for the mask. If omitted, it is the default mask.

# Examples

```
# Display in the current mask the fields of rank 1, 15 to 30
# and of fields CHP1, VAR to FIN.
Affzo 1, 15-30, CHP1, VAR-FIN

# Display in the abbreviation mask ABC the fields of rank 20 to 30
# and the field TOTO for index I+1.
Affzo [ABC]20-30, TOTO(I+1)

# Display  all the fields of mask with the abbreviation ABC.
Affzo [ABC]

# Display all the field in rank I+10
Affzo [ABC] =I+10
```

# Description

`Affzo` is used to display all or part of the fields.

`Affzo` is used for fields declared as being displayable in the mask.

The diaplay order is the logical rank and position order on the screen. As a consequence if this order needs to be modified, it is necessary to use several `Affzo` statements.

Similarly, when giving an interval of the fields to be displayed, it is the entry order that is considered to determine which are the fields in the interval.

A grid can be fully or only partially displayed. The syntaxes are the same:

`Affzo [M]NBLIG` Where NBLIG is the grid bottom variable  
or `Affzo [M]xx` Where xx is the rank

`Affzo [M]FIELD` Where FIELD is a column name, activates the column  
 `Affzo [M]FIELD(nolign-1)` Where FIELD is a column name and `nolign`the line number, activates a cell.

# Notes

If the `zonsui` system variable contains the name of a mask field, the display starts from this field. `[S]zonsui` will be reset as "empty string" after the display.

The instruction `Affzo` class will set the screen as being valid; the field checks will not be performed. The instruction `Affzo` on rank(s) or field(s) does not alter the validity status of the mask.

# See also

[Actzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html).

  

[Index](index.html)  [Home](getting-started_home.html)