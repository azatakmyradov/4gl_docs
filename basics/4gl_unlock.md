[Index](index.html)  [Home](getting-started_home.html)

Unlock

`Unlock` allows to unlock either a symbol or all the tables previously locked by the development partner.

# Syntax

```
   (1)  Unlock CLASS_LIST
   (2)  Unlock SYMBOL_LIST
```

* `CLASS_LIST` is a list of `CLASSES` separated by commas that correspond to opened tables.
* `SYMBOL_LIST` is a list of `SYMBOLS` separated by commas that correspond to locked symbols.
* `CLASS` is an abbreviation between square brackets with the syntax `[ABBR]` or `[F:ABBR]`.
* `SYMBOL` can have one of the following syntaxes:
  + `SYMB`
  + `SYMB` From FOLDER
  + `SYMB` From "`SERVER`@`FOLDER`"
  + =`EXPRESSION`
  + =`EXPRESSION` From `FOLDER`
  + =`EXPRESSION` From "`SERVER`@`FOLDER`"
* `SERVER` is the name of a SAFE X3 server.
* `FOLDER` is the name of a folder (by default, the current folder is used).
* `EXPRESSION` is an alphanumeric expression that returns the name of the symbol to be unlocked.
* `SYMB` is the symbol name (starts with an upper case letter, can include other upper case letters, digits, and underscores).

# Examples

```
   # Let's free the symbol SYMBOL that was previously locked
    Unlock SYMBOL

    # Let's free a record previously locked
     Readlock [TEST]CLE2(1) = date$
     If [S]fstat
        [TEST]ZONE += 100
        Rewrite [TEST]
        Unlock [TEST]
     Endif

    # Let's unlock a computed symbol
    SYMBOL = "MYLOCK"
    Lock =SYMBOL With lockwait = 0
    ...
    Unlock =SYMBOL
```

# Description

`Unlock` unlocks:

* A table locked by [Lock](4gl_lock.html).
* A symbol locked by [Lock](4gl_lock.html).
* All the records locked on a table by [Readlock](4gl_readlock.html) or by [For](4gl_for.html) [With](4gl_with.html) [Lock](4gl_lock.html) loop.

`Unlock` does not update the [fstat](4gl_fstat.html) variable.

`Unlock` works on tables only if no transaction was created by [Trbegin](4gl_trbegin.html). In a transaction, `Unlock` does not work (the [Commit](4gl_commit.html) or [Rollback](4gl_rollback.html) will release the locks).

# Comments

A lock on a table is automatically released when the table is closed. This means that a [Close](4gl_close.html), as well as a [LogicClose](4gl_logicclose.html) done on a [Local](4gl_local.html) [File](4gl_file.html) will implicitly unlock the table and its lines.

In a transaction, the updated lines are automatically locked and unlocked upon transaction end (by [Commit](4gl_commit.html) or [Rollback](4gl_rollback.html)). The symbols are not concerned by this automatic release of locks.

If a symbol lock is performed within a transaction, it is part of the transaction. If a [Rollback](4gl_rollback.html) occurs, the lock is reverted as all the updates done in the database.

You can lock symbols in another folder and even a server than the current one. In this case, [Unlock](4gl_unlock.html) frees all the locks created on the corresponding folder by the user.

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | The class does not exist (table not opened). |
| 10 | Argument has a bad data type. |

# See also

[Lock](4gl_lock.html), [Readlock](4gl_readlock.html), [For](4gl_for.html), [Close](4gl_close.html), [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), [Rollback](4gl_rollback.html), [adxtlk](4gl_adxtlk.html).

  

[Index](index.html)  [Home](getting-started_home.html)