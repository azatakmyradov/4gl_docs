[Index](index.html)  [Home](getting-started_home.html)

For

`For` is used to perform loops in two cases:  
\* Read loops on database tables or joins.  
\* Loops on index values or on a list of values.

# Syntax

```
(1)   For INDEX_VARIABLE = FIRST_VALUE To LAST_VALUE  STEP_CLAUSE
       ...
      Next INDEX_VARIABLE

(2)   For LIST_VARIABLE = LIST_OF_VALUES
       ...
      Next LIST_VARIABLE

(3)   For KEY_DESC HINT_CLAUSE FROM_TO_CLAUSE WHERE_CLAUSE WITH_CLAUSE
       ...
      Next

(4)   For (VARIA_LIST) From DATAB_TYPE Sql SQL_STATEMENT As  [CLASS]
      Next
```

## Syntax 1:

* `INDEX_VARIABLE` is a numeric value that will take its first value with the result of `FIRST_VALUE` and then vary by steps given by the `STEP_CLAUSE` (1 if no `STEP_CLAUSE` exists) until `END_VALUE` has been exceeded (the execution will continue after [Next](4gl_next.html)).
* `FIRST_VALUE` and `END_VALUE` are numeric expressions that give the beginning and the end of the loop.
* `STEP_CLAUSE` is an optional clause that gives the step value of the loop, with the following syntax: [Step](4gl_step.html) `STEP_VALUE`, where `STEP_VALUE` is a numeric expression that gives the value that increment the index variable at every loop.

## Syntax 2:

* `LIST_VARIABLE` is a variable that will successively take every loop all the values given in `LIST_OF_VALUES`.

## Syntax 3:

* `KEY_DESC` is a key description from a table or join, with the following syntax:
  + [`ABBREV`]`KEY_NAME`
  + `KEY_NAME`
  + [`ABBREV`]`KEY_NAME`(`GROUPING_LEVEL`)
  + `KEY_NAME`(`GROUPING_LEVEL`)
  + [`ABBREV`]
  + [`ABBREV`][reckey](4gl_reckey.html)
  + [reckey](4gl_reckey.html)
* `ABBREV` is the abbreviation of the table or the link in which the loop is performed (by default, the default table as indicated by [File](4gl_file.html) or [Default](4gl_default.html) [File](4gl_file.html)).
* `KEY_NAME` is the name of a key defined in the dictionary for the table, or given by an [Order By](4gl_order-by.html) syntax. By default, it is the default key as defined by [currind](4gl_currind.html).
* `GROUPING_LEVEL` is the number of key components used in the loop. Every loop will take a different key value if you consider the number of elements given by `GROUPING_LEVEL`. By default, the loop will be done on every selected line of the database.
* When the [reckey](4gl_reckey.html) keyword is used, no FROM\_TO\_CLAUSE is allowed.
* `HINT_CLAUSE` is an optional clause that defines a hint sent to the database. If this clause is ommitted, the engine acts as if the [With](4gl_with.html) [Nohint](4gl_nohint.html) had been sent. For more information, see [Hint](4gl_hint.html).
* `FROM_TO_CLAUSE` gives a key range for a loop on a table, with the following syntax : [From](4gl_from.html) `KEY_VALUE` [To](4gl_to.html) `KEY_VALUE`.
* `KEY_VALUE` is a list of at least one expression, separated by semicolons, that defines a value for the different segments of the key.
* `WHERE_CLAUSE` is an optional clause with the following syntax: [Where](4gl_where.html) `FILTER_EXPRESSION`, Where `FILTER_EXPRESSION` is an expression that filters the lines in the database. For more information, see [Where](4gl_where.html).
* `WITH_CLAUSE` is an optional clause that can have one of the two following syntaxes:
  + [With](4gl_with.html) [Lock](4gl_lock.html)
  + [With](4gl_with.html) [Stability](4gl_stability.html)

## Syntax 4

This is declared in the [following document](4gl_system.html).

# Examples

