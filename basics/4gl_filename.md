[Index](index.html)  [Home](getting-started_home.html)

Filename

`filename` is an internal character string array that gives the list of the table that have been opened by [File](4gl_file.html).

# Syntax

```
   filename(INDEX_VALUE)
```

* `INDEX_VALUE` is an expression returning an index in the (1,[adxmto](4gl_adxmto.html)) range.

# Example

```
Subprog TABLE_LIST(TABLES,ABBREV)
Variable Char TABLES()(1..),ABBREV()(1..)
Local Integer I

    For I = 1 To [S]adxmto
       TABLES(I)=filename(I)
       ABBREV(I)=fileabre(I)
    Next I
End
```

# Comment

This system variable is reserved for internal use. If the table is referred by `filename`, it does not mean that the table is still accessible.

# See also

[adxmto](4gl_adxmto.html), [fileabre](4gl_fileabre.html), [File](4gl_file.html).

  

[Index](index.html)  [Home](getting-started_home.html)