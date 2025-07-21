[Index](index.html)  [Home](getting-started_home.html)

Where

Use `Where` to add a filter:   
\* In a table declared by [File](4gl_file.html).   
\* On a join declared by [Link](4gl_link.html).   
\* On an update triggered by [Update](4gl_update.html) or [Delete](4gl_delete.html).   
\* On a read loop executed with [For](4gl_for.html).

# Syntax

```
   SYNTAX 1
   ... Where Key KEY_IDENTIFIER = EXPRESSION_LIST
   ... Where Key KEY_IDENTIFIER(INDEX_EXPRESSION)= EXPRESSION_LIST

   SYNTAX 2
   ... Where EXPRESSION
```

* `KEY_IDENTIFIER` is the identifier of one of the keys in the table.
* `INDEX_EXPRESSION` is an expression returning an integer that gives the number of elements of the key used. By default, the whole key is used.
* `EXPRESSION_LIST` is a list of expressions separated by semicolons. The number of expressions must at most be equal to the number of key components. The Nth expression type must fit the type of the Nth component of the key. The expressions are evaluated and the key component value is filtered with the result of the evaluation.
* `EXPRESSION` is a logical expression that can use operators, functions, columns from the tables concerned, and any other variables that are evaluated and considered as constant when the Where SQL statement described is executed.

**When using the syntax 2:**

* All the elements of the expressions that do not include columns of the table are evaluated and transmitted as values.
* The supported operators and functions used on table columns in the expression are directly transmitted to the database to optimize the cost of the request execution.
* The operator and function not supported are processed by the engine as additional filters.

The supported operators and functions are the following:

| Element | Description | Status and restrictions |
| --- | --- | --- |
| Comparison operators | =, <, >, <=, >=, <>. | Supported. |
| Arithmetic operators | +,-,\*,/,^. | Supported, except for '-' on string values. |
| Logical operators | [and](4gl_and.html), [or](4gl_or.html), [not](4gl_not.html), [xor](4gl_xor.html). | Supported. |
| String functions | [left$](4gl_left$.html), [right$](4gl_right$.html), [mid$](4gl_mid$.html), [seg$](4gl_seg$.html), [len](4gl_len.html), [num$](4gl_num$.html), [ctrans](4gl_ctrans.html), [tolower](4gl_tolower.html), [toupper](4gl_toupper.html), [val](4gl_val.html), [ascii](4gl_ascii.html), [chr$](4gl_chr$.html), [instr](4gl_instr.html), [pat](4gl_pat.html), [string$](4gl_string$.html), [space$](4gl_space$.html), [mid$](4gl_mid$.html), [vireblc](4gl_vireblc.html). | Supported. |
| Numeric functions | [abs](4gl_abs.html), [int](4gl_int.html), [ar2](4gl_ar2.html), [avg](4gl_avg.html), [var](4gl_var.html), [prd](4gl_prd.html), [pat](4gl_pat.html). | Supported. See comments on pat function. |
| Date functions |  | Not supported. |
| Multitype functions | [find](4gl_find.html), [min](4gl_min.html), [max](4gl_max.html), [uni](4gl_uni.html). | Supported except for date values. See also comments on find. |
| Special cases | [evalue](4gl_evalue.html). | Supported, but the evaluation is not done as it would be the case in an assignment: the expression is analyzed and transmitted as a 'where' clause. If the parameter transmitted to [evalue](4gl_evalue.html) is an array of strings, a global concatenation is done on all the indexes. |

# Examples

