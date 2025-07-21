[Index](index.html)  [Home](getting-started_home.html)

Delfile

This function deletes a file.

It returns a status 0 on success or a negative code.

Notes:

* On UNIX this function performs an *unlink* so the file may still exist if referenced by several hard links.
* This function superseeds `System "del"-PATH` on Windows and `System "rm"-PATH` on Unix. It is faster because it does not fork a process.

# Syntax

```
RETURN_VALUE=delFile(PATH)
```

# Example

```
# Procedure that deletes a log file
Subprog DELETE_LOG_FILE(LOGFILE_NAME, ERR_CODE)
 Const Char LOGFILE_NAME()
 Variable Integer ERR_CODE

  # Delete the file
  # The file is supposed to be located in TMP directory on the application server with a tra extension
  ERR_CODE=delFile(filpath('TMP',LOGFILE_NAME,'tra'))
  End ERR_CODE
```

# Return values

| Value | Explanation |
| --- | --- |
| 0 | Operation succeeded. |
| -20 | File does not exist. |
| -27 | Access denied. |

# See also

[RenameFile](4gl_renamefile.html)

  

[Index](index.html)  [Home](getting-started_home.html)