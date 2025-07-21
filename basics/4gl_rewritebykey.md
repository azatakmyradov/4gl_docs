[Index](index.html)  [Home](getting-started_home.html)

Rewritebykey

This instruction updates a record at a given key after checking for edit conflicts. It compares the [Updtick](4gl_glossary-updtick.html) value of the [F] record with the [updtick](4gl_updtick.html) value of the corresponding database record, and it updates the database record only if the two ticks are equal.

This instruction allows CRUD operations to work safely in a multi-user environment without locking resources. The operation fails if the database record got modified after the [F] record had been read.

The `fstat` variable is set by this instruction. A status other than 0 indicates a failure.

# Syntax

This instruction requires an abbreviation, an index, and a key value.

* The abbreviation must match a `File` declaration.
* The index is either the name of one of the table's indexes or the name of a temporary index from an `Order By Key` clause.
* The key value is a list of expressions separated by semicolons.

All of these elements are optional.

* If the abbreviation is omitted, the default table is used. The default table is either the first table in the last `File` declaration, or the table declared by the last `Default File` instruction.
* If omitted, the default index value is the `Order By` index if present; otherwise, the default value is the first index of the table.
* If omitted, the default key value is the key of the corresponding [F] record.

All these elements can be omitted. The "maximum" and "minimum" syntaxes are:

```
RewriteByKey [abbreviation]index = key_value
RewriteByKey =
```

# Example

```
# Procedure that updates the currency code for a given customer only if the customer is active
Subprog CHANGE_CUSTOMER_CURRENCY(CUST_CODE, NEW_CURR, ERR_CODE,  ERR_MESSAGE)
 Const Char CUST_CODE(), NEW_CURR()
 Variable Integer ERR_CODE
 Variable Char ERR_MESSAGE()

# Declare the table
  If !clalev([BPC])
    Local File BPCUSTOMER [BPC]
  Endif

# Read the record
  Read [BPC]BPCNUM=CUST_CODE
  If fstat : ERR_CODE=fstat : ERR_MESSAGE="Customer"-CUST_CODE-"not found" : End : Endif

# Check if the condition is fulfilled
  If [BPC]BPCSTA=1 : ERR_CODE=8 : ERR_MESSAGE="Customer"-CUST_CODE-"not active" : End : Endif

# Update the record
  [BPC]CUR=NEW_CURR
  RewriteByKey [BPC]BPCNUM=CUST_CODE

# Check the fstat value
  ERR_CODE=fstat
  Case ERR_CODE
    When 0 : ERR_MESSAGE="Operation succeeded"
    When 1 : ERR_MESSAGE="Customer record is locked"
    When 3 : ERR_MESSAGE="Attempt to create a duplicate key"
    When 6 : ERR_MESSAGE="Customer record was modified"
    When 7 : ERR_MESSAGE="Customer record does not exist"
  Endcase
  End
```

# fstat values

| Value | Explanation |
| --- | --- |
| 0 | Operation succeeded |
| 1 | Record is locked |
| 3 | Duplicate value on unique index |
| 6 | Update conflict |
| 7 | Record does not exist |

# See also

[Updtick](4gl_glossary-updtick.html), [DeleteByKey](4gl_deletebykey.html).

  

[Index](index.html)  [Home](getting-started_home.html)