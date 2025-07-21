[Index](index.html)  [Home](getting-started_home.html)

Dir$

`dir$` returns the path of the directory where the Sage X3 runtime engine is installed.

# Syntax

```
  dir$
```

# Example

```
  Local Char INSTALLDIR(200)
  INSTALLDIR=dir$
```

`dir$` is the directory, located on the process server, where the Sage X3 engine runtime is installed.
The result type is [Char](../4gl/char.md).

# Associated errors

| Error code | Description |
| --- | --- |
| 29 | The function cannot be executed (no open channels available). |

# See also

[filpath](4gl_filpath.html), [adxdir](4gl_adxdir.html), [System](4gl_system.html).

  

[Index](index.html)  [Home](getting-started_home.html)