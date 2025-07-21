[Index](index.html)  [Home](getting-started_home.html)

Sleep

`Sleep` allows you to pause the execution of a script for a given number of seconds.

# Syntax

```
   Sleep EXP_NUM
```

* `EXP_NUM` is a numeric expression returning a number of seconds (positive).

# Examples

```
   # Let's try to lock a symbol
   # If the symbol is already locked, wait for 1 second before trying again
    NB_ATTEMPTS=0
    Repeat
       NB_ATTEMPTS+=1
       Lock DOSSIER
       If fstat <> 0
           Sleep 1
       Endif
    Until fstat = 0 or NB_ATTEMPTS>10
```

# Description

The `Sleep` statement allows you to pause the execution of a script. The execution is suspended for the given number of seconds and then resumes after the `Sleep`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a numeric value. |

  

[Index](index.html)  [Home](getting-started_home.html)