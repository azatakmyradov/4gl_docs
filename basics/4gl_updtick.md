[Index](index.html)  [Home](getting-started_home.html)

Updtick

This technical column is added in every database table when the table is validated in version 7 for the supervisor. This column stores a revision number for every line in the database. The revision numbers start at 1 when a line is created, and increment by 1 every time an update is made through a database trigger.

Updtick is also a system property that exists in every class or representation instance (it does not have to be declared in the class or representation dictionary). When a standard 'read' method is used on a persistent class, the `SetInstance` transfers the `Updtick` value from the database table to the class to manage concurrent updates.

For detailed information, see the [corresponding reference document](4gl_glossary-updtick.html).

# Syntax

```
[xxxx]Updtick
MYINSTANCE.Updtick
```

# Example

```
Subprog UPDATE_CUST(CUST_CODE,ERR_MSG)
Value Char CUST_CODE()
Variable Char ERR_MSG

# Table declaration
Local File CUSTOMER [CUST]
Local File CUSTOMER [CUS1]
Local Instance MY_CUSTOMER Using C_CUSTOMER

  Read [CUST]KEY=CUST_CODE
  If fstat
     ERR_MSG="Customer does not exist" : End
  Endif
  SetInstance MY_CUSTOMER With [CUST]
  Gosub LONG_PROCESS_UPDATING_MY_CUSTOMER_STEP_1
  Read [CUS1]KEY=CUST_CODE
  If MY_CUSTOMER.Updtick<>[CUS1]Updtick
     ERR_MSG="The customer was modified after step 1" : End
  Endif
  Gosub LONG_PROCESS_UPDATING_MY_CUSTOMER_STEP_2
  SetInstance [CUST] With MY_CUSTOMER
  # The RewriteByKey instruction performs the update only if Updtick has not changed
  RewriteByKey [CUST]KEY=CUST_CODE
  If fstat>=6
     ERR_MSG="The customer was modified or deleted after step 2" : End
  Elsif fstat<>=0
     ERR_MSG="AN error occured at update time fstat="+num$(fstat) : End
  Endif

  # At this step, as the update has been successful, [CUST]UPdtick is equal to MY_CUSTOMER.Updtick+1
  ERR_MSG="The customer record has been successfully updated to revision "+num$([CUST]Updtick)
End
```

# See also

[DeleteByKey](4gl_deletebykey.html), [RevertUpdtick](4gl_revertupdtick.html), [RewriteByKey](4gl_rewritebykey.html), [Updtick definition](4gl_glossary-updtick.html)

  

[Index](index.html)  [Home](getting-started_home.html)