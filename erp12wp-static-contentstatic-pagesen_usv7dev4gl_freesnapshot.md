[Index](index.html)  [Home](getting-started_home.html)

Freesnapshot

This built-in method frees the [Snapshot](4gl_glossary-snapshot.html) of an instance.

# Syntax

```
MY_INSTANCE.freeSnapshot
```

# Example

```
 # SORDER is a sales order instance. Its AMOUNT is 1000 initially

 # Enable snapshot on SORDER
 SORDER.snapshotEnabled=1

 # Change the customer code and the amount
 SORDER.CUSTOMER_CODE="JOHNDOE"
 SORDER.AMOUNT=3000

 # Check the credit limit
 # if ok, we free the snapshot otherwise we revert to the snapshot.
 OK=Fmet SORDER.CHECK_CREDIT_LIMIT : # This is a method of the C_SALESORDER class
 If OK=1 : Credit limit ok
   SORDER.freeSnapshot
   # SORDER not modified but its snapshot has been discarded
 Else : # Credit limit is not ok
   SORDER.revertToSnapshot 
   # SORDER reverted to its original state
 Endif

 # If credit limit was ok, the snapshot has been freed and a new snapshot will be recreated when we modify 
 # AMOUNT again.
 SORDER.AMOUNT=5000

 # If credit limit was ok, SORDER.AMOUNT is 5000 and SORDER.snapshot.AMOUNT is 3000
 # Otherwise SORDER.AMOUNT is also 5000 but SORDER.snapshot.AMOUNT is 1000
```

# See also

[revertToSnapshot](4gl_reverttosnapshot.html), [SnapshotEnabled](4gl_snapshotenabled.html), [getmodified](4gl_getmodified.html), [snapshot](4gl_snapshot.html), [Sage X3 Script Glossary Snapshot](4gl_glossary-snapshot.html)

  

[Index](index.html)  [Home](getting-started_home.html)