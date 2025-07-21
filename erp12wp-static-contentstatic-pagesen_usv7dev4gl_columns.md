[Index](index.html)  [Home](getting-started_home.html)

Columns

`Columns` is used to limit the number of columns associated with a table:  
\* Loaded in the class [F] when reading the data by a [For](4gl_for.html), [Readlock](4gl_readlock.html) or [Read](4gl_read.html) instruction.  
\* Updated from the class [F] when writing the data by a [Rewrite](4gl_rewrite.html) or [RewriteByKey](4gl_rewritebykey.html) instruction.

# Syntax

```
Columns CLASS (FIELD_LIST)
Columns CLASS (FIELD_LIST) Extended
Columns CLASS
```

* `CLASS` is a class associated with the table opened by [File](4gl_file.html), or a join opened by [Link](4gl_link.html).
* `FIELD_LIST` is a list of columns in the table or join, separated by commas. The columns can be prefixed by the table abbreviation. This is especially useful when used in conjunction with a [Link](4gl_link.html).

# Examples

```
   # Read then rewrite limited to 2 fields, code and file name
   Local File BPARTNER [BPR]
   # Position of the filter on the code and client name
   Columns [BPR](BPRNUM,BPRNAM)
   For [BPR]
       ...
       Rewrite [BPR]
   Next
   # Filter deletion: all the columns are now available again
   Columns [BPR]

  # Column filter on the class derived from the link
  Local File ORDERS [ORD]
  Local File ITMMASTER [ITM]
  Link [ORD] with [ITM]ITM0=[F:ORD]ITMREF as [ORI]
  # Position of the filter on the product ref., the product dest., the order no.
  Columns [ORI]([ITM]ITMREF,[ITM]ITMDES1,[ORD]WIPNUM)
  For [ORI]
       ...
  Next
  # Filter deletion: all the columns are now available again
  Columns [ORI]

  # Column filter on the class that applies also on Read instruction
  Local File ORDERS [ORD]
  Columns [ORD] (ORDNUM,CUSTOMER) Extended
  Read [ORD]ORD0=MY_ORDER
  If [ORD]CUSTOMER=MY_CUSTOMER
    ...
  Endif

  # Column filters that excludes some columns
  # - those having some data types (Clob, Blob, strings with a max length over 50 characters)
  # - for columns having a dimension greater than 1, we will only include the 2 first indexes
  Local File ORDERS [ORD]
  # Let's first build the INCLUDE_LIST array by using the meta data stored in [G:ORD] class
  Local Char INCLUDE_LIST(250)
  Local Integer I,J,K
  INCLUDE_LIST=""
  For I=1 to dim([G:ORD]nbzon-1
    J=evalue("type([G:ORD]adxfname("+num$(I)+"))"
    K=evalue("dim([G:ORD]adxfname("+num$(I)+"))"
    If (J<=60 or J>265) and (J<>522) and (J<>523)
      INCLUDE_LIST+=string$(INCLUDE_LIST<>"",",")+[G:ORD]adxfname(I)+string$(K>2,"(0..1)")
    Endif
  Next I
  # Now the Columns can be done by evaluating a string constant that contains the list
  Columns [ORD] (=evalue('"'+INCLUDE_LIST+'"'))
```

# Description and comments

* By default, [Read](4gl_read.html) and [For](4gl_for.html) instructions perform `select *` SQL sentences on the database. This may be very costly if a large number of columns are present on the table. `Columns` is used to limit the access to the columns; in that case, the `select` sentence executed by the engine will send the list of columns given by the `Columns` instruction.
* The use of `Columns` is very cost effective when a large set of data is extracted from the database (usually with the [For](4gl_for.html) instruction). When a unique record is accessed by [Read](4gl_read.html) or [Readlock](4gl_readlock.html), the cost is lower, and thus `Columns` does not apply on [Read](4gl_read.html) or [Readlock](4gl_readlock.html) except if the [Extended](4gl_extended.html) keyword is used.
* `Columns` without a list of fields restore the default behavior for the future requests done on the table.
* At update time, the `Columns` instruction is not taken into account by the [Write](4gl_write.html) instruction that still manages class[F] as a whole, but only by [Rewrite](4gl_rewrite.html) and [RewriteByKey](4gl_rewritebykey.html).
* The class [F] variables excluded by the `Columns` instructions are still present, but they are no longer loaded or used for update by the corresponding instructions.
* A `Columns` instruction replaces a previous `Columns` instruction done on the same class.
* Elements in a column can be evaluated specifically with the syntax `=evalue(EXPRESSION)` where `EXPRESSION` is a string expression.
* When elements have a dimension, it is possible to limit the number of indexes considered by the syntax `FIELD(INDEX1..INDEX2)` where `FIELD` is a column of the table and `INDEX1` and `INDEX2` are constants giving the ranges of index.
* The column list for a table opened by [Local](4gl_local.html) [File](4gl_file.html) is managed at the right nesting level in the script. Thus, if a `Columns` instruction on a table is declared with [Local](4gl_local.html) [File](4gl_file.html) keywords, and a nested script executes another [Local](4gl_local.html) [File](4gl_file.html) keywords with a new `Columns` instruction, then the the list of table columns involved in the upper level `Columns` instruction remains unchanged after the execution of the inner level `Columns` instruction even if this one concerns another list of columns on the same table. This last point can be illustrated by the following example:

```
   # Read data in a loop with a filter on properties
   Local File BPARTNER [BPR]
   # Position of the filter on the code and client name
   Columns [BPR](BPRNUM,BPRNAM)
   For [BPR]
       ...
   Next

   # Call another subprogram
   Call MY_SUB

   # Read again the data
   # The data read is still restricted here to the BPRNUM and BPRNAM columns
   For [BPR] Where...
       ...
   Next
End

Subprog MY_SUB

   # Read data in the same table, but restricted on other properties
   Local File BPARTNER [BPR]
   # Position of the filter on the code and client name
   Columns [BPR](FCY,CRY,CRN)
   For [BPR]
       ...
   Next
End
```

# Errors

| Code | Description |
| --- | --- |
| 6 | Column does not exist in the table. |
| 7 | Class does not exist (table not opened). |
| 8 | Dimension given exceeds maximum dimension of the column. |

# See also

[File](4gl_file.html), [Link](4gl_link.html), [For](4gl_for.html), [Read](4gl_read.html), [Rewrite](4gl_rewrite.html), [RewriteByKey](4gl_rewritebykey.html).

  

[Index](index.html)  [Home](getting-started_home.html)