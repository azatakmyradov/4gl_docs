[Index](index.html)  [Home](getting-started_home.html)

Adxtlk

`adxtlk` is a [Char](4gl_char.html) variable. It defines the name of the table that stores the logical locks.

# Syntax

```
adxtlk
```

The Sage X3 engine manages logical locks with a dedicated instruction called [Lock](../4gl/lock.md). This instruction creates a record in a database table which name is defined by the variable `adxtlk`.

The variable `adxtct` returns the name of this table (APLLCK).

# See also

[adxtct](4gl_adxtct.html), [adxtms](4gl_adxtms.html), [Lock](4gl_lock.html), [Unlock](4gl_unlock.html).

  

[Index](index.html)  [Home](getting-started_home.html)