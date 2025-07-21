[Index](index.html)  [Home](getting-started_home.html)

Lockwait

`lockwait` is an Integer system variable of the Integer type. It allows you to set the maximum of seconds that each lock attempt will last using the [Lock](4gl_lock.html) and [Readlock](4gl_readlock.html) instructions.  
After a first failed lock attempt, the system will retry every second for the duration defined by the `lockwait` value.

## Syntax

```
 lockwait

 Lock ... with lockwait=...
 Readlock ... with lockwait=...
```

## Comments

If the value of `lockwait` is negative, the attempt time will be unlimited. If its value is null, a single attempt will be made.

The [Lock](4gl_lock.html) or [Readlock](4gl_readlock.html) syntax `With lockwait =...` allows you to assign this variable only for the instruction considered.

`lockwait` is not taken into account by `For... With Lock` syntax, nor by the [Update](4gl_update.html) instruction. A single attempt will be made for these instructions.

## Examples

```
# Update a counter value with a five seconds waiting time when conflict occurs
  Trbegin
  Raz BADLOCK
  Lock COUNTER With lockwait = 5
  If fstat
     BADLOCK = 1
     Rollback
  Else
     [C]COUNTER += 1
     Commit
  Endif

# Set the lockwait value to 0 (return immediately an error in case of locking issue)
  lockwait=0
  Readlock [MYT]KEY=MYKEY
  If fstat=1
    # The record has already been locked
    ...
  Endif
```

  

[Index](index.html)  [Home](getting-started_home.html)