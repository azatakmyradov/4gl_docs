[Index](index.html)  [Home](getting-started_home.html)

Rowcount

`rowcount` allows you to return the number of lines corresponding to a selection condition in a database table.

# Syntax

```
   rowcount(CLASS)
```

* `CLASS` is a class associated with an opened table.

# Examples

```
   # How many customers and items are active ?
     Local Integer CUST_COUNT, ITEM_COUNT
     Local File BPCUSTOMER [BPC] Where BPCSTA=2, ITMMASTER [ITM] Where ITMSTA=1
     CUST_COUNT=rowcount([BPC])
     ITEM_COUNT=rowcount([ITM])
```

# Description

`nbrecord` returns the number of lines that corresponds to the filter defined by a [Where](4gl_where.html) clause on a table opened by [File](4gl_file.html) or [Trbegin](4gl_trbegin.html).

It performs a `Select count(*) Where... From TABLE`.

The type of result is [Integer](4gl_integer.html) or [Decimal](4gl_decimal.html).

# Comment

If no [Where](4gl_where.html) clause has to be used on the count, [nbrecord](4gl_nbrecord.html) must be used.

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | The table is not opened. |

# See also

[File](4gl_file.html), [Trbegin](4gl_trbegin.html), [nbrecord](4gl_nbrecord.html).

  

[Index](index.html)  [Home](getting-started_home.html)