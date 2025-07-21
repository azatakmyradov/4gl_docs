[Index](index.html)  [Home](getting-started_home.html)

Nbrecord

`nbrecord` returns the number of lines in a database table.

# Syntax

```
   nbrecord(CLASS)
```

* `CLASS` is a class associated with an opened table.

# Examples

```
   # How many customers and items?
     Local Integer CUST_COUNT, ITEM_COUNT
     Local File BPCUSTOMER [BPC], ITMMASTER [ITM]
     CUST_COUNT=nbrecord([BPC])
     ITEM_COUNT=nbrecord([ITM])
```

# Description

`nbrecord` returns the number of lines on a table opened by [File](4gl_file.html) or [Trbegin](4gl_trbegin.html).

It performs a `Select count(*) From TABLE`.

The type of result is [Integer](4gl_integer.html) or [Decimal](4gl_decimal.html).

# Comment

No [Where](4gl_where.html) clause is used on the count, even if [Where](4gl_where.html) conditions have been given on the table declaration or in a [Filter](4gl_filter.html) statement. If the count must be done on a selection, [rowcount](4gl_rowcount.html) must be used.

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | The table is not opened. |

# See also

[File](4gl_file.html), [Trbegin](4gl_trbegin.html), [rowcount](4gl_rowcount.html).

  

[Index](index.html)  [Home](getting-started_home.html)