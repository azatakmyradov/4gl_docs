[Index](index.html)  [Home](getting-started_home.html)

Adxpno

`adxpno` gives access to the stacked scripts called with [Call](4gl_call.html), [Fmet](4gl_fmet.html), or [func](4gl_func.html).

# Syntax

```
   adxpno(EXP_INTEGER)
```

* `EXP_INTEGER` is an integer expression that returns the level of call.

# Examples

```
   # Let's find the current script
   CURRENT_SCRIPT=adxpno(0)

   # Another function can also be used
   CURRENT_SCRIPT=trtcou

   # Let's find the number of call stacked
    Integer LEVEL
    While adxpno(LEVEL) <> ""
           LEVEL += 1
    Wend
```

# Description

The `adxpno(EXP_INTEGER)` function returns the name of the current script called at a given level in the following format:

`[email protected]/SCRIPT$adx`

With the following values:

* `server` is the server name (empty if the server is the same as the execution server).
* `FOLDER` is the folder name where the script is found.
* `TRT` is the subfolder where the script is found (usually TRT).
* `SCRIPT` is the script name.
* `$adx` is a constant that corresponds to the extension of the executable (compiled) script.

The type of result is [Char](4gl_char.html).

`EXP_INTEGER`=0 corresponds to the current level, `EXP_INTEGER`= 1 corresponds to the calling level, and so forth. When `EXP_INTEGER` becomes greater than the number of stacked scripts, `adxpno(EXP_LEVEL)` returns the empty string `""`.

# Associated errors

No associated error.

# See also

[trtcou](4gl_trtcou.html), [nomap](4gl_nomap.html), [adxmother](4gl_adxmother.html).

  

[Index](index.html)  [Home](getting-started_home.html)