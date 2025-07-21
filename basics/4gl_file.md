[Index](index.html)  [Home](getting-started_home.html)

File

`File` is used to declare the tables that can be used in a script.

# Syntax

```
   Local File FILEDEC_LIST
   File FILEDEC_LIST
```

* `FILEDEC_LIST` is a list of `FILEDEC` separated by commas.
* **`FILEDEC` can have one of the following syntaxes:**

  ```
  FIL_NAME
  FIL_NAME Order By ORDER_LIST
  FIL_NAME Where CONDITION
  FIL_NAME Where CONDITION Order By ORDER_LIST
  ```
* **`FIL_NAME` can have one of the following syntax:**
  `FILE_NAME
  FILE_NAME [CLASS]
  [CLASS]
  ( VARIABLE_LIST ) From System STRING_EXPRESSION As [CLASS]
  (VARIA_LIST) From Variable ARRAY_LIST As [CLASS]`
* **`FILE_NAME` can be:**

  + A table identifier such as ATABLE.
  + A table identifier from another folder with the syntax `FOLDER_NAME.FILE_NAME`.
  + A table identifier from another folder located on another server with the syntax `[email protected]_NAME`.
  + A string constant that embeds one of the three previous syntaxes.
  + A string expression prefixed by an equal sign: `=STRING_EXPRESSION`.
* `CLASS` is the identifier of a class (up to eight characters). When only [CLASS] is given in the previous syntax list, the table must already be declared, and no [Where](4gl_where.html) clause is allowed.
* `FOLDER_NAME` is the identifier of a folder. By default, it is the current folder known by the variable [nomap](4gl_nomap.html).
* `STRING_EXPRESSION` is a valid expression whose evaluation returns a character string value.
* `VARIABLE_LIST` is a list of valid variable names separated by commas, which indicates the name of the column returned by the System order.
* `SERVER` is the name or the IP address of a server in which a runtime of the Sage X3 engine has been installed and in which a folder is installed. SERVER can be followed by the service number if it is not the same as the current one (the syntax becomes `SERVER:[email protected]_NAME`).
* `CONDITION` is an evaluated condition that can include constants, variables, columns from the table, and functions and operators to filter only some lines on the table. For more information about how the `CONDITION` is managed by the engine, see the [Where](4gl_where.html) documentation.
* `ORDER_LIST` is a list of elements that defines an Order By in the SQL sentence. For more information, see the [Order By](4gl_order-by.html) documentation.
* `VARIA_LIST` is a list of `VARIA` separated by commas.
* **`VARIA` can have one of the following syntaxes:**

  + `DECLARATION` `VARNAME`.
  + `DECLARATION` `VARNAME` ( `INDEX_SEP` ).
* `DECLARATION` is a declaration keyword that can be [Char](4gl_char.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Date](4gl_date.html), [TinyInt](4gl_tinyint.html), [Decimal](4gl_decimal.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Datetime](4gl_datetime.html), or [Uuident](4gl_uuident.html). If `DECLARATION` is [Char](4gl_char.html), `VARNAME` must be followed by `(N)` where `N` is the maximum size of the string, before a possible list of (`INDEX_SEP`).
* `VARNAME` is a variable name starting with a letter, and followed by letters, digits, or underscores.
* `INDEX_SEP` is a list of `DIMENSION` or `DIMENSION_RANGE` separated by commas. If N commas are given, it describes an array of dimension N+1. The number of commas is therefore limited to three.
* `DIMENSION_RANGE` has the following syntax : `DIMENSION`..`DIMENSION`.
* `DIMENSION` is an expression returning a numeric dimension.
* `ARRAY_LIST` is a list of `ARRAY_VARIABLE` that contains the values of the different columns value for the records of a "pseudo-table" in memory. `ARRAY_VARIABLE` has the following syntax : `VARNAME`(`DIMENSION_RANGE`). All the arrays presented must have the same dimension; the number of elements in the list must correspond to the number of elements in `VARIA_LIST`.

# Examples

