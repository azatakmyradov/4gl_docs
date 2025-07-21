[Index](index.html)  [Home](getting-started_home.html)

Adxlog

`adxlog` is a variable that states if a database transaction has already been started (by [Trbegin](4gl_trbegin.html)).

# Syntax

```
adxlog
```

`adxlog` can have two values:

* **'0' :** if no transaction is in progress.
* **'1' :** if a transaction is in progress.

This is especially useful when a function performs several updates that have to be executed either autonomously as a consistent transaction, and can be executed in a bigger transaction.

# Example

```
# A stock movement increases the quantity from a location A and decreases the same quantity from a location B
# This function can be called within a transaction or autonomously

Funprog STOCK_MOVE(LOC_A, LOC_B, PRODUCT, QUANTITY)
Value Char LOC_A(), LOC_B(), PRODUCT()
Value Decimal QUANTITY

Local Shortint IFTRANSAC

  IFTRANSAC=adxlog

  If IFTRANSAC=0 : Trbegin [STO] : Endif

  Update [STO] where LOC=LOC_A With QTY=QTY+QUANTITY

  If fstat=0
    Update [STO] where LOC=LOC_B With QTY=QTY-QUANTITY
   Endif

   If fstat
     If IFTRANSAC=0 : Rollback : Endif
     End [V]CST_AERROR
   Endif

   If IFTRANSAC=0 : Commit : Endif

End [V]CST_AOK
```

  

[Index](index.html)  [Home](getting-started_home.html)