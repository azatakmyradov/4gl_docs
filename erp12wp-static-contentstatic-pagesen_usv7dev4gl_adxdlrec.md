[Index](index.html)  [Home](getting-started_home.html)

Adxdlrec

This function returns the number of records processed by the last [Delete](4gl_delete.html) instruction. It must be called after the [Delete](4gl_delete.html) instruction.

# Syntax

```
adxdlrec
```

# Example

```
# This function deletes all the lines for a sales order, and returns the number of lines deleted
Funprog ORDER_DROP_LINES(ORDER_NUM)
Value Char ORDER_NUM()

# Declare the ORDERLINE table
  If clalev([ORDL]) : LogicClose ORDERLINE : Endif : Local File ORDERLINE [ORDL]

# Let's delete the lines
  Delete [ORDL] Where ORDERNUM=ORDER_NUM
End adxdlrec
```

# See also

[Delete](4gl_delete.html), [adxuprec](4gl_adxuprec.html), [adxsqlrec](4gl_adxsqlrec.html).

  

[Index](index.html)  [Home](getting-started_home.html)