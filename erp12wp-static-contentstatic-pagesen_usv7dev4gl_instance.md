[Index](index.html)  [Home](getting-started_home.html)

Instance

This keyword declares an [instance](4gl_glossary-structure.html) of a [class](developer-guide_classes.html) or a [representation](developer-guide_representations.html). The instance is `Null` initially. You must allocate it with [NewInstance](4gl_newinstance.html) before reading or writing its properties.

# Syntax

Syntax is similar to other declarations, except that it requires a mandatory `Using CLASS_NAME` clause, where `CLASS_NAME`is either:

* A class name starting with `C_`, defined in the class dictionary.
* A representation name starting with `R_`, defined in the representation dictionary.
* A special class name like `OBJECT`.

# Examples

Simple declarations:

```
  # Instance of a customer class
  Local Instance MY_CUSTOMER Using C_CUSTOMER

  # Let us allocate it
  MY_CUSTOMER = NewInstance C_CUSTOMER AllocGroup Null

  # Now we can call standard methods
  Fmet MY_CUSTOMER.AREAD("CUST012345")

  # Instance of a customer representation
  Local Instance MY_CUSTOMER_UI Using R_CUSTOMER
```

A more complex example with generic instances and cast operator:

```
  # Declare generic instance (will be specialized later by a cast)
  Local Instance OBJECT_INSTANCE Using OBJECT

  # Allocate an ORDERLINE instance
  # As OBJECT_INSTANCE is a generic instance, you cannot invoke methods on it
  OBJECT_INSTANCE = NewInstance C_ORDERLINE AllocGroup Null

  # Declare an array of 15 ORDERLINE instances
  Local Instance SORDER_LINES(1..15) Using C_ORDERLINE

  # Assign the previously allocated instance pointer to the first array entry. Cast is necessary here.
  SORDER_LINES(1) = cast(OBJECT_INSTANCE,"C_ORDERLINE")

  # Get the type of the first array entry
  TYPE=SORDER_LINES(1).Objecttype
  # TYPE is "C_ORDERLINE"

  # As SORDER_LINES(2) was not assigned, the following test will be false and Objecttype will not be called
  If SORDER_LINES(2)<>null
    TYPE=SORDER_LINES(2).Objecttype
  Endif
```

# Comments

You must provide a class or representation name when declaring an instance variable.   
The special `OBJECT` class name allows you to declare a variable which may be assigned to an instance of any class later.   
You will not be able to access properties or invoke methods on an `OBJECT` variable, besides built-in properties like `objectType`, unless you cast it first to a known class with the [Cast](4gl_cast.html) function.

The [objecttype](4gl_objecttype.html) method returns the name of the instantiation class or representation as `C_CLASSNAME` or `R_REPNAME`.

# Implicit data type conversion

There are no implicit type conversions by default for an Instance. However, implicit type or property conversion may be explicitly specified in the script.

```
  
...  
this.PROPERTY = MY_INSTANCE.OTHER_PROPERTY  
...  

```

In this case, the CONTROL and PROPAGATE actions will be called for this.PROPERTY.

# See also

[Structure](4gl_glossary-structure.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [NewInstance](4gl_newinstance.html), [SetInstance](4gl_setinstance.html), [allocgrp](4gl_allocgrp.html), [cast](4gl_cast.html), [null](4gl_null.html), [Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Date](4gl_date.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html)

  

[Index](index.html)  [Home](getting-started_home.html)