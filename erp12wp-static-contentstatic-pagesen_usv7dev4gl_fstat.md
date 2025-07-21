[Index](index.html)  [Home](getting-started_home.html)

Fstat

`fstat` is a numeric status that is returned upon execution of a database operation, a sequential file operation, or a lock instruction.

# Syntax

```
fstat
```

# Examples

```
# MYTABLE is a table with a key called KEY1, that has a unique component called KEYVAL
# Create a record in the table MYTABLE with they key value 1 if it doesn't exist 
Local File MYTABLE [MYT]
Read [MYT]KEY1=1
If fstat
   [MYT]KEYVAL=1 : Write [MYT]
   If fstat
      MSG="The key was created in the mean time"
   Else
      MSG="Key created"
   Endif
Else
   MSG="Key already exists"
Endif
```

# Details

`fstat` is always set to '0' if the operation is successfully completed, and has a non-null value if there is an error:

* In a sequential read ([Getseq](4gl_getseq.html) and [Rdseq](4gl_rdseq.html)), `fstat` is set to '1' at the end of the file.
* On [Lock](4gl_lock.html), `fstat` is set to '1' if the lock could not be performed.
* For a database operation ([Read](4gl_read.html), [Look](4gl_look.html), [Readlock](4gl_readlock.html), [For](4gl_for.html), [Write](4gl_write.html), [Delete](4gl_delete.html), [Rewrite](4gl_rewrite.html), [DeleteByKey](4gl_deletebykey.html), and [RewriteByKey](4gl_rewritebykey.html)), the error statuses are from 1 to 7, as shown in the following table.

**Note that the use of literal numbers should be avoided: dedicated constants exist for this purpose.**

| Constant | Value | Explanation |
| --- | --- | --- |
| [V]CST\_AOK | 0 | Operation succeeded. |
| [V]CST\_ALOCK | 1 | Record is locked. |
| [V]CST\_AOUTSEARCH | 2 | In <= or >= read mode, indicates that read succeeded, but the key found is not equal to the value. |
| [V]CST\_ADUPKEY | 3 | Duplicate value on unique index. |
| [V]CST\_AOUTKEYS | 4 | Attempt of reading a key value that is smaller or greater than all existing key values. |
| [V]CST\_ANOREC | 5 | Record not read (no current record exists). |
| [V]CST\_ARECTICKUPD | 6 | Update conflict: the line no longer exists with the right updtick value (concurrency error during an update operation). |
| [V]CST\_ARECTICKDEL | 7 | Delete conflict: The line no longer exists with the right updtick value (concurrency error during a delete operation). |

# See also

[Getseq](4gl_getseq.html), [Rdseq](4gl_rdseq.html), [Lock](4gl_lock.html), [Read](4gl_read.html), [Look](4gl_look.html), [Readlock](4gl_readlock.html), [For](4gl_for.html), [Write](4gl_write.html), [Delete](4gl_delete.html),[Rewrite](4gl_rewrite.html), [DeleteByKey](4gl_deletebykey.html), [RewriteByKey](4gl_rewritebykey.html).

  

[Index](index.html)  [Home](getting-started_home.html)