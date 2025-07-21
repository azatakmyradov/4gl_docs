[Index](index.html)  [Home](getting-started_home.html)

Snapshots

## Definition

To manage updates on class instances, version 7 of the Sage X3 engine introduced a new concept called `Snapshot`. A snapshot is an initial copy of the state of a class instance, which allows the following features:

* Any property of the class instance can be modified by the process, but the snapshot will remain in the initial state copy.
* A comparison can be made between any property of the class and its snapshot copy.
* A return to the snapshot copy can be made for the complete class.
* A new snapshot that will replace the previous snapshot can be made any time.

This is useful when a CRUD operation is performed on complex classes. On any instance of a class and child classes, a snapshot can be managed and initialized after the read operation. Thus, it becomes very easy to identify, at any level of nested classes, what was modified.

The access to the snapshot instance of a class is performed by the syntax CLASS\_INSTANCE.Snapshot. For example, in a control method of a property called PROP1, `This.PROP1` will provide the current value of the property while `This.snapshot.PROP1` will provide the origin value of the property.

## Functions used to implement snapshots

Snapshots are automatically managed in the standard CRUD operation generated code, and it is almost unnecessary to manage the snapshots manually.

In a CRUD event, a snapshot value contains either the default values as they have been defined in the INIT rules (when a creation is requested), or the values read through the AREAD method when an update is requested).

The following functions are available to manually managed snapshots:

* `SnapshotEnabled` is a property of the class that can be set to 0 or to 1. When a class is instantiated, the default value of this property is 0. If set to 1, the snapshot will be managed, that is, every modification made on a property that was not previously modified will create a snapshot value with this previous value. If set to 0, no snapshot value will be created.
* `FreeSnapshot` is a method of the class that will destroy the snapshot values. If `Snapshotenabled` is still equal to 1, the current value of the class will be considered as future snapshot values when are modified.
* `RevertToSnapshot` is a method of the class that will replace the value modified in the class by its snapshot values, and then destroy the snapshot. If `SnapshotEnabled` is still equal to 1, the process will restart from the current value of the class that will then be considered as future snapshot values when they are modified.
* `getmodified` is a method of the class that fills arrays with the list of modified properties since the snapshot is enabled.

## Example

```
# Let's declare an instance pointer of a class called C_SALESORDER, containing at least the following properties:
# CUSTOMER, CREATION_DATE, PAYMENT_CODE, TOTAL_AMOUNT
Local Instance MYOR Using C_SALESORDER
Local Integer RETVAL

# Let's instantiate it
  MYOR=NewInstance SALESORDER AllocGroup Null

# Let's call the init method
# The default values set are: AMOUNT=1000, PAYMENT_CODE="CHECK"
  RETVAL = Fmet MYOR.AINIT

# ...or let's read an existing sales order
  RETVAL = Fmet MYOR.AREAD("12345") : # The order 12345 is supposed to have the same default values here


# Let's change a value, and check the snapshot
  MYOR.AMOUNT=2000

  If MYOR.snapshot.AMOUNT<>1000 or MYOR.AMOUNT<>2000
    # Will not happen, because the snapshot value is 1000 and the new value is 2000
  Elsif MYOR.PAYMENT_CODE<>MYOR.snapshot.PAYMENT_CODE
    # Will not happen because PAYMENT_CODE has not been modified
  Endif

  MYOR.PAYMENT_CODE="CREDIT_CARD"
  If MYOR.PAYMENT_CODE<>"CREDIT_CARD" or MYOR.snapshot.PAYMENT_CODE<>"CHECK"
    # Will not happen, because now the new value is "CREDIT_CARD" while the previous value is "CHECK"
  Endif

# Let's make a final test after reverting the snapshot
  MYOR.RevertToSnapshot
  If MYOR.PAYMENT_CODE<>"CHECK" or MYOR.AMOUNT<>1000
    # Will not happen, because the values of the instance have been reassigned with the snapshot values
  Endif
```

# Comments

The snapshot is created only at the first access when it has been enabled. If no modification has been performed and the snapshot is disabled, `This.snapshot` is equal to a `Null` pointer and accessing a property will then trigger an error. This never happens in normal CRUD operations because the snapshot is managed by the supervisor.

Creating a snapshot is not costly because a snapshot stores only the modified values and points on the class values if they are not modified.

The management of line deletion on collections has an impact on the snapshots, and it is important to use the ADELLINE method to perform them; otherwise, you might have unexpected results. The next example is a **bad example** of what should not be done by a development partner who manages the line deletion manually:

```
# MYORDER is an instance of a C_SALESORDER class
# it includes an array of references called LINES on instances of a C_SALESORDERLINE class
# MYORDER has already been read and instantiated, as well as MYORDER.LINES(1) and MYORDER.LINES(2)
# the snapshot is managed by the supervisor
# The lines have been instantiated with another allocation group

# The first modification that is done now is to delete line # 2
  FreeInstance MYORDER.LINE(2)

# Now let's set the line pointer #2 to Null
  MYORDER.LINE(2)=Null

# If we now try to revert the snapshot...
  MYORDER.revertToSnapshot

# Any line such as:
  LINE_AMOUNT=MYORDER.LINE(2).AMOUNT
# will trigger an error because MYORDER.LINE(2) does not point on a valid address !!!!

# The reason is the following:
# - when the FreeInstance was done, no snapshot existed (no modification had been done)
# - MYORDER.LINE(2) was deleted and not marked as deleted
# - The assignment of MYORDER.LINE(2) created a snapshot (too late) and copied the pointer in the snapshot
# Reverting the snapshot brought back a pointer on an invalid address
# This would not have been the case if any other modification had been done on the order before !!!

# If we want to write a code that works, we have to write the following lines
  Local Instance CURLINE Using C_SALESORDERLINE
  MYORDER.snapshotEnabled=1

# Let's save the value of the pointer on line 2
  CURLINE=MYORDER.LINE(2)

# Now let's set the line pointer #2 to Null: this creates the snapshot
  MYORDER.LINE(2)=Null

# Now we can free the instance. As there is a reference on it in a snapshot, it will only be flagged as deleted
  FreeInstance CURLINE

# If we now try to revert the snapshot, it will work because the line #2 will be considered as active again
  MYORDER.revertToSnapshot

# No more errors will happen here
  LINE_AMOUNT=MYORDER.LINE(2).AMOUNT
```

  

[Index](index.html)  [Home](getting-started_home.html)