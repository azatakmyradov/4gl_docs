[Index](index.html)  [Home](getting-started_home.html)

Lock

`Lock` is used to lock either a symbol or a table.

# Syntax

```
   Lock CLASS_LIST
   Lock CLASS_LIST with lockwait=INTEGER_EXPR
   Lock SYMBOL_LIST
   Lock SYMBOL_LIST with lockwait=INTEGER_EXPR
```

* `CLASS_LIST` is a list of `CLASS` separated by commas.
* `CLASS` is a class code between square brackets that corresponds to an opened table.
* `SYMBOL_LIST` is a list of `SYMBOL` separated by commas.
* `SYMBOL`can either be:
  + A constant name in uppercase characters, starting with a letter, which can include digits and underscores.
  + An evaluated symbol with the syntax =`EXPRESSION`, where `EXPRESSION` is an evaluated expression that returns a string result.
  + A constant name followed by `From` `FOLDER`.
  + A constant name followed by `From` `server@FOLDER`.
* `INTEGER_EXPR` is an evaluated expression that returns an integer value.

# Examples

```
  # Let's lock a symbol: [fstat](../4gl/fstat.md) value will immediately be returned
  Lock ACCOUNTING With lockwait=0

  # Let's lock a symbol in another folder: if not successful after 1 seconds, fstat will be returned
  Lock FOLDER_MGT From X3 With lockwait=1

  # Lock an entire table
  Lock [SALES] With lockwait=5

  # Lock a symbol and stay until the lock is ok
  Lock SILLY with lockwait=-1

  # Lock a computed symbol
  Lock ="ACC"-[ACC]ACCOUNT_ID
```

# Description

The `Lock` instruction is used to perform a complete database lock of a table, or to lock a symbol:

* Locking a table in the database will prevent any user to use the table. This should be reserved only in very rare cases.
* Locking a symbol can be used to have a mutual exclusion on a resource identified by the code. This means that every development partner who needs access to this resource has to perform the lock (it is more based on a convention, there is no control on the resource by itself).

If the lock is unsuccessful, locking attempts are done until the time given by the [With](4gl_with.html) [lockwait](4gl_lockwait.html) option is over. If no [With](4gl_with.html) [lockwait](4gl_lockwait.html) option is given, the system uses the default value given by the [lockwait](4gl_lockwait.html) variable value. A negative value tries to lock until the success occurs (it might create deadlocks and is therefore strongly discouraged). A null value will make an attempt and immediately return the result in [fstat](4gl_fstat.html) variable.

Unlocking a locked resource is done by [Unlock](4gl_unlock.html) and should occur quickly to avoid deadlocks.

After execution of `Lock`, the `fstat` variable returns the following values:

* **0** if the resources have been successfully locked.
* **1** if the lock couldn't be done.

The `Lock` SYMBOL stores a record in a table which name is given by [S][adxtlk](4gl_adxtlk.html) (by default, APLLCK). This record persists only if an [Unlock](4gl_unlock.html) is not performed. This method is used in version 6 to perform pessimistic locks on object records (the key being the object abbreviation followed by the main key value). The disadvantage of this technique is that it might create contention on the APLLCK table if a huge number of update transactions are done through version 6 objects.

Therefore, this technique is no longer used in version 7 style programming based on optimistic locks that use [RewriteByKey](4gl_rewritebykey.html) instructions.

Importantly, the symbol `Lock` should be done outside a transaction; otherwise, the locking status will not be returned and the system will wait until the lock is no longer present.

If a `Lock` is done on a list of resources, it will be considered as successful only if all the locks could be done successfully. If this is not the case, [(fstat]] is set to '1' and all the resources are unlocked.

# Comments

## Lock symbols

If several symbols need to be locked simultaneously, it is important to use a single `Lock` instruction with a list of symbols rather than several locks that could trigger deadlocks at execution time.

There is no link between a symbol that is supposed to control the access to a resource and the resource itself (a resource being a counter sequence, or a call to a function that should be executed in mutual exclusion). What is important is that when a symbol is locked by a user, it cannot be locked by another user. This means that if the counter sequence can be changed by a development partner that does not lock the symbol before, no control can be done.

The table where the locks are stored must not be changed, although it might be possible to change some of its characteristics if they are protected by an activity code (for example, enlarge the size of the symbols that can be stored (column LCKSYMB).

A symbol lock is done at the folder level, but a lock can be done in another folder. It might be important if you need to manage a mutual exclusion for some operations that imply all the folder of the solution; in that case, the lock should be placed on the root folder - usually X3.

Removing a symbol lock is done by [Unlock](4gl_unlock.html). However, if a transaction is in progress, the [Unlock](4gl_unlock.html) will take effect only when the transaction is committed.

When a `Lock` symbol is placed on another folder, the corresponding unlock will unlock all the symbols locked on this folder by the user.

## Lock on tables

* Locking a single line in the database is done with [Readlock](4gl_readlock.html).
* Locking a set of lines can be done with [For](4gl_for.html) [With](4gl_with.html) [Lock](4gl_lock.html).
* Locking all the lines uses [Lock](4gl_lock.html).

If the table has been successfully locked, any individual lock done by other users will fail.

A lock on a table is automatically released if the table is closed, and also if a transaction in progress is committed or rolled back; [Commit](4gl_commit.html) and [Rollback](4gl_rollback.html) release, and the symbol `Lock` placed within the transaction (but not the ones placed outside a transaction).

When massive locks are done in a transaction, depending on the database, it might be possible to run out of resource locking. If this happens, an error #43 is triggered. The locking policy can be different from a database version to another. For example, SQL server can sometimes lock the table if the number of locks exceeds a given portion of the table.

Locking a line on a table cannot be done by using the [Link](4gl_link.html) abbreviation if a join has been created on the table; it must be the abbreviation of the table itself.

# Associated errors

| Error code<:th> | Description |
| --- | --- |
| 7 | The class abbreviation does not correspond to an opened table. |
| 10 | The expression giving the symbol locked does not return a string value. |
| 43 | Out of locking resources. |

  

[Index](index.html)  [Home](getting-started_home.html)