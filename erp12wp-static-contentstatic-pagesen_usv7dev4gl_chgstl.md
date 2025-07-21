[Index](index.html)  [Home](getting-started_home.html)

Chgfmt

`Chgfmt` changes the format of a field in a screen mask.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Chgstl [CLASS] FIELD_LIST With STYLE
```

* `FIELD_LIST` is a list of FIELDS separated by commas.
* `FIELD` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX)`, where `INDEX` is an integer values that provides the indexes of the element in the array, or a rank (numeric value), or a range of fields with the syntax `VARIABLE_NAME` - `VARIABLE_NAME`, or a range of ranks with the syntax `RANK_1` - `RANK_2`, or a numeric or alphanumeric expression prefixed by `=`wich computation returns a rank or a field name.
* If no field is given, all the fields in the mask are set.
* `[CLASS]` is the abbreviation that has been used for the mask. If omitted, it is the default mask.
* `STYLE` is a string expression that provides a valid style name.

# Examples

```
# Format change for the AMTVAL1 field in the TXM1 screen
# to right justify an amount displayed in an alpha field
Chgfmt[M:TXM1]AMTVAL1 With "K>:18"
```

# Description

`Chgstl` is used to change the style for all or part of the contents of the fields in a mask. The style is defined by a name with which graphical characteristics are associated : text color, background color, character fonts, font size, attributes (underlined, italic, bold, crossed out).

If the style is not defined, there is no error but there is no application of a style.

If the style is not specified ( With "" ), the default style is allocated. In Sage X3, this default style is defined in the "Tools/Options/Fonts and styles" menu.

In a grid, it is not necessary to carry out an `Affzo` (field display), in order to modify the style of a column, a line or a cell.

The order of the processing of the fields used is always that resulting from the entry ranks and the position of the fields in the screen. As a consequence, in order to change this order of processing, it is necessary to use several `Chgstl` instructions.

Similarly, when giving an interval of the fields to be processed, it is the order entry that is considered to determine which are the fields in the interval.

# Comments

Some limits exist in the styles applied to the deactivated fields (that is the value is not in the sense of the given context) with the `Grizo` instruction, and for displayed fields only (this characteristic is obtained by the instruction `Diszo`).

The styles can be static (defined in the dictionary) or dynamic (i.e. sent contextually by the software as a function of the context : this is notably the case for conditional styles. When a dynamic style is defined and sent to the interface, this style replaces the existing static style; it is never combined with a static style. To illustrate this, let's take the example of an underlined field to which a style "color red" is applied. It would become becomes red and underlined if there were a combination; but this is not what happens: the field becomes red but not underlined.

# See also

[Chgfmt](4gl_Chgfmt.html), [Chgtbk](4gl_Chgtbk.html), [Chgtfd](4gl_Chgtfd.html), [Chgtzn](4gl_Chgtzn.html).

  

[Index](index.html)  [Home](getting-started_home.html)