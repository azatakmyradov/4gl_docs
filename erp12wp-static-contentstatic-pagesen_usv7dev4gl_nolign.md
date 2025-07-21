[Index](index.html)  [Home](getting-started_home.html)

nolign

`nolign` is a system variable used on grid input in masks. It gives the current line value (starting at 1).  
It is also used in class assignment to identify the current line when a grid in a mask class is assigned from or to a table class.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   [S]nolign
   nolign
```

# Examples

```
# [M:ORD] is an order mask that contains an array of lines
# [M:ORD]NBLIG is the array associated variable that contains the number of lines
# [F:ORD] is the table that contains the sales order header
# [F:LIN] is the table that contains the sales order lines
# ORDNUM is the key property for [F:ORD] (ORD0 is the key name)
# ORDNUM+NUMLIN is the key property for [F:LIN] (LIN0 is the key name)
# We suppose that the tables and the mask have been declared before
# [L]ORDNUM is the key value to be read

# Read the order and transfer it to the mask
# fstat can be checked and will be 0 if everything is ok
$READ_ORDER
  Read [ORD]ORD0=ORDNUM
  If fstat=0
    [M:ORD]=[F:ORD]
    nolign=1
    Repeat
      Read [LIN]ORD1=[F:ORD]ORDNUM;nolign
      If fstat=0
        [M:ORD]=[F:LIN]
      Endif
      nolign+=1
    Until fstat<>0
    fstat=0
  Endif
Return

# Creates the order after transfer from the mask
# fstat can be checked and will be 0 if everything is ok
# The transaction is not managed here (Trbegin/Commit/Rollback are done in the script calling this subprogram)
$CREATE_ORDER
  [F:ORD]=[M:ORD]
  Write [ORD]
  If fstat=0
    For nolign=1 to [M:ORD]NBLIG
      [F:LIN]=[M:ORD]
      Write [LIN]
      Break (fstat<>0)
    Next nolign
  Endif
Return

# Other example: control on a field (QTY) in the order grid
# The quantity cannot be 0 on the first line of the grid
Subprog C_QTY(VALEUR)
  If VALEUR=0 and nolign=1
    GMESSAGE = "Quantity cannot be 0 on the first line"
    mkstat=1
  Endif
End
```

# Description

`nolign` is a system variable that defines the current line in operations involving arrays in screen masks. For instance, when a label (control, default values, buttons...) is called from a variable present in an array, `nolign` defines the current index on which the routine is called.

For some operation needing an interval of lines, `nolign` is the first value of the line range, and `nolign1` is the end value.

It is also used to define the current line in class assignments: whan a variable is an array on one side and a single value on the other side, `nolign` defines the current index for the assignment. `nolign` starts at 1 when the index starts at 0.  
This means that if you want to access to an array element `ELT` as a variable on line `nolign`, you have to use `[M]ELT(nolign-1)`.

# See also

[nolign1](4gl_Nolign1.html), [Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html).

  

[Index](index.html)  [Home](getting-started_home.html)