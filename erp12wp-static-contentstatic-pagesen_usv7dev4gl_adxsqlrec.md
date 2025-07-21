[Index](index.html)  [Home](getting-started_home.html)

Adxsqlrec

This function returns the number of records processed by the last [ExecSql](4gl_execsql.html) instruction. It must be called after an [ExecSql](4gl_execsql.html) instruction that inserts, updates, or deletes records. This function returns 0 after [ExecSql](4gl_execsql.html) instructions that execute DDL statements like `CREATE TABLE` or `DROP TABLE`.

# Syntax

```
adxsqlrec
```

# Example

```
Funprog SQL_EXECUTION
Local Char DATABASE_TYPE(1)
Local Integer I
Local Char ERROR_MESSAGE(100)

# Set the database type
  DATABASE_TYPE="3" : # "3" is Oracle, "5" is Sql server

# Handle errors
  Onerrgo SQL_ERROR

# No need to test adxsqlrec after executing CREATE TABLE. It will always be 0. 
# If CREATE TABLE fails, an error is raised and execution resumes at SQL_ERROR.
  MESSAGE="creating MYTABLE"
  Execsql From DATABASE_TYPE  Sql "Create table MYTABLE( t integer )"

# Let us insert records: adxsqlrec should be 1 after every inserted record
  For I=1 to 10
     Execsql From DATABASE_TYPE  Sql "Insert into MYTABLE values ("+num$(I)+")"
     If adxsqlrec=0
        End "No record inserted with "+num$(I)+" value"
     Endif
  Next I

# Now delete records having value 5 and above (5,6,7,8,9,10 ==> 6 records)
  Execsql From DATABASE_TYPE  Sql "delete from MYTABLE where t >= 5"
  If adxsqlrec<>6
     End num$(adxsqlrec)-"records deleted, expected 6"
  Endif

# adxsqlrec will be 0 after executing DROP TABLE
  MESSAGE="dropping MYTABLE"
  Execsql From DATABASE_TYPE  Sql "drop table MYTABLE"

# End of job
  End "Job completed successfully"
End

# If an error occurred
$SQL_ERROR
  Errbox "error"
  End "An error occurred while"-MESSAGE
End
```

# See also

[Execsql](4gl_execsql.html) [adxuprec](4gl_adxuprec.html) [adxdlrec](4gl_adxdlrec.html)

  

[Index](index.html)  [Home](getting-started_home.html)