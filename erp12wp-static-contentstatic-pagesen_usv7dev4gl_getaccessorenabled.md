[Index](index.html)  [Home](getting-started_home.html)

Getaccessorenabled

This built-in property defines whether the [get accessors](getting-started_glossary-a-e.html#accessors) are enabled on an instance or not.

By default, this property is 0 (false), immediately after a call to `NewInstance`. You must set it to 1 (true) to activate the get accessors.

This property is reserved for supervisor generated codes.

# Syntax

```
MY_INSTANCE.getAccessorEnabled
```

# Example

```
# local variable storing customer risk (computed)
Local Decimal RISK

# Instantiate a customer
Local Instance MYCUSTOMER Using C_CUSTOMER
MYCUSTOMER=Newinstance C_CUSTOMER AllocGroup Null

# Read the customer (the RISK property is not set by this method)
RETCODE=Fmet MYCUSTOMER.AREAD("JOHNDOE")

# If the accessors are not enabled, RISK will return 0
MYCUSTOMER.getAccessorEnabled=0
RISK=MYCUSTOMER.RISK

# If the accessors are enabled, RISK will be computed and return a value that might not be null
MYCUSTOMER.getAccessorEnabled=1
RISK=MYCUSTOMER.RISK
```

# See also

[setAccessorEnabled](4gl_setaccessorenabled.html), [get accessors](getting-started_glossary-a-e.html#accessors).

  

[Index](index.html)  [Home](getting-started_home.html)