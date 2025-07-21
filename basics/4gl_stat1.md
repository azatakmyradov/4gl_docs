[Index](index.html)  [Home](getting-started_home.html)

Stat1

`stat1` is a system variable that contains the number of lines returned by a [System](4gl_system.html) instruction.

# Syntax

```
  [S]stat1
  stat1
```

# Examples

```

  # On an Unix system, let's list a returned as parameter
  Subprog DIRECTORY_LIST(DIRECTORY,RESULT,NBLINES,PARTIAL)
  Value Char DIRECTORY()
  Variable Char RESULT()(1..)
  Variable Integer NBLINES
  Variable Tinyint PARTIAL: # Set to 1 if only a partial result is returned
  Local Integer I

  System RESULT="ls -l"-DIRECTORY
  NBLINES=stat1
  PARTIAL=(NBLINES>dim(RESULT))
  End
```

# Description and comments

When performing a [System](4gl_system.html) order on one of the servers available, the standard output can be captured by using the syntax `System VARIABLE_ARRAY=SYSTEM_ORDER`. The number of lines returned by the system order is returned in `stat1`.

This value can exceed the dimension of the array that returns the result. Only the first returned lines are stored in the array, and the value of `stat1` is greater than the dimension of the array.

# Associated errors

No error is returned, but if the System order fails, a negative value can be returned in `stat1` (for example, the error status returned by the shell that executed the system instruction on Unix).

# See also

[System](4gl_system.html).

  

[Index](index.html)  [Home](getting-started_home.html)