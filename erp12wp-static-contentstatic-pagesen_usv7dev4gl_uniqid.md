[Index](index.html)  [Home](getting-started_home.html)

Uniqid

`uniqid` allows you to generate a unique series of long integer for every database table.

# Syntax

```
   uniqid (CLASS)
```

* `CLASS` is the abbreviation of a table that must be opened with the syntax `[ABBR]` or `[F:ABBR]`.

# Examples

```
   # Let's assign a unique id to a line in my table
    [F:MYT]ID = uniqid([MYT])
    Write [MYT]
```

# Description

`uniqid` returns a unique long integer value for a given database table. These numbers are attributed sequentially and can therefore by used as an access key.

The next number to be assigned can be transferred by copy of the table, by backup and restoration, or by revalidation of the table. If a number is assigned in a transaction and a [Rollback](4gl_rollback.html) is performed, the number will never be recovered. Thus, lines numbered by a sequence may not be consecutive.

The implementation of this function is based on a database sequence created for every table.

The type of result is [integer](4gl_integer.html).

# Comments

For a newly created table, the number sequence starts at 1. A RTZ on the table will also restart the sequence from 1.

As holes can be present in the sequence when [Rollback](4gl_rollback.html) is performed, this function is not suitable if lines need to have a sequential numbering with no lost number. Other supervisor resources (counters) are available to assign document numbers to database records.

The `uniqid` function executes even if the table is locked.

`uniqid` does not update [S][fstat](4gl_fstat.html).

UUID handling functions have been added in the SAFE X3 languages; therefore, using UUIDs to manage unique identifiers for database lines is preferred.

# Troubleshooting with unique ID keys

A number is used in some database tables to get a unique key. If for any reason the sequence has been recreated independently from the table, errors with duplicate keys will happen when attempts are done to create new lines.

A script like the example below can be executed to restore the situation:

```
$GET_UNIQID
  Read [F:X4R]X4R1 Last
  [M:X4R1]IDFLX=uniqid([F:X4R])
  While [M:X4R1]IDFLX<=[F:X4R]IDFLX
    [M:X4R1]IDFLX=uniqid([F:X4R])
  Wend
Return
```

  
A SQL request can also be used to know the last sequence number used for 'MYTABLE' (on the `FOLDER` folder):

* **On the Oracle database:**

```
Select last_number from user_sequences where sequence_name =âSEQ_MYTABLEâ;
```

* **On the SQL server database:**

```
select value from SS_SEQUENCE where usr='FOLDER' and name='MYTABLE'
```

You can also change the sequence number through a database connection, but you must be connected as a single user:

* **On Oracle database:**

  ```
  Drop sequence SEQ_MYTABLE;
  Create sequence SEQ_MYTABLE increment by 1 start with <MAX+1> ;
  Grant select on SEQ_MYTABLE to USER_ADONIX;
  Grant select on SEQ_MYTABLE to ADMIN_ADONIX;
  ```
* **On the SQL server database:**

  ```
  update SS_SEQUENCE set value=<MAX> where name='MYTABLE' and usr='FOLDER'
  ```

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | The table is not opened. |

# See also

[Read](4gl_read.html), [Write](4gl_write.html), [Rewrite](4gl_rewrite.html), [Update](4gl_update.html), [RewriteByKey](4gl_rewritebykey.html), [DeleteByKey](4gl_deletebykey.html), [Readlock](4gl_readlock.html), [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html).

  

[Index](index.html)  [Home](getting-started_home.html)