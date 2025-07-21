[Index](index.html)  [Home](getting-started_home.html)

nolign1

`nolign1` is a system variable used on grid input in masks. It gives the range end on operation involving a range of lines (`nolign` is the starting point of the range).

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   [S]nolign1
   nolign1
```

# Examples

```
# Lets's perform a test on a range deletion operation (status=68 or 83)
# The delivered quantity (variable DLVQTY) must be 0 otherwise the line cannot be deleted
  If status=68 or status=83
    mkstat=0
    For I=nolign-1 to nolign1-1
      If [M]DLVQTY(I)<>0
        GMESSAGE="Line #"+num$(I+1)-"cannot be deleted. Operation aborted"
        mkstat=1
        Break
      Endif
    Next I
    If mkstat=0
      Gosub DELETE_LINES
    Endif
  Endif
```

# Description

For some operation needing an interval of lines, `nolign` is the first value of the line range, and `nolign1` is the end value. Both values are inputted by the user when he triggers the corresponding operation.

# See also

[nolign](4gl_Nolign.html), [Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html).

  

[Index](index.html)  [Home](getting-started_home.html)