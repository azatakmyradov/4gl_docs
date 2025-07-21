[Index](index.html)  [Home](getting-started_home.html)

Flush

`Flush` flushes the write buffer, which is filled by the [Writeb](4gl_writeb.html) instruction.

# Syntax

```
 Flush [CLASS]
```

* `CLASS` is the abbreviation of the table in which the flush is done. By default, the current table as defined by [File](4gl_file.html) or by [Default](4gl_default.html) [File](4gl_file.html) is considered.

# Example

```
# First example : let's create a set of account. fstat will be not null if an error occured
 Local File ACCOUNTS [ACC]
 Trbegin [ACC]
 For I=1 to dim([L]ACCOUNT_LIST)
   [ACC]ACCOUNT=[L]ACCOUNT_LIST(I)
   [ACC]TYPE=1
   [ACC]DESCRIPTION="Account"-num(I)
   Writeb [ACC]
   Break (fstat<>0)
 Next I
 If fstat=0
   Flush [ACC] : # Mandatory before Commit, otherwise the Commit would raise an error if lines not flushed
   If fstat=0
     Commit
   Else
     Rollback
   Endif
 Else
   Rollback
 Endif


# Second example: a subprogram that creates a set of records given by an array of instances
Subprog CREATE_RECORD(VALUES,NUMBER,RETURN_MESSAGE)
Variable Instance VALUES(1..) Using C_RECORD
Value Integer NUMBER
Variable Char RETURN_MESSAGE

Local File MYTABLE [MYT]
Local Integer I

  Trbegin [MYT]

# Let's create the lines with a buffer value of 10
  [S]adxwrb=10
  Gosub CREATE_REC
  If fstat=0
    Flush [MYT] : # Mandatory before Commit
    If fstat=0
      Commit
      RETURN_MESSAGE="SUCCESS"
      End
    Endif
  Endif

# If fstat is not null, retry again the transaction without buffering to identify the first line in error
  Rollback
  Trbegin [MYT]
  [S]adxwrb=0
  Gosub CREATE_REC
  If fstat=0 : # It might work at the second attempt
    # No Flush is necessary, because adxwrb is equal to 0
    RETURN_M_MESSAGE="SUCCESS"
    Commit
  Else       :  If not, the error message will contain the first line in error
    Rollback
  Endif
End

# Buffered write loop
$CREATE_REC
 For I=1 To NUMBER
   Setinstance [F:MYT] With VALUES(I)
   Writeb [MYT]
   If fstat<>0 : RETURN_MESSAGE="ERROR ON LINE"-num$(I) : Break
 Next I
Return
```

# Description and comments

The `Flush` instruction sends to the database the lines that have not already flushed when the [Writeb](4gl_writeb.html) syntax is used to create lines in the database. Note that an automatic flush is performed every [adxwrb]] lines.

When several lines have to be written in a database table, it is important to use the [Writeb](4gl_writeb.html) instruction instead of the [Write](4gl_write.html) syntax. The difference is that the lines are sent to the database by groups of [adxwrb](4gl_adxwrb.html) lines. This avoids too many exchanges with the database server and is therefore less time consuming. The only consequence is that the [fstat](4gl_fstat.html) value is returned only at flush time or for every [adxwrb](4gl_adxwrb.html) record. This means that the development partner can no longer identify the exact line where the error occurred; however, it is still possible to retry the create transaction with [adxwrb](4gl_adxwrb.html) equals to 0 (that disables the buffering).

It is mandatory to flush the write buffer before a [Commit](4gl_commit.html); otherwise, an error occurs if lines remain in the flush buffer at [Commit](4gl_commit.html).

Flush updates the [fstat](4gl_fstat.html) variable to give the result of the write operations, as indicated by the following table:

| fstat value | Description |
| --- | --- |
| 0 | The write operation has been successful. |
| 1 | The write operation failed due to locking issues. |
| 3 | The write operation failed on a duplicate key creation attempt. |

# See also

[Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html), [Writeb](4gl_writeb.html), [adxwrb](4gl_adxwrb.html), [adxftl](4gl_adxftl.html).

  

[Index](index.html)  [Home](getting-started_home.html)