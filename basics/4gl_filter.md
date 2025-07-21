[Index](index.html)  [Home](getting-started_home.html)

Filter

Use `Filter` to select the lines from a table previously opened and to specify an order to get the results.

# Syntax

```
  Filter [CLASS]
  Filter [CLASS] Where EXPRESSION
  Filter [CLASS] Order By ORDERBY_EXP
  Filter [CLASS] Where EXPRESSION Order By ORDERBY_EXP
```

* `CLASS` is the abbreviation of the table in which the filter is set.
* `EXPRESSION` is a filtering expression. For more information, see the [Where](4gl_where.html) documentation.
* `ORDERBY_EXP` is an ordering expression syntax. For more information, see the [Order By](4gl_order-by.html) documentation.

# Examples

```
   # Let's read the sales order lines in the order of its index ORDLIN (ordernumber,orderline)
   # Only for the orders having a type equal to 1 between 2 dates
   Local File SALESORDER [SORDER] Where ORDTYP=1
   Filter [SORDER] Where ORDDATE>= START_DATE and ORDDATE<=END_DATE
   For [SORDER]ORDLIN(1)
       For [SORDER]ORDLIN(2)
       ...
       Next
   Next
   # Now let's start again for all the orders having a type equal to 1
   Filter [SORDER]
   For [SORDER]ORDLIN(1)
       For [SORDER]ORDLIN(2)
       ...
       Next
   Next

   # Let's delete all the order for a given customer
    Filter [SORDER] Where CUSTOMER=[L]CUSTOMER_TO_DELETE
    Delete [SORDER]ORDNUM >= "" : # All the orders that fulfills the previous filter are concerned
    Filter [SORDER] : # Cancels the selection
```

# Description and comments

`Filter`, in association with the [Where](4gl_where.html) clause, is used to select records from a table previously opened. This speeds up access to the data in this table.

The access key can also be changed, using the [Order By](4gl_order-by.html) clause. This new key can be either an existing key or a new one defined in the [Order By](4gl_order-by.html) clause.

If the table was opened with a [Where](4gl_where.html) clause, `Filter` combines the two selection expressions with an [and](4gl_and.html).

If a `Filter` instruction follows another `Filter`, it cancels and replaces the first instruction. To cancel a filtering expression set by a `Filter` instruction, use the syntax `Filter [abv]` without the [Where](4gl_where.html) clause.

# Comments

If a table opened in a script is used without a new declaration in a subroutine called by [Call](4gl_call.html), a filter that is set on the table during the execution of the [Call](4gl_call.html) remains active after the end of the call. If it is redeclared (with the syntax `File TABLENAME` and not with `File [ABBREVIATION]`), the Filter condition is [local](4gl_local.html) and is not returned.

The following example illustrates this:

```
 Local FILE CUSTOMER [CUST]
 Filter [CUST] Where CATEGORY="A"
 Call NEW_FILT
 For [CUST]
   # Here, the filter has been changed by the NEW_FILT Subprog and is CATEGORY="B"
   ...
 Next
 Filter [CUST] Where CATEGORY="A"
 Call LOCAL_FILT
 For [CUST]
   # Here, the filter has not been changed by the LOCAL_FILT Subprog and is CATEGORY="A"
   ...
 Next
End

Subprog NEW_FILT
Local File [CUST]: # This is optional (it just checks that the table is opened)
Filter [CUST] Where CATEGORY="B"
 For [CUST]
   # Here, the filter has been changed and is CATEGORY="B"
 ..
 Next
End

Subprog LOCAL_FILT
Local File CUSTOMER [CUST] : # Here the table is reopened, the filter that follows will last only for the Subprog
Filter [CUST] Where CATEGORY="B"
 For [CUST]
   # Here, the filter has been changed and is CATEGORY="B"
 ..
 Next
End
```

  
After `Filter`, the variable [currind](4gl_currind.html) in the `[G]` class associated with the table is set to 1.

In terms of performance, the selection can be made on opening the table, or by `Filter`. This latter syntax gives more flexibility to writing routines since it can be changed or cancelled at any time.

General restrictions relating to [Where](4gl_where.html) and [Order By](4gl_order-by.html) clauses apply when they are used with `Filter`.

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | The abbreviation does not correspond to an opened table. |

# See also

[Where](4gl_where.html), [Order By](4gl_order-by.html), [Filter](4gl_filter.html), [For](4gl_for.html), [Trbegin](4gl_trbegin.html), [Link](4gl_link.html), [Read](4gl_read.html), [Delete](4gl_delete.html), [Update](4gl_update.html), [currind](4gl_currind.html).

  

[Index](index.html)  [Home](getting-started_home.html)