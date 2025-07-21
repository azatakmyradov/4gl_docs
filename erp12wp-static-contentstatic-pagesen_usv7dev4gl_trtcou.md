[Index](index.html)  [Home](getting-started_home.html)

Trtcou

`trtcou` returns the name of the current script.

# Syntax

```
   trtcou
```

# Examples

```
   # Let's find the current script
   CURRENT_SCRIPT=trtcou

   # Another function can also be used
   CURRENT_SCRIPT=adxpno(0)
```

# Description

The `trtcou` function returns the name of the current script in the following format:

`[email protected]/SCRIPT$adx`

With the following values:

* `server` is the server name, and it is empty if the server is the same as the execution server.
* `FOLDER` is the folder name where the script has been found.
* `TRT` is the subfolder where the script is found (usually TRT).
* `SCRIPT` is the script name.
* `$adx` is a constant that corresponds to the extension of the executable (compiled) script.

The type of the result is [Char](4gl_char.html).

# Associated errors

No associated error.

# See also

[adxpno](4gl_adxpno.html), [nomap](4gl_nomap.html), [adxmother](4gl_adxmother.html).

  

[Index](index.html)  [Home](getting-started_home.html)