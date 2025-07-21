[Index](index.html)  [Home](getting-started_home.html)

Renamefile

This function renames a file.

It returns a status: 0 on success; otherwise, it returns a negative code.

**Note:** This function supersedes `System "ren"-PATH-PATH1` on Windows and `System "mv"-PATH-PATH1` on Unix. It is faster because it does not fork a process.

# Syntax

```
RETURN_VALUE=RenameFile(PATH, PATH1)
```

# Example

```
# Renames a log file by changing its extension from .tra to .old
Subprog RENAME_LOG_FILE(LOGFILE_NAME, ERR_CODE)
 Const Char LOGFILE_NAME()
 Variable Integer ERR_CODE

  # Rename the file
  ERR_CODE=RenameFile(filpath('TMP',LOGFILE_NAME,'tra'),filpath('TMP',LOGFILE_NAME,'old'))
End
```

# Return values

| Value | Explanation |
| --- | --- |
| 0 | Operation succeeded |
| -20 | File does not exist |
| -27 | Access denied |

# See also

[DelFile](4gl_delfile.html)

  

[Index](index.html)  [Home](getting-started_home.html)