```
   # Declaration of two tables: SALESORDER with its default abbreviation, and CUSTOMER with [CST] as abbreviation.
   Local File SALESORDER, CUSTOMER [CST]

   # Use of 2 account tables from 2 accounting folder ACCOUNTING1 and ACCOUNTING2. 
   # my_server.my_domain is the network name of the server where ACCOUNTING1 folder is installed,
   # the second folder is installed on the current application server.
    Local File "[email protected]" [ACC1], "ACCOUNTING2.ACCCOUNT" [ACC2]

   # Declaration of one table twice with different abbreviations.
   # This can be useful to perform joins within the same table
    Local File ACCOUNT [GACC1], ACCOUNT [GACC2]

   # Declaration of 5 already opened tables.
    Local File [A1],[A2],[A3],[A4],[A5]

   # ITEMS table with a filer and an order by clause
    Local File ITEMS [ITM] Where [ITM]ITMKEY >= "fzzz" Order By Key A = [ITM]ITMCATEG Desc

   # Let's compute the global size of files belonging to the "sage" group present in a directory on UNIX
    Local Integer TOTAL_SIZE
    Local File (D,L,P,G,T) From System "ls -l" As [SYS] Where [SYS]G = "sage"
    For [SYS] : [L]TOTAL_SIZE += val([F:SYS]T) : Next

   # Let's create a table in memory and use it
   Local Char MY_KEY(20)(1..200)
   Local Integer MY_VALUE(1..200)
   Local Date MY_DATE(1..200)
   Local Integer NB_REC
   Gosub FILL_TABLE : # Fills MY_KEY, MY_VALUE, MY_DATE arrays and returns NB_REC as the number of records
   Local File (Char THEKEY(20), Integer AMOUNT, Date POSTING_DATE)
&  From Variable MY_KEY(1..NB_REC), MY_VALUE(1..NB_REC), MY_DATE(1..NB_REC)
&  As [MEM] Order By POSTING_DATE
   For [MEM]
     # For every loop, we have [MEM]THEKEY, [MEM]AMOUNT, [MEM]POSTING_DATE available (found in MY_* arrays)
     # This type of table is usable only in read mode
   Next
```

# Description and comments

**File is used to declare the tables used in a routine. A table can be:**

* **A database table** (located on the same server and the current folder by default):

  + If the folder is not specified and the table not found in the current folder, an attempt is done successively in the folder hierarchy given by [adxmother](4gl_adxmother.html).
  + If the abbreviation used for the table is not given in the syntax, the default abbreviation defined in the dictionary is used by default.
  + If only the abbreviation is given, it is a redeclaration of a previously opened table (the current record is not lost).
  + The [Where](4gl_where.html) clause is used to filter the data returned by the read made after the `File` declaration. Additional filters can be added on the table by a [Filter](4gl_filter.html) instruction, and finally a [Where](4gl_where.html) clause can also be added on the [For](4gl_for.html) syntax. These conditions are combined by the 'and' operator. For more information about the operators available, see the [Where](4gl_where.html) documentation.
  + The [Order By](4gl_order-by.html) clause is used to define (or redefine) the order in which the records are returned by default. For more information on this clause, see the [Order By](4gl_order-by.html) documentation.
* **The result of a system command.** Every line is split into words separated by spaces or tabs and every word is assigned to the fields on the list. Two consecutive spaces are considered as a unique one. When the list is full, the remaining characters of the lines are ignored and the next line is considered. If the end of the line is encountered before all the fields on the list have been considered, the remaining fields are returned empty. The end of line character can be either LF (line feed) or CR+LF (carriage return+line feed). The fields declared on the list are therefore all character strings with a maximum length of 255. This type of table has some usage restrictions:

  + It is accessible in read only.
  + Only sequential read operations (using [Curr](4gl_curr.html), [First](4gl_first.html), [Next](4gl_next.html), [Prev](4gl_prev.html), and [Last](4gl_last.html) keywords), and [For](4gl_for.html) loops are possible.
  + The [Where](4gl_where.html) clause is defined the same way as other files.
  + The [Order by](4gl_order-by.html) clause is not supported. There is no key on such a table and it is impossible to specify one. The ascending scan command corresponds to the way in which the screen display is shown.
  + After a read (by [Read](4gl_read.html) or [For](4gl_for.html)), the [fstat](4gl_fstat.html) variable is updated as usual.
* **The content of arrays stored in memory.** This is possible only in read mode.

**The result of the execution of this instruction is the following:**  
 \* It creates variable classes [F] and [G] and updates the variables [S][fileabre](4gl_fileabre.html) and [S][filename](4gl_filename.html).  
 \* It updates the list of tables opened. The table that is first in the command becomes the default table. This can be changed by the [Default](4gl_default.html) File instruction.  
 \* The maximum number of tables that can be opened simultaneously is limited by the system variable `[S]adxmto`. The value of this variable is normally defaulted by the supervisor (assigned in APL.ini configuration file). A common value for [adxmto](4gl_adxmto.html) is 200.

A `File` command closes all the tables opened by an earlier `File` (or [Trbegin](4gl_trbegin.html)) instruction. The use of this syntax is therefore deprecated in the application code. You must use `Local File` to open the tables in a routine to avoid conflicts on the calling context.

