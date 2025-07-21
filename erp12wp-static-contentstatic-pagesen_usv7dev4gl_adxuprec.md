[Index](index.html)  [Home](getting-started_home.html)

Adxuprec

This function returns the number of records processed by the last [Update](4gl_update.html) instruction, and it must be called after the instruction.

# Syntax

```
adxuprec
```

# Example

```
# This function sets all the shipped lines of a sales order to closed, and returns the number of lines updated
Funprog ORDER_CLOSE_LINES(ORDER_NUM)
Value Char ORDER_NUM()

# Declare the ORDERLINE table
  If clalev([ORDL]) : LogicClose ORDERLINE : Endif : Local File ORDERLINE [ORDL]

# Let's update the lines
  Update [ORDL] Where ORDERNUM=ORDER_NUM and CLOSED=1 and QTYSHIPPED=QTYORDERED with CLOSED=2
End adxuprec
```

# See also

[Update](4gl_update.html), [adxdlrec](4gl_adxdlrec.html), [adxsqlrec](4gl_adxsqlrec.html).

  

[Index](index.html)  [Home](getting-started_home.html)