```
   # Select only the customer in category A
    Local File CUSTOMER Where CATEGORY="A"

   # On UNIX, select the files (not the directories) present in my home directory that don't belong to me
    File (D,L,U,G,T,M,J,A,N) From System "ls -l"-getenv$("HOME")
    & As [LSL] Where P <> getenv$("LOGNAME") and left$(D,1) = "d"

   # Join between sales orders and inactive carriers
   # Then select only the lines concerning a finite customer list given by an array
    Link SALESORDER With [CARR]CARRIER = [ORDER]CARRIER As [LNK] Where [CARR]ACTIVE = 1
    Filter [LNK] Where find (CUSTOMER,[L]CUST_LIST)<>0

   # Select a set of sales orders, and then loop on the lines.
   # [ORDLIN] is the order line table. It has a 2 components key called NUMLIG defined by order;order line
    For [ORDLIN]LINE(1) Where find(ORDNUM,[L]ORDER_LIST)<>0
       # Here an order is selected
       For [ORDLIN]NUMLIG(2)
         # Here the lines of the selected order are read in a loop
       Next : # Loop on the lines
    Next : # Loop on the orders

   # Evaluated Where
   Local Char CONDITION(200)(1..5)
   If ITEM_ACTIVE=2
      CONDITION(1)="ACTIVE=2 and (SUPPORT_DATE>=date$ or SUPPORT_DATE=[0/0/0])"
   Else
      CONDITION(1)="(1=1)" : # Always true
   Endif
   # Second condition: POLICY=1 if SERIE=2, POLICY=2 if LOT=2, POLICY=3 if SUBLOT=2, POLICY=0 otherwise
   CONDITION(2)=" & POLICY="+num$(find(1,SERIE=2,LOT=2,SUBLOT=2))
   # Third condition is given by an entry point
   Call ENTRY_POINT(CONDITION(3))
   If CONDITION(3)="" : CONDITION(3)="& (1=1)" : Endif
   Filter [ITEMS] Where evalue(CONDITIONS)
```

# Description

Use `Where` with [File](4gl_file.html), [Link](4gl_link.html), [Filter](4gl_filter.html), and [For](4gl_for.html) to filter the records sent, and with [Update](4gl_update.html) and [Delete](4gl_delete.html) to manage all the records fulfilling the conditions.

Several `Where` clauses added by different instructions on the same table are combined by a logical [and](4gl_and.html). A Filter instruction executed after a previous Filter instruction on the same table will replace the filter.   
For example:

```
 Local File CUSTOMER [CUST] Where ACTIVE=2
 Filter [CUST] Where COUNTRY="US"
 Link [CUST] With [CATEG]CATCOD=[CUST]CATEG As [CC] Where [CUST]CATEG>="B"
 For [CC] Where PAYTERM="CHQ"
   # Here, the condition that applies are ACTIVE=2 and COUNTRY="US" and CATEG>="B" and PAYTERM="CHQ"
 Next
 For [CUST] Where PAYTERM="CHQ"
   # Here, the condition that applies are ACTIVE=2 and COUNTRY="US" and PAYTERM="CHQ"
 Next
 For [CUST]
   # Here, the condition that applies are ACTIVE=2 and COUNTRY="US"
 Next
 Filter [CUST]
 For [CUST]
   # Here, the condition that applies are ACTIVE=2
 Next
```

  
When nested [For](4gl_for.html) loops are executed, a unique clause `Where` is allowed on the main loop.

The functions not supported are managed by the engine.   
For example:

```
 Local File CUSTOMERS [CUST]
 # This table has the following columns:
 #  - MANAGER, BUYER, PAYTERM , CATEGORY are string values
 #  - TRESHOLD is a denormalized array of 5 numeric values (0 to 4)
 #  - RANK is an integer value that goes from 1 to 10
 #  - LAST_REMINDER and FIRST_REMINDER are date values
 # Local variables are used as well:
 #  - PAYMENT_TERM is a character string
 #  - ALLOWED_RANKING is a integer array (10 indexes, every index value is 1 or 2)

  Filter CUSTOMERS Where
& ([CUST]PAYTERM=[L]PAYMENT_TERM or [CUST]MANAGER<>[CUST]BUYER)
& and find([CUST]CATEGORY,[L]CATEGORY_LIST)<>0
& and sum([CUST]TRESHOLD(1..3))>1000
& and [CUST]LAST_REMINDER-[CUST]FIRST_REMINDER>=5
& and [L]ALLOWED_RANKING([CUST]]RANK)=2
```

  
In the example provided above:

