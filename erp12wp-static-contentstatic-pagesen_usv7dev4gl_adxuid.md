[Index](index.html)  [Home](getting-started_home.html)

Adxuid

`adxuid` returns a unique identifier for a connection.

# Syntax

```
   adxuid(NUM_EXPR)
```

* `NUM_EXPR` is a numeric expression that can have either a 1 or 2 value.

# Examples

```
   # Creation of a unique temporary file for the user
    [L]THE_FILE = filpath("tmp",num$(adxuid(2)),0)
    Openo [L]THE_FILE
```

# Description

`adxuid` is a function that returns a unique identifier :

* For any user connected to a SAFE X3 instance (server+service) if the parameter value is 1.
* For any user connected to the current folder if the parameter value is 2.

The type of result is [Integer](4gl_integer.html).

`adxuid(2)` is used internally by the [Lock](4gl_lock.html) instruction on symbols stored in the lock table which name is given by [S][adxtlk](4gl_adxtlk.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not numeric. |
| 50 | The argument is out of the range (1-2). |

# See also

[adxtlk](4gl_adxtlk.html), [adxpid](4gl_adxpid.html).

  

[Index](index.html)  [Home](getting-started_home.html)