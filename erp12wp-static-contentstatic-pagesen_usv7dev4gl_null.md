[Index](index.html)  [Home](getting-started_home.html)

Null

This keyword represents the ***null*** instance.

An instance variable which has been declared but not assigned yet is `null`.

# Syntax

```
null
```

# Example

```
# Creates child instances (lines) in a sales order from arrays of products and quantities
# If product code is empty or quantity is zero no line is created
Funprog CREATE_LINES(MY_ORDER, PRODUCTS, QUANTITIES)
Variable Instance MY_ORDER with C_SALESORDER
Variable Char PRODUCTS()(1..)
Variable Decimal QUANTITIES(1..)
Local Integer I, LINE_COUNT
  For I=1 to dim(PRODUCTS)
    If PRODUCTS(I)<>"" and QUANTITIES(I)<>0
      SALESORDER.LINES(I)=NewInstance C_SORDERLINE AllocGroup SALESORDER
      SALESORDER.LINES(I).PRODUCT=PRODUCTS(I)
      SALESORDER.LINES(I).QUANTITY=QUANTITIES(I)
    Endif
  Next I

  LINE_COUNT=0
  For I=1 to dim(PRODUCT)
    # Increment LINE_COUNT only if SALESORDER.LINES(I) has been allocated
    LINE_COUNT+=(SALESORDER.LINES(I)<>null)
  Next I

End LINE_COUNT
```

# See also

[Structure](4gl_glossary-structure.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [Instance](4gl_instance.html), [NewInstance](4gl_newinstance.html), [SetInstance](4gl_setinstance.html), [allocgrp](4gl_allocgrp.html), [cast](4gl_cast.html).

  

[Index](index.html)  [Home](getting-started_home.html)