The `Local File` instruction is used to open files locally for a routine or subprogram and temporarily. This declaration does not close files previously opened by a File or Local File command, but adds to the list of open tables. The first table opened this way becomes the new default table. After the [Close](4gl_close.html) Local File command (or the end of the subprogram), the list of tables is as it was before the instruction, as are the current records.

A locality level is attached to each Local file. Therefore, using Local File and the same abbreviation, you can reopen a file already opened elsewhere, but this cannot be done in the same level of the nesting call.

# Comments

You can open a file with `Local File` within a transaction, but files opened in write mode by [Trbegin](4gl_trbegin.html) will no longer be accessible â even if they are not physically closed before the end of the transaction.

In version 6, opening a table is costly if the table has not been opened, or if a [Close](4gl_close.html) instruction closed the table previously. This is the reason that in version 6 programming style, tests are performed by using [clalev](4gl_clalev.html) to open a table only if it is not previously opened. The main issue with this programming technique is that it creates conflicts (for example, filters can be inherited from a previous declaration). Therefore, a new instruction called [LogicClose](4gl_logicclose.html) file has been implemented in version 7. It performs as a [Close](4gl_close.html) instruction, but does not release all the resources and is therefore cost effective when the table is reopened. As these instructions are managed by the supervisor layers, the best practice for version 7 is to declare systematically with the [Local](4gl_local.html) `File` all the tables used in a routine called by [Call](4gl_call.html), [Func](4gl_func.html), or [fmet](4gl_fmet.html) instructions.

Temporary files created for a File command (sort file or System file) are stored in the '/tmp' folder, unless the environment variable TMPDIR contains the name of another folder. Their names are randomly generated. They are only accessible from the current procedure and are physically deleted at the end of their use or at the end of the procedure.

A Close Local File or LogicClose Local File can be done within a transaction, but it will be taken into account only at the end of the transaction (instructions [Commit](4gl_commit.html) or [Rollback](4gl_rollback.html)).

The [nbrecord](4gl_nbrecord.html) function is available to perform a `count(*)` on a table. It assumes that the table has been previously declared by `File`, and uses the abbreviation of the table as an argument. This count does not consider the filter that can be added by any [Where](4gl_where.html) clause. The instruction [rowcount](4gl_rowcount.html) performs the count on the filtered lines.

A table can be opened several times with different locality levels, using a new [Where](../4gl/where.md) clause each time. It is not added to the previous ones, but it is attached to a locality level and thus deleted at the end of the subprogram. For example, consider the following script:

```
  Local File CUSTOMER [CUST] Where COUNTRY="USA"
  Call MY_ROUTINE
  Read [CUST]CODE First : # This will return the first customer having COUNTRY equal to the USA
  Call MY_OTHER_ROUTINE
  ...
End

Subprog MY_ROUTINE
  Read [CUST]CODE First : # Table has not been declared, previous condition applies: the first US customer code is read
  Local File CUSTOMER Where COUNTRY<>"USA" : # The opposite condition
  Read [CUST]CODE First : # Previous condition applies, now the first non US customer code is read
  Filter [CUST] Where CITY<>"PARIS"
  Read [CUST]CODE First : # Filter added to previous condition: first non US customer with a city not equal to PARIS is read
End

Subprog MY_OTHER_ROUTINE
  Local File [CUST] Where COUNTRY<>"USA" : # The abbreviation refers to the previous file instruction, the condition is added
  Read [CUST]CODE First : # No record will be returned, because the condition is COUNTRY="USA" and CONTRY<>"USA"
End
```

# Associated errors

| Code | Description |
| --- | --- |
| 7 | Abbreviation not found. |
| 10 | The expression that contains the table name does not return a character string. |
| 20 | Table not found. |
| 27 | Table access error. |
| 28 | Table opened twice. |
| 29 | Too many tables opened. |

# See also

[Trbegin](4gl_trbegin.html), [Where](4gl_where.html), [Order By](4gl_order-by.html), [adxmto](4gl_adxmto.html), [clalev](4gl_clalev.html), [Default](4gl_default.html), [Close](4gl_close.html), [Local](4gl_local.html), [LogicClose](4gl_logicclose.html), [nbrecord](4gl_nbrecord.html), [Filter](4gl_filter.html), [For](4gl_for.html), [Link](4gl_link.html), [filename](4gl_filename.html), [fileabre](4gl_fileabre.html).

  

[Index](index.html)  [Home](getting-started_home.html)