[Index](index.html)  [Home](getting-started_home.html)

Adxdir

This function returns the path of the directory where the Sage X3 execution engine run-time is installed on the current process server.

# Syntax

```
adxdir
```

# Examples

```
# checks if a sub-directory temp has been installed
If filinfo(adxdir+"\temp",0)<0
  End -1 : # There is an error
Endif
```

# Comments

The returned value is a character string.

# See also

[filpath](4gl_filpath.html).

  

[Index](index.html)  [Home](getting-started_home.html)