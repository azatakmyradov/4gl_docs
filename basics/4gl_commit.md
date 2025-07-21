[Index](index.html)  [Home](getting-started_home.html)

Commit

`Commit` is used to validate a database transaction.

# Syntax

```
  Commit
```

# Examples

```
# This function debits an account 'ACCOUNT1' and credits and account 'ACCOUNT2' with an AMOUNT value.
# It manages a transaction except if a transaction is already in progress.
# Returns  [V]CST_AOK if the operation was successful, otherwise returns [V]CST_AERROR.

Funprog TRANSFER(ACCOUNT1, ACCOUNT2, AMOUNT)
Value Char ACCOUNT1(), ACCOUNT2()
Value Decimal AMOUNT
Local Integer IF_TRANS

# Start the transaction if no transaction is in progress
  Local File ACCOUNT
  If adxlog
    Trbegin ACCOUNT
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

# The operation is successful. If IF_TRANS=1, the transaction must been committed by the calling program
  If IF_TRANS=0 : Commit : Endif
End [V]CST_AOK
```

# Description and comments

* `Commit` is used to validate a database transaction, which is a set of operations that update the database tables (including counters). A transaction is started by a [Trbegin](4gl_trbegin.html) instruction.
* The tables opened before the transaction stay open, and files opened by [Trbegin](4gl_trbegin.html) or after [Trbegin](4gl_trbegin.html) are closed, except those redeclared using an existing abbreviation.
* `Commit` can only be carried out in the script or subprogram level that started the transaction.
* A unique level of transaction is supported by the Sage X3 engine. Thus, if a subprogram that performs an autonomous transaction can be called within another transaction, the [Trbegin](4gl_trbegin.html) / [Commit](4gl_commit.html) / [Rollback](4gl_rollback.html) instruction must be executed in the calling nested level. The fact that a transaction is already in progress is defined by the value of [adxlog](4gl_adxlog.html): if a transaction is in progress, its value is 1, otherwise is 0.
* `Commit` releases all the locks placed on the tables and records and the symbols locked during the transaction. `Commit` also releases locks placed before the start of the transaction, except for those placed on symbols.
* The database is only updated when `Commit` is executed. Before `Commit`, the new or modified data is not visible to other users.
* `Commit` does not return any particular status, except if the buffered database write operations are done by the `Writeb` operation. In that case, `fstat` will return an error status if a delayed write operation failed (the status has the same value as a [Write](4gl_write.html) operation that failed).

# Associated errors

| Code | Description |
| --- | --- |
| 32 | Transaction started at a higher level of the nesting call. |
| 48 | No transaction in progress. |

# See also

[File](4gl_file.html), [Trbegin](4gl_trbegin.html), [Rollback](4gl_rollback.html), [Onerrgo](4gl_onerrgo.html), [Read](4gl_read.html), [Write](4gl_write.html), [Writeb](4gl_writeb.html), [Rewrite](4gl_rewrite.html), [RewriteByKey](4gl_rewritebykey.html), [Delete](4gl_delete.html), [DeleteBykey](4gl_deletebykey.html), [Lock](4gl_lock.html), [adxlog](4gl_adxlog.html).

  

[Index](index.html)  [Home](getting-started_home.html)