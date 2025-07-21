[Index](index.html)  [Home](getting-started_home.html)

Writeb

`Writeb` has the same syntax as [Write](4gl_write.html), but allows you to optimize the performances when several insertions of database lines must be done.

# Syntax

```
   Writeb
   Writeb [CLASS]
```

* `CLASS` is a class identifier that corresponds to the abbreviation used to open a database table.

# Examples

```
# This script called by Gosub creates several lines in a table
# The creation is done by group of 10 lines
# If an error occures, an attempt is done again with no buffering
# If fstat is not null, it gives the lines where the error happens
$WR_MANY_LINES
  Trbegin MYTABLE [MYT]
  adxwrb=10 : # Reasonable value
  Gosub WR_LINES
  If fstat
    Rollback
    adxwrb=1
    Trbegin MYTABLE [MYT]
    Gosub WR_LINES
  Endif
  If fstat
    Rollback
  Else
    Commit
  Endif
Return

$WR_LINES
  For I=1 to NB_LINES
    Gosub ASSIGN_MYT
    Writeb [MYT]
    Break (fstat<>0)
  Next I
  If fstat=0
    If adxwrb>1 : Flush [MYT] : Endif
    If fstat=0
      Commit
    Else
      Rollback
    Endif
  Else
    Rollback
  Endif
Return
```

# Description

`Writeb` allows you to buffer the lines written in a database table before sending them globally. This instruction should be used when massive inserts are done in a given table.

* When [S][adxwrb](4gl_adxwrb.html) <= 1, `Writeb` works exactly as [Write](4gl_write.html).
* When [S][adxwrb](4gl_adxwrb.html) > 1, `Writeb` stores the lines to be written in a buffer, and flushes the buffer by transmitting the data to the database when reaching the buffer size, or when using the [Flush](4gl_flush.html) instruction.
* If a CLOB or a BLOB is present on the table, `Writeb` behaves exactly as [Write](4gl_write.html) (no buffering is done).

`Writeb` updates [fstat](4gl_fstat.html) to indicate the result of the write operation only when transmitting the data to the database. It is therefore not possible to identify the line in which the error occurred. The best practice is to run the transaction again with [S][adxwrb](4gl_adxwrb.html) set to 1. The [fstat](4gl_fstat.html) value will then be returned after every `Writeb`.

The values available for status are the following:

| fstat value | Description |
| --- | --- |
| 0 | The write operation has been successful (or has only been placed for the moment in the write buffer). |
| 1 | Lock error on at least a database line. |
| 3 | An attempt to create a duplicate key has been detected. |

# Comments

The [Flush](4gl_flush.html) instruction triggers the database write operation for all the lines sent in the buffer and not yet written. Using [Flush](4gl_flush.html) before the execution of [Commit](4gl_commit.html) is mandatory. If this is not done, the execution of [Commit](4gl_commit.html) fails if lines are still in the write buffer. Using [Flush](4gl_flush.html) also ensures that the lines can be created successfully.

The [Rollback](4gl_rollback.html) and [Commit](4gl_commit.html) instruction take into account all the lines written by [Write](4gl_write.html) as well as by `Writeb`.

The modification of the [adxwrb](4gl_adxwrb.html) variable creates an error if lines are still present in the write buffer. It is therefore important to [Rollback](4gl_rollback.html) or to [Flush](4gl_flush.html) before modifying this value.

The `Writeb` instruction uses a buffer with a greater size than the usual write buffers. It is important to consider a reasonable value for [adxwrb](4gl_adxwrb.html) to avoid an error "no more memory left" (31), or to increase the [sadmem](4gl_sadmem.html) memory sizing parameter. This parameter defines the memory used by the sadodbc and sadora processes. By default, its value is set to 20480.

If the order in which the write operations are performed is important, do not mix `Writeb`, [Write](../4gl/write.md), and [Update](../4gl/update.md). An example of incorrect code is as follows:

```
  # Incorrect use of Writeb and Update
  # When the Update is done, the record "ABC" has not been created
  adxwrb=10 : [F:MYT]MYKEY= "ABC" : [F:MYT]DESCRIPTION="My description": Writeb [MYT] 
  Update [F:MYT]MYKEY="ABC" With DESCRIPTION="Change the description"
```

# See also

[adxwrb](4gl_adxwrb.html), [Flush](4gl_flush.html), [For](4gl_for.html), [Write](4gl_write.html), [adxftl](4gl_adxftl.html), [fstat](4gl_fstat.html).

  

[Index](index.html)  [Home](getting-started_home.html)