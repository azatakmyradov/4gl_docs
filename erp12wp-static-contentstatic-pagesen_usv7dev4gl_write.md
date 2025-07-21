[Index](index.html)  [Home](getting-started_home.html)

Write

`Write` allows you to insert a new line in a database table.

# Syntax

```
   Write
   Write [CLASS]
```

* `[CLASS]` is an abbreviation of an opened table. By default, the default table as defined by [Default](4gl_default.html) [File](4gl_file.html) is used.

# Examples

```
   # Extract of a AINSERT "hand written" method on a class : let's create a header and lines
    Trbegin HEADER [HEAD], LINES [LINE]
    SetInstance [HEAD] with this
    Write [HEAD]
    If fstat=0
      For I=1 to maxtab(this.LINES)
        If this.LINES(I)<>Null
           SetInstance [LINE] with this.LINES(I)
           Write [LINE]
           Break (fstat<>0)
        Endif
      Next I
    Endif
    If fstat=0
      Commit
    Else
      Rollback
    Endif
```

# Description

`Write` allows you to insert a line in the database.

[fstat](4gl_fstat.html) indicates the result of the operation:

| Value | Description |
| --- | --- |
| 0 | The write operation succeeded. |
| 1 | The table is locked. |
| 3 | An attempt to create a duplicate key value was done. |

A `Write` instruction does not modify the current record. If the current record must be the written one, it is necessary to perform a read operation.

# Comments

The behavior can be different depending on the database:

* In Oracle, the lines created by `Write` are not seen until the transaction ends.
* In SQL Server, they can be seen directly.

It is not possible to use an abbreviation associated with a join by Link to write a line.

The creation of a line must be done in a transaction.

The written line is locked until the transaction ends.

When several lines must be written on a given table, it is best to use the [Writeb](4gl_writeb.html) instruction that performs faster.

If the table is locked by [Lock](4gl_lock.html) [`ABBREV`], the other users cannot insert lines and will get a [fstat](4gl_fstat.html) value equal to 1.

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | Class does not exist (no table opened with the corresponding abbreviation). |
| 27 | A write attempt was done on a [Link](../4gl/link.md) abbreviation. |
| 44 | No more space to create lines. |
| 65 | No more space to create lines. |
| 75 | Database error. |

# See also

[File](4gl_file.html), [Readlock](4gl_readlock.html), [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html), [Update](4gl_update.html), [Rewrite](4gl_rewrite.html), [Delete](4gl_delete.html), [RewriteByKey](4gl_rewritebykey.html), [DeleteByKey](4gl_deletebykey.html), [Writeb](4gl_writeb.html), [fstat](4gl_fstat.html).

  

[Index](index.html)  [Home](getting-started_home.html)