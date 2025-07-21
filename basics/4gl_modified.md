[Index](index.html)  [Home](getting-started_home.html)

Modified

This attribute returns whether a property of an instance has been modified since the [snapshot](4gl_glossary-snapshot.html) has been enabled on the instance.

This attribute returns '1' if the property has been modified; otherwise, it returns '0'.

# Syntax

```
MY_INSTANCE.MY_PROPERTY.modified
```

# Example

```
  # Check if some properties have been modified to decide if a SORDER instance needs to be recomputed.
  If (SORDER.CUSTOMER.modified=1)    or (SORDER.CURRENCY.modified=1)
& or (SORDER.PAYMENTTERM.modified=1) or (SORDER.AMOUNT.modified=1)
& or (SORDER.DISCOUNT.modified=1)    or FORCE_RECOMPUTE=1
    OK=Fmet SORDER.RECOMPUTE
  Endif
```

# See also

[revertToSnapshot](4gl_reverttosnapshot.html), [freeSnapshot](4gl_freesnapshot.html), [SnapshotEnabled](4gl_snapshotenabled.html), [snapshot](4gl_snapshot.html), [Sage X3 Script Glossary Snapshot](4gl_glossary-snapshot.html),  
[SnapshotEnabled](4gl_snapshotenabled.html), [getmodified](4gl_getmodified.html).

  

[Index](index.html)  [Home](getting-started_home.html)