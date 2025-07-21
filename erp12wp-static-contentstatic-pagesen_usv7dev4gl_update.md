[Index](index.html)  [Home](getting-started_home.html)

Update

`Update` allows you to update a list of database lines defined by a [Where](4gl_where.html) condition with values transmitted as parameters.

# Syntax

```
   Update CLASS WHERE_EXPR With ASSIGNMENT_LIST
```

* `CLASS` is an optional argument that defines an opened table with the [`ABBRV`] syntax, where `ABBREV` is the abbreviation of an opened table. If omitted, the default table is used.
* `WHERE_EXPR` is a where clause with the following syntax: [Where](4gl_where.html) `EXPR`, where `EXPR` is a logical expression using constants and columns of the tables. For more information about the rules, see the [Where](4gl_where.html) documentation.
* `ASSIGNMENT_LIST` is a list of ASSIGNMENTS separated by commas.
* `ASSIGNMENT` is an assignment of columns from the table with the syntax `COLUMN_NAME`=`EXPRESSION`, `EXPRESSION` being an expression that can include columns of the table as well as constants or variables in the context. The assignments `COLUMN_NAME`+=`EXPRESSION`, `COLUMN_NAME`-=`EXPRESSION` are also allowed.

# Examples

```
   # The active flag is set to 1 (false) for all the customer having CREDIT and DEBIT equal to 0
   # Return the number of lines updated
    Funprog CLEAN_CUSTOMER
    Local File CUSTOMER [CUST]
    Update [CUST] Where DEBIT = 0 and CREDIT = 0 and FLGACT <> 1
    & With FLGACT = 1
    End [S]adxuprec

   # Increment the number of edition done and set the last edit date
    Update [DIV] Where FLAGEDIT & KEY >= KEY1 With NBEDIT += 1, LASTEDIT=date$

   # Set the pay for customer to the customer code if not defined
    Update [CUST] Where PAYCUST="" With PAYCUST=CUSTCODE
```

# Description

`Update` allows you to update columns in a table in one instruction that performs the read, lock, update, and unlock globally. It is much more efficient to use this syntax when several lines have to be updated.

The conditions that can be used are defined in the [Where documentation](4gl_where.html).

`Update` sets the [fstat](4gl_fstat.html) variable to indicate how the operation worked:

| fstat value | Description |
| --- | --- |
| 0 | The update was done successfully, [adxuprec](../4gl/adxuprec.md) records have been updated. |
| 1 | A lock was found and the transaction has been rolled back. |
| 3 | At least an update tried to create duplicated keys, so the transaction was rolled back. |

# Comments

An Update that assigns a column with a column that is updated in the same update is unpredictable. For example:

`Update [MYT] With COL1=VALUE1, COL2=COL1+1` gives an unpredictable result for COL2.

The way the locked records are handled may differ from the database implementation:

* **Oracle** locks first all the lines and updates them.
* **Sql server** locks the lines progressively as they are modified.

In both cases, if a lock is detected, the database waits until the lock is released and finally if it is not (deadlock), stops the update and returns with [fstat](4gl_fstat.html) equal to 1.

`Update` does not modify the content of the [F] class associated with the table.

You cannot use a join abbreviation (set by [Link](4gl_link.html)) to perform an update.

The `Update` must be done inside a transaction, and all the lines are updated. If the transaction implies a great number of lines, it may be that an error 43 (too many locks) is triggered. If this happens, the set-up of the database lock must be changed, or the transaction split in smaller transactions.

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | Class does not exist (table not opened). |
| 10 | Data types of expression don't correspond to the data types of the column assigned. |
| 43 | Too many locks used. |

# See also

[Where](4gl_where.html), [Readlock](4gl_readlock.html), [File](4gl_file.html),[Rewrite](4gl_rewrite.html), [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html), [fstat](4gl_fstat.html), [adxuprec](4gl_adxuprec.html), [Filter](4gl_filter.html).

  

[Index](index.html)  [Home](getting-started_home.html)