[Index](index.html)  [Home](getting-started_home.html)

Execsql

This instruction executes a SQL statement against the Sage X3 database.

Use this instruction with care as SQL statements may differ in syntax across databases.

# Syntax

```
Execsql From DATABASE_TYPE Sql SQL_COMMAND
```

`DATABASE\_TYPE` is a one-character string with the following values:

* "o", "O", "3": Oracle
* "s", "S", "5": SQL Server

# Example

```
  Execsql From "O"  Sql "create table MYTABLE (t integer)"
  Execsql From "O"  Sql "insert into MYTABLE values (1)"
  Execsql From "O"  Sql "drop table MYTABLE"
```

# See also

[adxsqlrec](4gl_adxsqlrec.html)

  

[Index](index.html)  [Home](getting-started_home.html)