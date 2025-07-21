[Index](index.html)  [Home](getting-started_home.html)

Adxmto

`adxmto` is an internal integer variable that indicates the maximum number of tables that can be simultaneously opened by [File](4gl_file.html).

# Syntax

```
   adxmto
```

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

This system variable is reserved for internal use only.

# See also

[fileabre](4gl_fileabre.html), [filename](4gl_filename.html), [File](4gl_file.html).

  

[Index](index.html)  [Home](getting-started_home.html)