[Index](index.html)  [Home](getting-started_home.html)

Getenv$

`getenv$` allows you to read an environment variable as given in the service definition if Sage X3 runs on Windows, and given by assignments in the script that starts the daemon for Sage X3.

`getenv$` always gives the value on the process server.

# Syntax

```
   getenv$(EXP_ENVVAR)
```

* `EXP_ENVVAR` is a string expression that gives the environment variable name.

# Examples

```
   # What is the HOME directory ?
   Local Char HOME_DIR(200)
     HOME_DIR=getenv$("HOME")

   # What is the PATH on the process server ?
   Local Char PATH_VAR(250)
     PATH_VAR=getenv$("PATH")
```

# Description

`getenv$` allows you to get the value of environment variables in the context of the server process.

If the variable does not exist, the empty string " " is returned.

# Comments

The most frequently environment variable are : `PATH`, `TMPDIR`, `SHELL`, `LOGNAME`, and `HOME`.

In a UNIX shell, the method to declare variables is the following:

```
VARIABLE=value
export VARIABLE
```

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a string. |

# See also

[System](4gl_system.html), [dir$](4gl_dir$.html), [adxpid](4gl_adxpid.html).

  

[Index](index.html)  [Home](getting-started_home.html)