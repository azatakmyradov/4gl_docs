[Index](index.html)  [Home](getting-started_home.html)

Titcol

`Titcol` allows to assign dynamically titles in the columns of a grid present on a screen.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
  Titcol [ABBREVIATION]BOTTOM_PAGE LIST_OF_STRING_EXPRESSIONS
  Titcol [ABBREVIATION]BOTTOM_PAGE STRING_EXPRESSION For COLUMN_NAME
```

ABBREVIATION is the abbreviation of the corresponding mask.
BOTTOM\_PAGE is the name of the "bottom-page" variable in the mask (the variable associated to a grid that stores the number of lines present).
LIST\_OF\_STRING\_EXPRESSIONS is a list of string expressions representing the titles of the consecutive columns in the grid.
COLUMN\_NAME is the name of the variable whose title should be changed

The syntax 1 allows to define titles for the first N columns (only the columns visible or enterable are concerned).  
The syntax 2 allows to define the title for a given column identified by its name.

# Examples

```
# Let's imagine we have a grid containing CATEG1, CATEG2, CATEG3, CATEG4, CATEG5 in [ITM] mask with CATEG as bottom-page variable
# Let's define the title of the 3 first columns of a grid by using the title of the Item category
  Titcol [ITM]CATEG mess(1,206,1), mess(1,206,2), mess(1,206,3)

# Let's redefine CATEG5 with another title
  Titcol [ITM]CATEG "Others" For CATEG5

# The title associated to CATEG4 remains unchanged
```

# Description and comments

`Titcol` is used to change dynamically the title of columns in a grid.

# Comment

When a mask includes a grid where the column titles are evaluated, the use of `Titcol` is automatically done in a generated script called in the "before-field" action of the bottom-page variable.

If the global variable GORITITCOL is set to "1", the corresponding script is not called.

# See also

[Chgfmt](4gl_Chgfmt.html), [Chgtbk](4gl_Chgtbk.html), [Chgtfd](4gl_Chgtfd.html), [Chgtzn](4gl_Chgtzn.html), [Chgstl](4gl_Chgstl.html).

  

[Index](index.html)  [Home](getting-started_home.html)