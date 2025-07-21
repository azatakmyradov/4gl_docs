[Index](index.html)  [Home](getting-started_home.html)

Delete

`Delete` is used to delete one or several lines from a database table.

# Syntax

```

Delete [ABV]
Delete [ABV] KEY MODE
Delete [ABV] KEY MODE KEY_VALUE
Delete [ABV] MODE
Delete [ABV] MODEK KEY_VALUE

Delete
Delete KEY MODE
Delete KEY MODEK KEY_VALUE
Delete MODE
Delete MODEK KEY_VALUE

Delete [ABV] Where CONDITION
Delete Where CONDITION
```

* `ABV` is the abbreviation of a table. It must match a [File](4gl_file.html) declaration.
* `KEY` is the description of the key used to access the table. It can include one of the following syntaxes:
  + `KEYVAR` where `KEYVAR` is the code of a key declared in the dictionary or the name of a temporary index from an `Order By Key` clause.
  + `KEYVAR`(`INDEX`) where `INDEX` is a numeric expression giving the number of key parts for the condition. When omitted, all the key parts are used.
* `KEY_VALUE` is a list of expressions separated by semicolons.
* `MODEK` is one of the following operators: `=`, `<`, `<=`, `>=`, `>`.
* `MODE` can be `MODEK` or the [Curr](4gl_curr.html) keywords.
* `CONDITION` is a logical condition based on columns in the table and constants or variable available in the context.

# Examples

```
 # First example : let's read a record and delete it
 # When no argument is given, the mode is Curr, the table is the default one
 Local File CUSTOMER [CUST]
 Read [CUST]CODE="JOHNDOE"
 If fstat=0
   Delete
 Endif


 # Second example : let's delete invoice lines
 # If no transaction  is opened, a transaction is performed
 # Otherwise, the transaction is supposed to be done at the previous level
 Funprog DELETE_INVOICE(INV_CODE)
 Value Char INV_CODE()
 Local Integer RETURN_STATUS, IF_TRANSACTION
 Local File INVOICE [INV], INVLINES [INL]
 IF_TRANSACTION=adxlog

 # Let's perform the header record deletion
 If IF_TRANSACTION : Trbegin INVOICE, INVLINES : Endif
 Delete [INV]CODE=INV_CODE
 RETURN_STATUS=fstat

 # Error handling : the only status that is a real error is when a locking problem occurs
 If RETURN_STATUS=[V]CST_ALOCK
   If IF_TRANSACTION : Rollback : Endif
   End RETURN_STATUS
 Elsif adxdlrec=0
   # No record deleted, so no line has to be deleted
   # This can be considered as an error or not (if yes, we could return [V]CST_AOUTSEARCH)
   If IF_TRANSACTION : Commit : Endif
   End 0
 Endif

 # Let's delete the lines
 Delete [INL]CODE(1)=INV_CODE
 RETURN_STATUS=fstat
 If RETURN_STATUS<>[V]CST_ALOCK : RETURN_STATUS=0 : Endif

 # Error handling
 If IF_TRANSACTION
   If RETURN_STATUS
     Rollback
   Else
     Commit
   Endif
 Endif

 End RETURN_STATUS


 # Third example : deletion of all the lines in a table in one transaction
 # If a lot of lines are there, it will be faster to destroy the table and to recreate it
 Local File TEMPTABLE [TMP]
 Delete [TMP] Where KEY>= ""
```

# Description and comments

`Delete` is used to delete lines from a table according to various modes listed below. Three cases can occur:

* With `Curr` mode: the current line is deleted.
* With modes `<`, `<=`, `=`, `>=` and `>`, all the lines corresponding to the selected read mode are deleted. If a [Where](4gl_where.html) clause has been specified in the [File](4gl_file.html) declaration or with an additional [Filter](4gl_filter.html) instruction, the filtering is taken into account.
* With a [Where](4gl_where.html) clause, all the selected lines (including [File](4gl_file.html) and [Filter](4gl_filter.html) defined [Where](4gl_where.html)) are deleted.

If no key value is specified for the modes that require one ( `<`, `>`, `<=`, `>=`, `=` ), the current value of the variables of class `[F]` corresponding to the file is used.

When no key is provided, the last key used to access the table is used. If no previous access was done since the [File](4gl_file.html) instruction, the key defined by [Order By](4gl_order-by.html) clause (the first key by default) is used.

When a [Where](4gl_where.html) clause is given, the database identifies by itself the most appropriate key to be used depending on the clause.

`Delete` does not modify the content of the variables of the corresponding class `[F]`.  
  
`Delete` sets the system variable [adxdlrec](4gl_adxdlrec.html) that contains the number of deleted lines.  
[fstat](4gl_fstat.html) contains the return status of the delete operation. Only the following values can be returned by [fstat](4gl_fstat.html):

| Status value | Description |
| --- | --- |
| [V]CST\_AOK (0) | The lines have been successfully deleted, or not matching record has been found ([adxdlrec](../4gl/adxdlrec.md) is equal to 0). |
| [V]CST\_ALOCK (1) | Some lines are locked. |
| [V]CST\_AOUTSEARCH (2) | with <= or >= mode, no line strictly equal to the key value has been found. This is not really an error ([adxdlrec](4gl_adxdlrec.html) lines have been deleted). |

There is a small difference of behavior between the SQL server and Oracle when the 'Delete... Where' syntax is used. If the 'where' clause cannot be directly sent to the database and has to be executed by the engine, a deletion loop with locking option is done. If a locking problem is encountered:

* As Oracle locks the lines before starting the deletion, the locking status is returned by Oracle before any 'Delete' has been made.
* As SQL server locks the records during the deletion process, it is returned by the SQL server when one of the records to be deleted is only locked.

This can happen with such a code example:

```
 Local File SALESORDER [ORD]
 Trbegin SALESORDER
 # STATUS can have a value from 1 to N
 # A local variable array gives, for every status, if the case is blocking or not

 # Such a syntax cannot be transmitted to the database
 Delete [ORD] Where [L]BLOCKING_CASE([ORD]STATUS)=0

 If fstat=[V]CST_ALOCK
   # If oracle, no line has been deleted
   # If SQL server, some lines can have been deleted
   # So if we Commit here, the state is unexpected here !!! 
 Endif


 # A much better code would be the following
 Local Char CONDITION(250)
 If sum([L]BLOCKING_CASE)<>0
   CONDITION="find([ORD]STATUS"
   For I=1 to dim([L]BLOCKING_CASE)
     If [L]BLOCKING_CASE(I) : CONDITION+=","+num$(I) : Endif
   Next I
   CONDITION+=")=0"
   # CONDITION contains now an expression like : "find([ORD]STATUS,1,5,8)=0"
   Delete [ORD] Where evalue(CONDITION) : # This will send a "not in" clause with a list of constants
 Endif
```

# Associated errors

| Error | Description |
| --- | --- |
| 7 | The [F] class does not exist (table not declared). |
| 8 | The number of given values or the index mentioned exceeds the number of elements of the key. |
| 22 | Read mode incorrect. |
| 21 | The key does not exist for this table. |
| 27 | File declared in "read only" mode in the table dictionary. |
| 43 | No more locks available. |

# See also

[File](4gl_file.html), [Where](4gl_where.html), [For](4gl_for.html), [fstat](4gl_fstat.html), [adxdlrec](4gl_adxdlrec.html).

  

[Index](index.html)  [Home](getting-started_home.html)