* The first filter is transmitted to the database as the following condition: `payterm = value given or manager=buyer`.
* The second filter is transmitted to the database as the following condition: `category in (list of values given by category_list)`.
* The third filter is transmitted to the database as the following condition: `treshold_1+treshhold_2+treshold_3>value of 1000`.
* The fourth and fifth filters are executed in a second step by the engine on the lines returned when the three first filters apply. The reason is that the fourth filter applies on date calculation, and the fifth filter uses an indexation operator based on a column value.

The fifth filter is different. It is preferable to write the following code to implement this kind of filter:

```
Local Char RANKING_LIST(250)
Local Integer I
 For I=1 to dim([L]ALLOWED_RANKING)
   If [L]ALLOWED_RANKING(I)=2
     RANKING_LIST+=","+num$(I)
   Endif
 Next I
 If RANKING_LIST<>""
   RANKING_LIST="find([CUST]RANK"+RANKING_LIST+")<>0"
 Else
   RANKING_LIST="(1=0)"
 Endif

 # Now we have a find([CUST]RANK,value1,value2...valueN)<>0 condition that is evaluated as an "in" by database
 Filter [CUST] Where evalue(RANKING_LIST)
```

# Comments

## Performance considerations

To obtain the best performance, it is always preferable to send as many filters as possible to the database because a filtering by the engine is always less effective.

Also, using the [or](4gl_or.html) operator can lead to performance issues. For example, if RANK is an integer column that can have values between 1 and 10: `RANK=4 or RANK=5 or RANK=6 or RANK=7` is less effective than `find(RANK,4,5,6,7)<>0`, which is less effective than `RANK>=4 and RANK<=7`. This might depend on the database optimizations.

The [pat](4gl_pat.html) and the [find](4gl_find.html) functions are transmitted to the database only if they are followed by an (equal to 0) or (different from 0) condition:

* `Where pat(COLUMN,PATTERN)<>0` is sent as `COLUMN like PATTERN`.
* `Where pat(COLUMN,PATTERN)=0` is sent as `COLUMN not like PATTERN`.
* `Where find(COLUMN,LIST)<>0` is sent as `COLUMN in (list)`.
* `Where find(COLUMN,LIST)=0` is sent as `COLUMN not in (list)`.

For example, `Where pat(CODE,"*AB*")<>0` is sent to the database as a `code like '%AB%'` filter, while `Where pat(CODE,"*AB*")` is managed by the engine and therefore much less effective. All the lines are sent by the database to the engine and filtered.

## Find with multi-dimension columns

Take care of the way [find](4gl_find) works on columns that are arrays. Let's imagine that you have a column MYCOL that has 3 occurrences in the database:

* When you write `Where find(MYCOL(0),1,2,3)`, the where clause sent to the database is `Where MYCOL_0 in (1,2,3)`
* When you write `Where find(MYCOL,1,2,3)`, all the index values of MYCOL are considered, but only the first one as a base for comparizon. This means that the where clause sent to the database is `Where MYCOL_0 in (MYCOL_1,MYCOL_2,1,2,3)`

## Tables with a big number of columns

If your table has more than 255 columns, take care that the columns with a rank over 255 cannot be used in a `Where` clause. To count the number of columns, you have to consider the dimensions. For instance, a field MYLIST with a dimension of 3 is considered as 3 columns in the table (MYLIST\_0, MYLIST\_1, MYLIST\_2).

# Associated errors

| Error code | Description |
| --- | --- |
| 4 | Function not authorized (syntax 2). |
| 10 | Type of expression incompatible with the key segment type (syntax 1). |
| 21 | Key does not exist (syntax 1). |

  

[Index](index.html)  [Home](getting-started_home.html)