[Index](index.html)  [Home](getting-started_home.html)

Trbegin

`Trbegin` is used to start a database transaction.

# Syntax

```
  Trbegin TABLE_LIST
```

* `TABLE_LIST` is a list of `TABLE` separated by commas.
* `TABLE` can be either a table name or an abbreviation of a table already declared.

# Examples

```
# This function debits an account ACCOUNT1 and credits and account ACCOUNT2 with an AMOUNT value
# It manages a transaction except if a transaction is already in progress
# It also updates a statistical table
# Returns  [V]CST_AOK if the operation was successful, otherwise returns [V]CST_AERROR.

Funprog TRANSFER(ACCOUNT1, ACCOUNT2, AMOUNT)
Value Char ACCOUNT1(), ACCOUNT2()
Value Decimal AMOUNT
Local Integer IF_TRANS

# Start the transaction if no transaction is in progress
  Local File ACCOUNT [ACC]
  If adxlog
    Trbegin [ACC], STATISTICS
    IF_TRANS=0
  Else
    # The transaction has been started by the calling program
    IF_TRANS=1
  Endif

# Debit operation (CODE is a unique index so only one database line is updated)
  Update ACCOUNT Where CODE=ACCOUNT1 With BALANCE=BALANCE-AMOUNT
  If fstat
    # If IF_TRANS=1, the transaction must been aborted by the calling program
    If IF_TRANS=0 : Rollback : Endif
    End [V]CST_AERROR
  Endif

# Credit operation
  Update ACCOUNT Where CODE=ACCOUNT2 With BALANCE=BALANCE+AMOUNT
  If fstat
    # If IF_TRANS=1, the transaction must been aborted by the calling program
    If IF_TRANS=0 : Rollback : Endif
    End [V]CST_AERROR
  Endif

# Updates account movement statistics
  Update [STA] Where STACODE="ACCOUNTS" With MOVEMENTS=MOVEMENTS+1
  If fstat
    # If IF_TRANS=1, the transaction must been aborted by the calling program
    If IF_TRANS=0 : Rollback : Endif
    End [V]CST_AERROR
  Endif

# The operation is successful. If IF_TRANS=1, the transaction must been committed by the calling program
  If IF_TRANS=0 : Commit : Endif
End [V]CST_AOK
```

# Description and comments

* `Trbegin` is used to start a database transaction, which is a set of operations that update the database tables including counters.
* If the `Trbegin` instruction is used with the abbreviation of a table that has been opened before, the [Filter](4gl_filter.html) options that have been previously placed on the table will continue to apply.
* If the `Trbegin` instruction is used with the name of a table that is not yet opened, the table will automatically be opened as a [Local](4gl_local.html) [File](4gl_file.html) instruction.
* If the `Trbegin` instruction is used with the name of a table that is already opened, the table will automatically be reopened as a [Local](4gl_local.html) [File](4gl_file.html) instruction. This means that the [Filter](4gl_filter.html) options that have been previously placed on the table will no longer apply. They will be restored after the end of the transaction.
* When the transaction ends, the tables opened before the transaction stay open and the tables opened by [Trbegin](4gl_trbegin.html) or after [Trbegin](4gl_trbegin.html) are closed, except those redeclared with an existing abbreviation.
* [Commit](4gl_commit.html) can only be carried out in the script or subprogram level that executed the [Trbegin](4gl_trbegin.html).
* A single level of transaction is supported by the Sage X3 engine. Thus, if a subprogram that performs an autonomous transaction is called within another transaction, the [Trbegin](4gl_trbegin.html) / [Commit](4gl_commit.html) / [Rollback](4gl_rollback.html) instructions must be executed in the calling nested level. The fact that a transaction is already in progress is defined by the value of [adxlog](4gl_adxlog.html): if a transaction is in progress, its value is 1, otherwise it is 0.
* Even if some tables have not been declared in `Trbegin`, but were opened before the transaction started, the updates on these tables will be parts of the transaction. They will be committed or rolled back on the [Commit](4gl_commit.html) / [Rollback](4gl_rollback.html) as well as the updates done on the table explicitly declared in `Trbegin`.
* The data updated in a transaction is automatically locked. It is therefore recommended to avoid writing transactions that are too long, and especially not to have a waiting loop inside a transaction (this would create deadlocks).
* Writing a transaction inside a [For](4gl_for.html) ... [With](4gl_with.html) [Lock](4gl_lock.html) syntax does not work properly. The transaction must include the [For](4gl_for.html) loop.

# Associated errors

| Code | Description |
| --- | --- |
| 7 | Abbreviation not found. |
| 20 | Table not found. |
| 27 | Table access error. |
| 28 | Table opened twice. |
| 29 | Too many tables opened simultaneously. |
| 32 | Transaction started at a higher level of the nesting call. |
| 49 | Transaction already in progress. |

# See also

[File](4gl_file.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html), [Onerrgo](4gl_onerrgo.html), [Read](4gl_read.html), [Write](4gl_write.html), [Writeb](4gl_writeb.html), [Rewrite](4gl_rewrite.html), [RewriteByKey](4gl_rewritebykey.html), [Delete](4gl_delete.html), [DeleteBykey](4gl_deletebykey.html), [Lock](4gl_lock.html), [adxlog](4gl_adxlog.html).

  

[Index](index.html)  [Home](getting-started_home.html)