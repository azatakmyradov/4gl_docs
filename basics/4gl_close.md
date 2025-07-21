[Index](index.html)  [Home](getting-started_home.html)

Close

`Close` is used to free the `[F]` classes associated with tables and to free the cursors opened on the tables.

# Syntax

```
Close Local File CLASS_LIST
Close File CLASS_LIST
```

\* `CLASS\_LIST` is a list of table classes separated by commas. The corresponding tables must be opened.

# Examples

```
# Close all tables
Close Local File

# Close CUSTOMER [CUS] and ITEM [ITM] tables
Close Local File [CUS], [ITM]
```

# Description and comments

* The instruction `Close File`, where `Local` is omitted, is used to close the tables opened by `File` without `Local` clause. These syntaxes are deprecated and should no longer be used. Only `Local File` declaration and `Local Close` should be done.
* A new instruction called [LogicClose](4gl_logicclose.html) can also be used to close the table in an optimized manner. The buffer is cleaned but not freed.
* `Close Local File` without argument closes all the tables opened by a `Local File` command.
* Default lists of tables are updated by `Close Local File`.
* The `Close Local File` instruction is done within a transaction, and takes effect only when the transaction is ended by [Commit](4gl_commit.html) or [Rollback](4gl_rollback.html).

# Errors

| Error code | Description |
| --- | --- |
| 7 | Abbreviation not found. |

# See also

[File](4gl_file.html), [Local](4gl_local.html), [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html).

  

[Index](index.html)  [Home](getting-started_home.html)