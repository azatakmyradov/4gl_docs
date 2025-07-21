[Index](index.html)  [Home](getting-started_home.html)

Rewrite

`Rewrite` allows you to rewrite a database line.

# Syntax

```
    Rewrite CLASS KEY READING_MODE KEY_VALUE
```

* `CLASS` is an optional clause that provides the table in which the `Rewrite` is done (by default, it will be the default table). The syntax is [`ABBR`], where `ABBR` is the abbreviation of an opened table.
* `KEY` is an optional key name with the following syntaxes:
  + `KEYNAME`.
  + `KEYNAME`(`INDEX_VALUE`).
* `KEYNAME` is the name of the key, and `INDEX_VALUE` is an expression providing the number of segments of keys used (by default, all).
* `READING_MODE` is one of the following keywords or symbols : [First](4gl_first.html), [Last](4gl_last.html), [Curr](4gl_curr.html), [Prev](4gl_prev.html), [Next](4gl_next.html), <, =, <=, >, or >=. By default, [Curr](4gl_curr.html) is used.
* `KEY_VALUE` is a list of expressions separated by semicolons. Every expression provides a key segment value that will be used for all the reading modes that compare the key with a value (<, <=, = >, >=). For [First](4gl_first.html), [Last](4gl_last.html), [Prev](4gl_prev.html), [Next](4gl_next.html), [Curr](4gl_curr.html), no `KEY_VALUE` is allowed. The expression must return a value with a type that corresponds with the type of the key segment.

# Examples

```
    # Let's read a line and modify it
     Trbegin TEST [TEST]
     Readlock [TEST]KEY2(1) = date$
     If [S]fstat
        [TEST]ZONE += 100
        Rewrite [TEST]
        Commit
       Else
        Rollback
     Endif

    # Let's shift lines (line number 2 values are written on line 1, line 3 on line 2...)
    # Works only if the table is not empty and if no key with no duplicates is present
     Read [TEST]KEY1 First
     Read [TEST]KEY1 Next
     While fstat=0
        Rewrite [TEST]KEY1 Prev
        Read [TEST]KEY1 Next
        Read [TEST]KEY1 Next
     Wend
```

# Description

`Rewrite` allows you to rewrite new values in a line read with one of the various modes:

| Mode | Description |
| --- | --- |
| First | The first line of the cursor defined by the file and filter if applicable. |
| Last | The last line of the cursor defined by the file and filter if applicable. |
| Next | The line that follows the current one in the cursor defined by the file and filter if applicable. |
| Prev | The line that is just before the current one in the cursor defined by the file and filter if applicable. |
| < value | The line with the biggest key value that is smaller than the given value. |
| <= value | The line with the biggest key value that is smaller or equal to the given value. |
| > value | The line with the smallest key value that is bigger than the given value. |
| >= value | The line with the smallest key value that is bigger or equal to the given value. |
| = value | The first line with the key value equal to the given value. |
| Curr | The current line (the last that has been read). |

The keys that can be used in `Rewrite` are the following:  
\* The key defined in an [Order By](4gl_order-by.html) clause if there is one.  
\* A key that has been defined in the dictionary.

If the key is omitted, the default key (provided by [G][currind](4gl_currind.html)) is used.

The [fstat](4gl_fstat.html) variable returns the status of the operation:

| Value | Description |
| --- | --- |
| 0 | The rewrite operation succeeded. |
| 1 | The line is locked. |
| 2 | With >= or <= mode, the key found was not equal to the value given. |
| 3 | An attempt of the creation of a duplicate key value was done. |
| 4 | Begin or end of table reached. |
| 5 | Line corresponding to the key value not found. |

When the `Rewrite` operation succeeds (for example, when [fstat](4gl_fstat.html) is equal to 0 or 2), the rewritten line becomes the default line.

# Comments

The behavior can be different depending on the database:  
\* In Oracle, the modification done by `Rewrite` will not be seen until the transaction ends.  
\* In SQl server, the modification can be seen directly.

You cannot use an abbreviation associated with a join by [Link](4gl_link.html) to rewrite a line.

The modification of a line must be done in a transaction.

The rewritten line will be locked until the transaction ends. If the line is already locked, [fstat](4gl_fstat.html) is set to 1.

When several lines have to be updated, use the [Update](4gl_update.html) instruction because it performs faster.

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | Class does not exist (no table opened with the corresponding abbreviation). |
| 8 | The number of values given, or the number of segments indicated, exceeds the number of segments of the key. |
| 21 | The key does not exist. |
| 22 | Incorrect read mode. |

# See also

[File](4gl_file.html), [Readlock](4gl_readlock.html), [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html), [Update](4gl_update.html), [Write](4gl_write.html), [Writeb](4gl_writeb.html), [Delete](4gl_delete.html), [RewriteByKey](4gl_rewritebykey.html), [DeleteByKey](4gl_deletebykey.html), [fstat](4gl_fstat.html).

  

[Index](index.html)  [Home](getting-started_home.html)