[Index](index.html)  [Home](getting-started_home.html)

Snapshot

This built-in method gives access to the [Snapshot](4gl_glossary-snapshot.html) image of an instance.

# Syntax

To access a property named "PROPERTY" in the snapshot:

```
This.snapshot.PROPERTY
```

# Example

```
# This program will check if a property has been modified in a class and in its parent class
# The main class is called SORDER, and includes a reference to LINE child classes.
# Here the code has been called on the line (This is a LINE instance)
$CONTROL_VAT
  # Access to a property of the instance (VAT) and another instance (snapshot) having the same properties
  If This.VAT<>This.snapshot.VAT : # The VAT value is no more the VAT value when data was read for update
     # Access to a property in the SORDER class by using APARENT instance (a default VAT rule)
     If This.VAT<>This.APARENT.DEFAULT_VAT
        # Was also the DEFAULT_VAT property modified ?
        If This.APARENT.DEFAULT_VAT<>This.APARENT.snapshot.DEFAULT_VAT
           # Here we are in the case where LINE.VAT was modified and DEFAULT.VAT also and they are different
        Endif
        ...
     Endif
   Endif
Return
```

# See also

[RevertToSnapshot](4gl_reverttosnapshot.html), [SnapshotEnabled](4gl_snapshotenabled.html), [getModified](4gl_getmodified.html), [modified](4gl_modified.html)

  

[Index](index.html)  [Home](getting-started_home.html)