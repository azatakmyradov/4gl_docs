[Index](index.html)  [Home](getting-started_home.html)

snapshotEnabled

This property of a class defines whether the [snapshot](4gl_glossary-snapshot.html) is enabled on the class (if equal to 1) or disabled (if equal to 0).

When a class is instantiated, the default value of this property is 0.

# Syntax

```
CLASSINSTANCE.snapshotEnabled
```

# Example

```
# This program will free a snapshot and consider (because snapshot is enabled) that a new snapshot will be
# created at the first modification of a property of the class
# The main class is called SORDER, and includes a reference to LINE child classes.
 Local Instance SORDER Using C_SALESORDER
 SORDER=newInstance C_SALESORDER AllocGroup Null
 OK=fmet SORDER.AREAD(ORDER_NUMBER)

# Now let's start the snapshot : Every modification done now will trigger the storage of the current value
 SORDER.snapshotEnabled=1
```

# See also

[freeSnapshot](4gl_freesnapshot.html), [revertToSnapshot](4gl_reverttosnapshot.html), [getmodified](4gl_getmodified.html), [modified](4gl_modified.html), [snapshot](4gl_snapshot.html) [Sage X3 Script Glossary Snapshot](4gl_glossary-snapshot.html)

  

[Index](index.html)  [Home](getting-started_home.html)