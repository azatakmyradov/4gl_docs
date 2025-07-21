[Index](index.html)  [Home](getting-started_home.html)

Order by

`Order By` is a clause that can be used in conjunction with several language keywords:

If we except [Sorta](4gl_sorta.html) that is described separately, `Order By` is related to the sorting order and used as an additional clause for SQL database requests:

* [File](4gl_file.html)
* [Filter](4gl_filter.html)
* [Link](4gl_link.html)

# Syntax

```
   SYNTAX 1
   ... Order By Key KEY_ID(INDEX_EXPR) ORDER
   ... Order By Key KEY_ID(INDEX_EXPR)
   ... Order By Key KEY_ID ORDER
   ... Order By Key KEY_ID

   SYNTAX 2
   ... Order By Key KEY_ID = EXPR_LIST

   SYNTAX 3
   ... Order By KEY_EXPR_LIST

   SYNTAX 4
   ... Order With Key KEY_ID = KEY_STRING

   SYNTAX 5
   ... Order With KEY_STRING
```

Where:
\* `KEY\_ID` is the name that defines the key. When using the syntax 1, `KEY\_ID` refers to an existing key in the table. Otherwise, it is the name that is given to a temporary key.
\* `INDEX\_EXPR` is an integer expression that gives the number of key segments used (especially when a partial key is used). When omitted, the whole key is used. It can have at most a value of 16.
\* `KEY\_EXPR\_LIST` is a list of `KEY\_EXPR` separated by semicolons.
\* `KEY\_EXPR` is a column of the table that can be followed by one of the two keywords [Asc](../4gl/asc.md) and [Desc](../4gl/desc.md) (ascending or descending mode; by default, [Asc](../4gl/asc.md) is used).
\* `EXPR\_LIST` is a list of `EXPR` separated by semicolons.
\* `EXPR` is an expression that can include columns of the table, functions, and constants; and can be followed by one of the two keywords [Asc](../4gl/asc.md) and [Desc](../4gl/desc.md) (ascending or descending mode; by default, [Asc](../4gl/asc.md) is used).

# Examples

```
   # Declare a table with an initial filter and a default sorting key
    Local File CUSTOMER Where CATEGORY="MIS" Order By Key COUNTRY

   # Join between the stock file (abbreviated STK) and the 
   # product file (abbreviated PRO) sorted by location and item code
    Link [STK] With [F:PRO]ITMCODE = [F:STK]ITEM As [LSTK]
    & Order By Key SORT_KEY = LOCATION;ITEM

   # Select lines in a table in a given order and process them, then cancel the filter
    Filter [TFI] Where CATEGORY=3 & RANK> 0
    & Order By RANK Asc; NAME Asc
    For [TFI] : Call PROCESS([F:TFI]NAME): Next
    Filter [TFI]

   # The two previous examples with another syntax
    Link [STK] With [F:PRO]ITMCODE = [F:STK]ITEM As [LSTK]
    & Order With Key CLE = "LOCATION;ITEM"

   # Same thing as the two previous examples, but written with a character string
    Filter [TFI] Where CATEGORY=3 & RANK> 0
    & Order With "RANK Asc;NAME Asc"

   # Sort the item description without taking the case in account
    Local File ITEMS [ITM] Order By KEY MYDESC=toupper([ITM]DESCRIPTION)
```

# Description and comments

`Order By` is used with the [File](4gl_file.html), [Link](4gl_link.html), and [Filter](4gl_filter.html) instructions to set the select order of a table (or a group of tables, in the case of a Link order) or to create a new key. It is prohibited on the System type files.

This key becomes the only one to be known for this table and then it masks all the others until the next `Order By` clause.

`Order With` is used instead of `Order By` when the list of elements defining the sort is contained in the character string.

## Declaration of a temporary key

* A new temporary key is created with syntax 2, 3, 4, and 5. By using the 3rd or 5th syntax, no name is given to the key which is accepted by most of the read/write orders.
* Such a key is always a key with Homonyms.
* Such a key is limited to 16 components and their size is 128 bytes.
* In syntax 2 only, evaluated formulas are accepted for the key elements when they can be transmitted to the database (see [the list of supported operators](4gl_where.html#supported_operators)).
* The number of keys is limited to 32 by the table. The new keys created by `Order by` are added to those defined by the table definition. For example, two temporary additional keys are added by performing the following sequence of instructions:
  `File MYTABLE ... Order by ...
  Filter [MYT] ... Order by ...`
* By default, the data is sorted in ascending order of each key component, unless the [Desc](4gl_desc.html) (Descending) clause is used. Applying [Desc](4gl_desc.html) to a pre-existing key (syntax 1) reverts the order for every key component. The key components defined as ascending become descending and vice versa.
* The declaration of an additional key costs time and money, irrespective of the database type. The number of involved recordings is large. It is recommended to:

# Comments

By specifying the key index to 'N' (syntax 1), a loop only selects a record per different value of key and ignores the records that have the same first 'N' keys value.

If a new key is created (syntax 2) it is not possible to redefine it. For example:

```
 File MYFILE [FIC1] Order By Key NEW = NAME;AGE
...
 Filter [FIC1] Order By Key NEW Desc
```

  
At execution time, this generates an error "NEW: Key does not exist in this table".

## Tables with a big number of columns

If your table has more than 255 columns, take care that the columns with a rank over 255 cannot be used in an `Order By` clause. To count the number of columns, you have to consider the dimensions. For instance, a field MYLIST with a dimension of 3 is considered as 3 columns in the table (MYLIST\_0, MYLIST\_1, MYLIST\_2).

# Associated errors

| Error | Description |
| --- | --- |
| 21 | Key does not exist (Order By : 1st syntax). |
| 55 | Key length redefined by "Order By ..." exceeds the size allowed. |

  

[Index](index.html)  [Home](getting-started_home.html)