[Index](index.html)  [Home](getting-started_home.html)

This

This function gives access to the class instance pointer when executing a method on a class or a property of a class.

# Syntax

To access a property named "PROPERTY":

```
This.PROPERTY
```

To access a method of the current instance named "METHOD" with 'I','J' as arguments:

```
This.METHOD(I,J)
```

# Example

```
# Label called on the operation on a field named VAT defined in sales order line (on an update operation)
# This is the SORDERLINE instance (instance is LINE(2))
# SORDERLINE is usually a child class of SORDER (instance is MYORDER)
$CONTROL_VAT
  # Access to a property of the instance (VAT) and another instance (snapshot) having the same properties
  If This.VAT<>This.snapshot.VAT : # The VAT value is no more the VAT value when data was read for update
     # Let's be sure the class is used as a child class
     If This.APARENT<>null
        # Is the parent class really SORDER?
        If This.APARENT.Objecttype="SORDER"
          # Access to a property in the SORDER class by using APARENT instance (a default VAT rule)
          If This.VAT<>This.APARENT.DEFAULT_VAT
            # Check consistency between VAT and header VAT (function)
            ERROR=Func(This.VAT,This.APARENT.DEFAULT_VAT)
            ...
          Endif
        Endif
     Endif
   Endif
Return
```

# See also

[Instance](4gl_instance.html), [snapshot](4gl_snapshot.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [NewInstance](4gl_newinstance.html), [Sage X3 Script Glossary Snapshot](4gl_glossary-snapshot.html)

  

[Index](index.html)  [Home](getting-started_home.html)