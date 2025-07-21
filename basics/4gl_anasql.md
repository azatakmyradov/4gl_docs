[Index](index.html)  [Home](getting-started_home.html)

Anasql

`Anasql` is used to parse a SQL sentence and return in an integer array the number and the types of values that are returned by the SQL sentence.

# Syntax

```
Anasql From DATABASE Sql SENTENCE Using TYPE_ARRAY
```

* **`DATABASE`** is a character string that can contain one of the following values:
  + "o", "O", and "3": used for an oracle database.
  + "s", "S", and "5": used for a SQL server database.
* **`SENTENCE`** is the SQL sentence must be parsed.
* **`TYPE_ARRAY`** is an array of integer values. The first index will return the number of columns returned by the SQL sentence, and the following indexes will return the data type of the Nth value returned.

The data type value is the one returned by the [type](4gl_type.html) function.

# Example

```
# Returns the number of columns of a table and their type
Subprog DESCRIBE_TABLE(TABLE_NAME,COLUMN_COUNT, COLUMN_TYPES)
Value Char TABLE_NAME()
Variable Integer COLUMN_COUNT, COLUMN_TYPES(1..)

# My current database can be known by a general parameter (1=oracle, 2=SQL server)
Local Char CURRENT_DATABASE
  CURRENT_DATABASE=num$(1+2*Fmet GACTX.APARAM.AGETVALNUM([V]CST_ALEVFOLD,"","TYPDBA"))

Local Integer RETURN_VALUES(0..dim(COLUMN_TYPES)), I

# What are the different columns type present in the table given as parameter?
  Anasql From CURRENT_DATABASE Sql "select * From "+TABLE_NAME Using RETURN_VALUES

# Set the return values
  For I=1 To RETURN_VALUES(0)
    COLUMN_TYPES(I)=RETURN_VALUES(I)
  Next I
  COLUMN_COUNT=RETURN_VALUES(0)

End
```

# See also

[Sql](4gl_sql.html), [ExecSql](4gl_execsql.html), [type](4gl_type.html).

  

[Index](index.html)  [Home](getting-started_home.html)