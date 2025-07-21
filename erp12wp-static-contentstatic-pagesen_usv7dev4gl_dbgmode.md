[Index](index.html)  [Home](getting-started_home.html)

Dbgmode

`dbgmode` is a system variable that must be different from 0 to enable the debugger to work.

# Syntax

```
   dbgmode
```

# Examples

```
   # Let's switch to debugger
    dbgmode = 1
    Dbgaff
```

# Description

The [Dbgaff](4gl_dbgaff.html) switches the Sage X3 execution engine in debugger mode. The `dbgmode` variable must not have a 0 value to allow the debugger to operate.

When this happens, the focus is given to the Eclipse debugger and the user can check the variables in the context, step on, create breakpoints, and so forth.

# Associated errors

No associated error.

# See also

[Dbgaff](4gl_dbgaff.html).

  

[Index](index.html)  [Home](getting-started_home.html)