[Index](index.html)  [Home](getting-started_home.html)

Adxpid

`adxpid` returns the process **ID** that executes the Sage X3 code on the Sage X3 server.

# Syntax

```
   adxpid
```

# Examples

```
   # Creation of a unique temporary file for the user
    [L]THE_FILE = filpath("tmp",num$(adxuid(2)),0)
    Openo [L]THE_FILE
```

# Description

`adxpid` returns the **ID** of the Sage X3 current process. Unlike [adxuid](4gl_adxuid.html), this process ID cannot be unique if several servers are involved.

The type of result is [Integer](4gl_integer.html).

# See also

[adxuid](4gl_adxuid.html).

  

[Index](index.html)  [Home](getting-started_home.html)