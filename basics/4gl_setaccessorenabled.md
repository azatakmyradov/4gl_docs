[Index](index.html)  [Home](getting-started_home.html)

Setaccessorenabled

This built-in property defines whether the set accessors are enabled on an instance.

By default, this property is 0 (false), immediately after a call to `NewInstance`. You must set it to 1 (true) to activate the set accessors.

This property is reserved for supervisor generated codes.

# Syntax

```
MY_INSTANCE.setaccessorEnabled
```

# Example

```
# Instantiate a customer
Local Instance MYCUSTOMER Using C_CUSTOMER
MYCUSTOMER=Newinstance C_CUSTOMER AllocGroup Null

# Read the customer: no controls are done because the set accessors (control, propagate) are not enabled yet
RETCODE=Fmet MYCUSTOMER.AREAD("JOHNDOE")

# Enable set accessors
MYCUSTOMER.setAccessorEnabled=1

# This assignment will trigger the control and propagate methods if they exist
MYCUSTOMER.PAYTERM="CHQ"
```

# See also

[getAccessorEnabled](4gl_getaccessorenabled.html)

  

[Index](index.html)  [Home](getting-started_home.html)