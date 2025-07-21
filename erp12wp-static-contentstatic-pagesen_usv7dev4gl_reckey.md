[Index](index.html)  [Home](getting-started_home.html)

Reckey

`reckey` is a pseudo key present in database table using this key ensures that the sequential reading order will be optimal (it uses the physical order of the database and thus avoids any data sort when the query is sent to the database). It can be used in [For](4gl_for.html) loops.

# Syntax

```
  For [abv]reckey
  For [abv]reckey Where conditions
```

By default, when a [For](../4gl/for.md) instruction is used on the database without giving a key, there is always an `Order By` clause sent to the database:

* The `Order By` can be placed directly on the [File](4gl_file.html) instruction.
* If the table is declared without any `Order By`, the first index is used.

It can be important to avoid an `Order By` clause that can be costly if the order in which the data is read has no importance.

In fact, `reckey` corresponds to the row id (ie. the physical location of the record in the storage area). Using this order allow the fastests way to access to data, but it is especially relevant when the whole table is accessed, and supposes that the order of access is absolutely not a constraint.

# Examples

```
   # Let's imagine we have to check all the order lines stored in the table
   # Let's imagine that there is no and no sorting order that would make the control faster or easier
     Local File SORDERD [SOD]
     For [SOD]reckey
       Gosub CONTROL
     Next
```

```
# Let's compute the sum of some lines in the database
# This type of computation can be faster when expressed in SQL with the use of aggregation operators on groups
Local File SALESORDER [ORD] Where CURRENCY="USD" and ORDER_DATE>=date$-100
Local Integer TOTAL_NUMBER
Local Decimal TOTAL_AMOUNT

  # We don't care about the order in which the lines are extracted
  For [ORD]reckey where SALESREP="JOHNDOE"
    TOTAL_AMOUNT+=[ORD]AMOUNT
    TOTAL_NUMBER+=1
  Next

  # If the only information we need is the count of lines, it will be preferable to use
  Filter [ORD] Where SALESREP="JOHNDOE"
  TOTAL_NUMBER=rowcount([ORD])

# Let's check if at least an order exist for a given customer
# ORDER_FOUND=1 if at least an order exist (we don't care about which one, no order is required)
  ORDER_FOUND=0
  For [ORD]reckey WHERE CUSTOMER="CUST001"
    ORDER_FOUND=1
    Break
  Next
```

# Comment

Although the cases where this order can be used is probably no very frequent, the performance gap justifies it in specific cases. A measure done on 2.5 millions of lines gave an average win on the execution timeequal to 15%.

# Associated errors

none

# See also

[For](4gl_for.html), [Filter](4gl_filter.html), [File](4gl_file.html), [Hint](4gl_hint.html), [Nohint](4gl_nohint.html).

  

[Index](index.html)  [Home](getting-started_home.html)