[Index](index.html)  [Home](getting-started_home.html)

Rollback

`Rollback` is used to end a database transaction and comes back to the situation before the beginning of the transaction ([Trbegin](4gl_trbegin.html)).

# Syntax

```
  Rollback
```

# Examples

```
# This subprogram debits an account ACCOUNT1 and credits and account ACCOUNT2 with an AMOUNT value
# It manages a transaction except if a transaction is already in progress
# OPERATION_STATUS returns [V]CST_AOK if the operation was successful, otherwise it returns [V]CST_AERROR.
# If a fatal error happens, OPERATION_STATUS returns [V]CST_AFATAL

Subprog TRANSFER(ACCOUNT1, ACCOUNT2, AMOUNT, RATE, OPERATION_STATUS)
Value Char ACCOUNT1(), ACCOUNT2()
Value Decimal AMOUNT,RATE
Variable Integer OPERATION_STATUS
Local Integer IF_TRANS

# Manage the exceptions
  Onerrgo ABORT_TRANS

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
  Update ACCOUNT Where CODE=ACCOUNT1 With BALANCE=BALANCE-ar2(AMOUNT/RATE)
  If fstat
    # If IF_TRANS=1, the transaction must been aborted by the calling program
    If IF_TRANS=0 : Rollback : Endif
    OPERATION_STATUS=[V]CST_AERROR
    End
  Endif

# Credit operation
  Update ACCOUNT Where CODE=ACCOUNT2 With BALANCE=BALANCE+ar2(AMOUNT/RATE)
  If fstat
    # If IF_TRANS=1, the transaction must been aborted by the calling program
    If IF_TRANS=0 : Rollback : Endif
    OPERATION_STATUS=[V]CST_AERROR
    End
  Endif

# The operation is successful. If IF_TRANS=1, the transaction must been committed by the calling program
  If IF_TRANS=0 : Commit : Endif
  OPERATION_STATUS=[V]CST_AOK
End

# Error management
# This may happen for instance when RATE is 0 (division by zero)
$ABORT_TRANS
  If IF_TRANS=0 : Rollback : Endif
  OPERATION_STATUS=[V]CST_AERROR
End
```

# Description and comments

* `Rollback` is used to abort a database transaction, which is a set of operations used to update the database tables including counters. A transaction is started by a [Trbegin](4gl_trbegin.html) instruction.
* The tables opened before the transaction stay open, files opened by [Trbegin](4gl_trbegin.html) or after [Trbegin](4gl_trbegin.html) are closed, except for those redeclared using an existing abbreviation.
* `Rollback` can only be carried out in the script or subprogram that started the transaction. The `Rollback` instruction can be found in an error rerouting script called by [Onerrgo](4gl_onerrgo.html).
* A unique level of transaction is supported by the SAFE X3 engine. Thus, if a subprogram that performs an autonomous transaction can be called within another transaction, the [Trbegin](4gl_trbegin.html) / [Commit](4gl_commit.html) / [Rollback](4gl_rollback.html) instruction must be executed in the calling nested level. The fact that a transaction is already in progress is defined by the value of [adxlog](4gl_adxlog.html): if a transaction is in progress, its value is 1; otherwise, the value is 0.
* `Rollback` releases all the locks placed on the tables and records and the symbols locked during the transaction. `Rollback` also releases locks placed before the start of the transaction, except from those placed on symbols.
* `Rollback` does not return any particular status.

# Associated errors

| Code | Description |
| --- | --- |
| 32 | Transaction started at a higher level of the nesting call. |
| 48 | No transaction in progress. |

# See also

[File](4gl_file.html), [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Onerrgo](4gl_onerrgo.html), [Read](4gl_read.html), [Write](4gl_write.html), [Writeb](4gl_writeb.html), [Rewrite](4gl_rewrite.html), [RewriteByKey](4gl_rewritebykey.html), [Delete](4gl_delete.html), [DeleteBykey](4gl_deletebykey.html), [Lock](4gl_lock.html), [adxlog](4gl_adxlog.html).

  

[Index](index.html)  [Home](getting-started_home.html)