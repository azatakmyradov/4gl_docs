[Index](index.html)  [Home](getting-started_home.html)

Fmet

This operator invokes a method on an instance (similar to [func](4gl_func.html)). It is used to invoke methods that do return values. For methods that do not return values, use the [CallMet](4gl_callmet.html) instruction.

# Syntax

```
fmet INST.METHOD_NAME
fmet INST.METHOD_NAME(parameter_list)
```

# Example

```
# MYSORDER is a sales order instance, with a CUST_CODE property
# C_CUSTOMER is a persistent class
# Declare and instantiate a C_CUSTOMER instance
Local Instance MYCUSTOMER Using C_CUSTOMER
MYCUSTOMER=NewInst [CUST] With C_CUSTOMER

# Load the customer record with the standard AREAD method
ERR= fmet MYCUSTOMER.AREAD(MYSORDER.CUSTOMER)
If Not ERR
  # The customer exists...
Endif
```

# See also

[Callmet](4gl_callmet.html), [Fmethod](4gl_fmethod.html), [Method](4gl_method.html).

  

[Index](index.html)  [Home](getting-started_home.html)