```
# Example 1: loop on a value with step 1
   Local Integer I,J
   For I=1 To 10
     J+=I
   Next I
   # At this point, I=11, and J=55

# Example 2: loop on a decimal value
  Local Decimal NUMBER
  Local Integer LOOP_COUNT
  For NUMBER=pi To 10 Step pi
    LOOP_COUNT+=1
  Next NUMBER
  # At this point, NUMBER is equal to 4*pi (the first value that exceeds 10) and LOOP_COUNT is equal to 3

# Example 3: descending loop
  Local Integer DOWN, LOOP_COUNT
  For DOWN=20 To 0 Step -4
    LOOP_COUNT+=1
  Next DOWN
  # At this point, DOWN is equal to -4 and LOOP_COUNT is equal to 6

# Example 4: Loop that will never be executed
  Local Integer I, STARTING_POINT,LOOP_COUNT
  Gosub SET_STARTING_POINT
  For I=STARTING_POINT To STARTING_POINT+3 Step -1
    LOOP_COUNT+=1
  Next I
  # At this point, LOOP_COUNT is equal to 0: as the range is ascending and the step descending no loop will be performed

# Example 5: Compute the planning for the first, third and fourth weeks of every month except June and July
  Local Char IMONTH(20)
  Local Integer IWEEK
  For IMONTH="January","February","March","April","May","September","October","November","December"
    For IWEEK=1,3,4
      Call GET_PLANNING(IWEEK,IMONTH)
    Next IWEEK
  Next IMONTH

# Example 6: Perform a loop for all the customers using the default key
  Local File CUSTOMERS [CUST]
  For [CUST]
    Call SEND_GREETINGS_MAIL([CUST]CUSTOMER)
  Next

# Example 7: Perform a loop for all the newly created customers using the default key 
  Local File CUSTOMERS [CUST]
  For [CUST] Where CRDATTIM>=format$("4Y[-]MM[-]DD",date$-10)+"T00:00:00Z"
    Call SEND_GREETINGS_MAIL([CUST]CUSTOMER)
  Next

# Example 8: Perform a loop for all the customer having a category between 3 and 5
  Local File CUSTOMERS [CUST] Order By Key CATEG=CATEGORY;CUSTOMER
  For [CUST]CATEG From 3 To 5
    Call SEND_ADVERTISING_MAIL([CUST]CUSTOMER)
  Next

# Example 9: Perform a loop for all the customer having a category between 3 and 5
#            Send them a letter depending on the country
  Local File CUSTOMERS [CUST] Where find(COUNTRY,"FRANCE","GERMANY","ITALY")<>0
&                             Order By Key CATEG=CATEGORY;COUNTRY;CUSTOMER
  For [CUST]CATEG(1) From 3 To 5
    # We will enter in this loop for every distinct value of CATEG
    For [CUST]CATEG(2)
      # We will enter in this loop for a given CATEG value for every distinct value of COUNTRY 
      MODEL=string$(COUNTRY="FRANCE","FRENCH")+string$(COUNTRY="GERMANY","GERMAN")+string$(COUNTRY="ITALY","ITALIAN")
      For [CUST]CATEG
        # This loop is performed for every customer for the CATEG and COUNTRY selected in the nesting loops.
        CALL SEND_MAIL(MODEL,[CUST]CUSTOMER)
      Next
    Next
  Next

# Example 10 : Update in a loop with lock with 2 conditions, one given by evalue(CONDITION), the other by  evalue(CONDITION1)
# Attention, this locks the whole set of data given by the first CONDITION until the commit or rollback is performed
  Trbegin MYTABLE [MYT]
  For [MYT] Where evalue(CONDITION) With Lock
    If evalue(CONDITION1) : Gosub UPDATE_MYT : Rewrite [MYT]
    Break (fstat<>0)
  Next
  If fstat : Rollback : Else : Commit : Endif

# Example 11: Perform a loop on all the lines of a table with no constraint on the reading order
  For [MYT]reckey Where evalue(CONDITION)
    ...
  Next
```

# Description

`For` .. `Next` instructions define loops that can be nested, either on variables (syntax 1 and 2), or on database tables or joins (syntax 3).

