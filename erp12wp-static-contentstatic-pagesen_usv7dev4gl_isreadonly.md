[Index](index.html)  [Home](getting-started_home.html)

Isreadonly

This built-in property returns whether the properties of an instance cannot or can be modified. It can be tested but tot modified.

* If `MY_INSTANCE.isReadonly` is 1, properties cannot be modified. Any modification attempt will raise an error with error code 143.
* If `MY_INSTANCE.isReadonly` is 0, properties can be modified and accessors will be triggered. This is the default value when a class is instantiated.

# Syntax

```
MY_INSTANCE.isReadonly
```

# Example

```
# MYCUSTOMER is an instance for CUSTOMER class
# The UPDATE_CUSTOMER call would raise a 143 error if isReadonly is not 0
  If MYCUSTOMER.isReadonly=0
    Call UPDATE_CUSTOMER(MYCUSTOMER)
  Endif
```

# See also

[Instance](4gl_instance.html), [NewInstance](4gl_newinstance.html), [FreeInstance](4gl_freeinstance.html), [FreeGroup](4gl_freegroup.html), [Developer Guide Classes](developer-guide_classes.html)

  

[Index](index.html)  [Home](getting-started_home.html)