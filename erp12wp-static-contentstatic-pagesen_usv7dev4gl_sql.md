[Index](index.html)  [Home](getting-started_home.html)

Sql

`Sql` allows you to execute a `Select` statement in the database.

# Syntax

```
   For (VARIA_LIST) From DATAB_TYPE Sql SQL_STATEMENT As  [CLASS]
   Next
```

* `VARIA_LIST` is a list of `VARIA` separated by commas.
* `VARIA` can contain one of the following syntaxes:
  + `DECLARATION` `VARNAME`
  + `DECLARATION` `VARNAME` ( `INDEX_SEP` )
* `DECLARATION` is a declaration keyword that can be [Char](4gl_char.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Date](4gl_date.html), [TinyInt](4gl_tinyint.html), [Decimal](4gl_decimal.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Datetime](4gl_datetime.html), or [Uuident](4gl_uuident.html). If `DECLARATION` is [Char](4gl_char.html), `VARNAME` must be followed by `(N)` where `N` is the maximum size of the string, before a possible list of (`INDEX_SEP`).
* `VARNAME` is a variable name starting with a letter, and followed by letters, digits, or underscores.
* `INDEX_SEP` is a list of `DIMENSION` or `DIMENSION_RANGE` separated by commas. If 'N' commas are given, it describes an array of dimension 'N+1'. The number of commas is therefore limited to 3.
* `DIMENSION_RANGE` has the following syntax: `DIMENSION``..``DIMENSION`.
* `DIMENSION` is an expression returning a numeric dimension.
* `DATAB_TYPE` is a string expression that returns a code defining the database used.
* `SQL_STATEMENT` is a string expression that returns the SQL Select statement executed by the `Sql`instruction. It can be an array of string variables, with or without a range of indexes. If no range is given, all the different indexes of the array are concatenated to give the SQL statement. Otherwise, only the elements within the range are used.

# Examples

```
  # Example 1: Request to select a maximum value in a table
  Local Char REQUEST(255)
  REQUEST="select max(ACCNUM_0) From GACCENTRYD"
  For (Integer NUM) From "3" Sql REQUETE As [XXX]
    MAX_VAL=[F:XXX]NUM
  Next


  # Example 2: Request to select the different fields of a table in data dictionary
  Local Char REQUEST(255)
  Local Char MYTABLE(20)
  ...
  REQUEST="select CODZONE_0, DIME_0 From ATABZON Where CODFIC='"+MYTABLE+"'"
  For (Char FIELD(12),Integer DIMENSION) From "3" Sql REQUETE As [ABB]
    # Here, we have for every loop FIELD that is equal to the column name and DIMENSION to its dimension
  Next


  # Example 3: Request with an array
  Local Char REQUEST(255)(1..5)
  REQUEST(1)="select BPCNAM_0"
  REQUEST(2)=" From BPARTNER"
  REQUEST(3)=" Where BPCFLG_0=1"

  # First request without where
  For (Char NAMES(20))From "S" Sql REQUEST(1..2) As [BPC]
    # All the lines will be seen
  Next

  # Second request with the where 
  For (Char NAMES(20))From "S" Sql REQUEST(1..3) As [BPC]
    # Only the lines with BPCFLG_0 equal to 1 will be seen
  Next


# Example 3: Use the default database
  Local Integer DBTYPE
  Local DATABASE_TYPE(10)
  DBTYPE = fmet GACTX.APARAM.AGETVALNUM([V]CST_ALEVFOLD,"","TYPDBA")
  DATABASE_TYPE=string$(DBTYPE=1,"O")+string$(DBTYPE=2,"S")

  For (Integer INDEX,Char NAMES(20)(1..2)) From DATABASE_TYPE SQL "Select INDEX_0, NAME_0, NAME_1 From MYTABLE" As [MYT]
    # On every loop instance, we have the following values available:
      # [MYT]INDEX, [MYT]NAMES(1), [MYT]NAMES(2) 
  Next
```

# Description

`Sql` allows you to execute a `Select` statement on the database. The list of parameters in this syntax will be filled by the data returned in every loop for one of the lines of the cursor.

The database type is given by the following values:  
\* "o","O","3" indicates Oracle.  
- "s","S","5" indicates SQL server.

The SQL expression can be given with a string array. When this happens, all the lines of the array (limited to a range if a range is given) are concatenated to give the SQL request to be executed.

The class abbreviation is used to access the variables in the list.

# Associated errors

| Error code | Description |
| --- | --- |
| 19 | Database incorrect: the database type is not Oracle or SQL server. |
| 69 | Incorrect arguments: the argument list has less or more than the number of columns returned by the select statement, or the data type does not fit with the columns returned. |
| 75 | Database error: a column mentioned in the SQL statement does not exist. |

# See also

[Anasql](4gl_anasql.html), [Execsql](4gl_execsql.html).

  

[Index](index.html)  [Home](getting-started_home.html)