**The loop will terminate and the execution will continue after the [Next](4gl_next.html) instruction in the following cases:**  
\* If a [Break](4gl_break.html) is found in the loop. [Break](4gl_break.html) *N* allows to quit *N* nested `For`-`Next`, `Repeat`-`Until`, `While`-`Wend` loops.  
\* If the loop variable took a value out of the limits given by `FIRST_VALUE` and `LAST_VALUE` in syntax 1.  
\* If all the values found in the list have been successfully used in the loop execution (syntax 3).  
\* If all the lines satisfying the conditions and in the key range have been reached in the loop (syntax 3). The key range is defined when `For` are nested on successive partial keys to create breaks on these levels.  
\* In the `For` `With` `Lock` syntax, encountering a locked line does not end the loop, but [fstat](4gl_fstat.html) will be set to 1 after the corresponding `Next` execution.

**The final state after the `Next` is:**  
\* The value of `INDEX_VARIABLE`, `VALUE_VARIABLE`, or the current record if a break was executed.  
\* The first value that is strictly greater or smaller than `LAST_VALUE` in syntax 1 (depending if the loop is ascending or descending).  
\* The last value in `LIST_OF_VALUES` for syntax 2.  
\* The last line read in the table or the join for syntax 3.

**When the `For` instruction is executed, the following operations are performed:**  
\* **In syntax 1,** `FIRST_VALUE`, `LAST_VALUE` and `STEP_VALUE` are evaluated:  
 \* If `STEP_VALUE` is 0, an error is displayed.  
 \* If (`LAST_VALUE`-`FIRST_VALUE`)\*`STEP_VALUE` is negative, the loop is not executed, but `INDEX_VARIABLE` is assigned with `FIRST_VALUE`.  
 \* `INDEX_VARIABLE` is assigned with `FIRST_VALUE` and the loop is executed:  
\* **In syntax 2,** `VALUE_VARIABLE` is assigned with the first value found in `LIST_OF_VALUES`.  
\* **In syntax 3:**  
 \* If it is the unique loop done on the table or the first level of nesting, the SQL select is executed and a fetch is done to get the first line.  
 \* On a nested `For` level (on the same table and the same index, with a breaking level *B* that is greater than the previous one), no read is done, but the breaking conditions for the next are set to the *B* first components of the key.

**When the `Next` instruction is executed, the following operations are performed:**  
\* **In syntax 1,** `INDEX_VARIABLE` is incremented by `STEP_VALUE`. If the value of `INDEX_VARIABLE` goes out of the range given by (`FIRST_VALUE`, `LAST_VALUE`), the loop ends, otherwise the loop continues.  
\* **In syntax 2**, if not all the values in `LIST_OF_VALUES` have been explored, the next value on the list will be assigned to `INDEX_VARIABLE` and the loop will continue, otherwise the loop ends.  
\* **In syntax 3:**  
 \* If the `For` was done without `BREAKING_LEVEL` on the key, the next record will be fetched. If the end of the selection is reached, the loop ends, otherwise the loop will continue.  
 \* If a value *B* is given for `BREAKING_LEVEL`, lines will be fetched until at least a value of the *B* segments of the key. If the end of the selection is reached, the loop ends, otherwise the loop stops.

If the loop continues, the execution continues with the instruction that follows the `For` instruction associated with the `Next`. If the loop stops, the execution continues with the instruction that follows the `Next` instruction.

# Comments

## For syntax 1

The loop variable cannot be modified inside the loop. Only the `For` instruction changes its value at every step. `FIRST_VALUE`, `LAST_VALUE`, and `STEP_VALUE` are also fixed to the value given when the `For` was executed and cannot be changed.

## For syntax 3

The keys usable in a `For` are:  
\* When a table is used:  
 \* The key defined by the [Order By](4gl_order-by.html) if there is one.  
 \* The keys defined in the dictionary.  
\* When a join is used:  
 \* The key defined by the [Order By](4gl_order-by.html) clause on the link or on the [Filter](4gl_filter.html) if there is one.  
 \* The key defined in the last [Order By](4gl_order-by.html) clause on the main table of the [Link](4gl_link.html).  
 \* The keys defined in the dictionary for the main table of the [Link](4gl_link.html).

