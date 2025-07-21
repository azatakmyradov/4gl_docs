[Index](index.html)  [Home](getting-started_home.html)

Deletebykey

This instruction deletes a record at a given key after checking for edit conflicts. It compares the [UpdTick](4gl_glossary-updtick.html) value of the [F] record with the UpdTick of the corresponding database record and it deletes the database record only if the two ticks are equal.

This instruction allows CRUD operations to work safely in a multi-user environment without locking resources. The operation fails if the database record was modified after the [F] record had been read.

The `fstat` variable is set by this instruction. A status other than 0 indicates a failure.

# Syntax

```
DeleteByKey [ABV]KEY = KEY_VALUE
DeleteByKey KEY = KEY_VALUE
DeleteByKey [ABV]KEY =
DeleteByKey KEY =
DeleteBykey =
```

* `ABV` is the abbreviation of a table. It must match a [File](4gl_file.html) declaration.
* `KEY` is the description of the key used to access to the table. It can have one of the following syntax:
  + `KEYVAR` where `KEYVAR` is the code of a key declared in the dictionary or the name of a temporary index from an `Order By Key` clause.
  + `KEYVAR`(`INDEX`) where `INDEX` is a numeric expression giving the number of key parts considered for the condition.
* `KEY_VALUE` is a list of expressions separated by semicolons.

All these elements are optional.

* If the abbreviation is omitted, the default table is used, which is either the first table in the last [File](4gl_file.html) declaration, or the table declared by the last [Default](4gl_default.html) [File](4gl_file.html) instruction.
* If omitted, the index defaults to the `Order By` index if present; otherwise, it defaults to the first index of the table.
* If omitted, the key value defaults to the key of the corresponding `[F]` record.

# Example

```
# Procedure that deletes a given customer record only if the customer is not active
Subprog DELETE_INACTIVE_CUSTOMER(CUST_CODE, ERR_CODE, ERR_MESSAGE)
 Const Char CUST_CODE()
 Variable Integer ERR_CODE
 Variable Char ERR_MESSAGE()

  # Declare the table
  If !clalev([BPC])
    Local File BPCUSTOMER [BPC]
  Endif

  # Read the record
  Read [BPC]BPCNUM=CUST_CODE
  If fstat : ERR_CODE=fstat : ERR_MESSAGE="Customer"-CUST_CODE-"not found" : End : Endif

  # Check if inactive
  If [BPC]BPCSTA=2 : ERR_CODE=8 : ERR_MESSAGE="Customer"-CUST_CODE-"still active" : End : Endif

  # Delete the record
  DeleteByKey [BPC]BPCNUM=CUST_CODE

  # Check the fstat value
  ERR_CODE=fstat
  Case ERR_CODE
    When 0 : ERR_MESSAGE="Operation succeeded"
    When 1 : ERR_MESSAGE="Customer record is locked"
    When 6 : ERR_MESSAGE="Customer record was modified"
    When 7 : ERR_MESSAGE="Customer record does not exist"
  Endcase
  End
```

# fstat values

| Value | Explanation |
| --- | --- |
| 0 | Operation succeeded. |
| 1 | Record is locked. |
| 6 | Update conflict. |
| 7 | Record does not exist. |

# See also

[Updtick](4gl_glossary-updtick.html), [RewriteByKey](4gl_rewritebykey.html), [File](4gl_file.html), [fstat](4gl_fstat.html)

  

[Index](index.html)  [Home](getting-started_home.html)