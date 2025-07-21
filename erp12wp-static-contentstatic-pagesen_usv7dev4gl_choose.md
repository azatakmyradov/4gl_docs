[Index](index.html)  [Home](getting-started_home.html)

Choose

`Choose` displays a popup windows with a set of lines extracted from a table in order to select a record.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
  Choose CLASS WHERE_CLAUSE ORDERBY_CLAUSE Using COLUMN_LIST TITLE_CLAUSE STARTING_CLAUSE
```

In this syntax:
\* `WHERE\_CLAUSE`, `ORDERBY\_CLAUSE`, `TITLE\_CLAUSE`, `STARTING\_CLAUSE` are optional.
\* `CLASS` is the abbreviation of a table, view, or join (by [Link](../4gl/link.md)) between square brackets. The table must have been opened.
\* `COLUMN\_LIST` is a list of columns present in the table. Every column can have a title with the syntax `Titled EXPRESSION`, where `EXPRESSION` is a string expression.
\* `ORDERBY\_CLAUSE` is a clause that is defined in a dedicated [documentation](../4gl/order-by.md).
\* `WHERE\_CLAUSE` is a clause that defines filtering condition. The syntax is defined in a dedicated [documentation](../4gl/where.md).
\* `TITLE\_CLAUSE` is a clause that uses the keyword `Titled` followed by a string expression.
\* `STARTING\_CLAUSE` is a clause that uses the keywords `Starting at` followed by a condition that uses the same condition syntax than for the [Where conditions](../4gl/where.md). It defines the record on which the cursor is placed by default.

# Example

```
# Let's open a table
  Local File BPCUSTOMER [SELB]

# Let's open the selection popup
  Choose [SELB]
& Where BPCNAM>"D"
& Order By BPCNAM; PTE; BPCNUM Using
& [SELB]BPCNUM Titled "Customer ID",
& [SELB]BPCNAM Titled "Customer name",
& Titled "Select a customer"
& Starting At [SELB]BPCNAM >= "DE" and [ZMS]PTE <>"CHQ"
```

# Description and comments

Choose is used to open a popup window on a list of recordings extracted from a table, and to select a record. This instruction is normally used in the selection process of a field defined in a mask, in order to perform an entry in a list, but it can also be used in any script, and disconnected from any entry statement.

The table in which the selection operates must have been opened by the File or Local File instruction. In particular, it can result from the execution of a system order, as it is allowed by the `File` instruction.

The `Where` clause, that is optional, defines the filtering criteria fulfilled by the records that appear in the selection window. If it is absent, only the first 255 lines in the table can be chosen. The selection criteria defined in `Choose` are added to those of the `File` instruction when the latter contains some, or to the last Filter.

The `Order By` clause defines the order in which the information will appear in the mask. Specifying a number of key parts makes it possible to limit the read of the recordings to the first encountered one (in the case of possible homonyms) for each new value taken by the key (on the given number of components). A default order based on the where clause is used if no `Order By` clause has been set.

The `Using` clause defines the table columns that will be viewed in the selection window.

`Choose` loads a maximum of 255 records. Then the cursor positions itself inside the selection window on:

* the first record if no `Starting at` clause is present.
* the first record that fulfills the `Starting at` condition if this condition is present
* the last record of the records sent back if no record fulfills the `Starting at` condition.

The `Titled` clause is used to give a title to the selection box.

# Comments

Choose updates the [fstat](4gl_fstat.html) variable which is equal to 0 when there are elements to be selected, or to 4, which means that the selection is empty.

The selected record becomes the current record and the variables of class [F] (like those of class [G]) contain the values that correspond to this record.

The status system variable returns the output status of the selection. It is equal to 28 if a record has been selected.

The selection boxes are closed once the choice is made.

# Associated errors

| Error | Description |
| --- | --- |
| ERCLAS (7) | The table is not opened. |

# See also

[File](4gl_file.html), [Link](4gl_link.html), [Order By](4gl_order-by.html), [Where](4gl_where.html).

  

[Index](index.html)  [Home](getting-started_home.html)