In a `For` loop where a `BREAKING_LEVEL` is given, the [G][currlen](4gl_currlen.html) variable is set with the `BREAKING_LEVEL` value.

If the abbreviation or the key is omitted:  
\* The default file is used as defined by [Default](4gl_default.html) [File](4gl_file.html), or [File](4gl_file.html).  
\* The default key is used:  
 \* The last key used if another access was previously done.  
 \* The key defined in the last [Order By](4gl_order-by.html) clause if there is one.  
 \* The first key by default.

At the end of the loop, [S][fstat](4gl_fstat.html) is set to 0 except if the end of the cursor was reached. [S]fstat will have a value set to 4.

When the `For`...`With Lock` syntax, the behavior might differ depending on the database:  
\* **With oracle,** the whole selection is locked immediately.  
\* **With SQL server,** the lines are locked successively and a locking issue will happen only when a locked line is encountered.  
When a locking issue happens, new read attempts will be done after a waiting time until the lock is released. The use of `For`...`With Lock` is discouraged.

The `WHERE_CLAUSE` and the `FROM_TO_CLAUSE` can only be used in the first `For` of the nested `For` on different breaking levels of a key. For example:

```
# Case that will not work
  Local File CUSTOMERS [CUST] Order By Key CATEG=CATEGORY;COUNTRY;CUSTOMER
  For [CUST]CATEG(1) From 3 To 5 : # Allowed because it is the first level of the nesting
    For [CUST]CATEG(2) Where find (COUNTRY,"FRANCE","USA")<>0 : # Syntax not allowed
      For [CUST]CATEG
       ...
      Next
    Next
  Next

# The right implementatipn
  Local File CUSTOMERS [CUST] Order By Key CATEG=CATEGORY;COUNTRY;CUSTOMER
&                             Where find (COUNTRY,"FRANCE","USA")<>0 : # The filter is set first
  For [CUST]CATEG(1) From 3 To 5 : # Allowed because it is the first level of the nesting
    For [CUST]CATEG(2)
      For [CUST]CATEG
       ...
      Next
    Next
  Next
```

  
When `For` is nested on a table and a key, the breaking levels indicated must be in increasing order. There is no constraint on the fact that they are consecutive. If no final `For` loop without breaking order exists, the lowest level of read will be grouped. For example, this is allowed:

```
  Local File MYTABLE [MYT] Order By Key MYKEY=A;B;C;D;E;F

  # Loop on all distinct values of (A,B)
  For [MYT]KEY(2)
    # Loop on all distinct values of (C,D) for a given value of (A,B)
    For [MYT]KEY(4)
      ...
    Next
  Next
```

  
There is a difference between Oracle and SQL server in the `For` loop when lines are inserted between the range of the `For` during its execution:  
\* **With Oracle,** the lines will not be visible.  
\* **With SQL server,** the lines will be visible, except if the clause [With](4gl_with.html) [Stability](4gl_stability.html) dedicated to this situation is used (this makes the execution slower).

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | Class does not exist (syntax 3). |
| 10 | FIRST\_VALUE, LAST\_VALUE or STEP\_VALUE are not numeric (syntax 1). |
| 10 | A value on the LIST\_OF\_VALUE is not consistent with the LIST\_VARIABLE data type (syntax 2). |
| 32 | Bad nesting order of breaking levels (syntax 3). |
| 41 | The STEP\_VALUE is 0 (syntax 1). |
| 43 | No more locks available (syntax 3). |

# See also

[To](4gl_to.html), [Step](4gl_step.html), [Next](4gl_next-loop.html), [Order By](4gl_order-by.html), [reckey](4gl_reckey.html), [Where](4gl_where.html), [With](4gl_with.html), [Lock](4gl_lock.html), [Stability](4gl_stability.html), [From](4gl_from.html), [System](4gl_system.html), [Hint](4gl_hint.html), [Nohint](4gl_nohint.html), [Break](4gl_break.html).

  

[Index](index.html)  [Home](getting-started_home.html)