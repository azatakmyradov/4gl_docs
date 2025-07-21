[Index](index.html)  [Home](getting-started_home.html)

Callmet

This instruction invokes a method on an instance (similar to [Call](4gl_call.html)). It is used to invoke methods that do not return any value. For methods that return a value, use the [fmeth](4gl_fmet.html) operator.

# Syntax

```
Callmet INST.METHOD_NAME
Callmet INST.METHOD_NAME(parameter_list)
```

# Example

```
# Example of SETERROR method call in a control event
  If this.AMOUNT=0
    Callmet this.SETERROR("AMOUNT","Amount cannot be zero",20,ASTATUS)
  Elsif this.AMOUNT<0
    Callmet this.SETERROR("AMOUNT","Amount must be positive",21,ASTATUS)
  Endif
```

# See also

[Fmet](4gl_fmet.html), [Fmethod](4gl_fmethod.html), [Method](4gl_method.html)

  

[Index](index.html)  [Home](getting-started_home.html)