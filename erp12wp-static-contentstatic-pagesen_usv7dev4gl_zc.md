[Index](index.html)  [Home](getting-started_home.html)

zc

`zc` is a system variable used on grid input in masks. It gives access to the current value during controls, initialization, selection and help routines.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   [S]zc
   zc
```

# Examples

```
# Let's control that a date is in the future. If this is not the case, assign it to the current date
$CONTROL_STARTDATE
  If zc<date$
    zc=date$
  Endif
End

# Let's check if a modification has been done on the field FIELD1 (in the control routine)
$CONTROL_FIELD1
  If zc<>[M]FIELD1
    Gosub PROPAGATE_UPDATE : # The field has been modified
  Endif
End
```

# Description

zc gives access to the "current field" being inputted or controlled in mask operation associated code.

The current field exists in the following cases:

* a formula or routine called from a mask to control the field. `zc` is the value entered by the user and it may be reassigned by the verification routine.
* a formula or routine called from a mask as default value. If zc has been modified, its value is then copied to the variable corresponding to the mask.
* a routine called from a mask by the help key. zc also represents the variable being entered and it may similarly be reassigned
* when the calculator is called, zc corresponds to the zone being entered.

# Comments

The data type associated to `zc` depends on the field. This can be tested by `type` function.

# See also

[Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html), [zonsui](4gl_Zonsui.html), [zoncou](4gl_Zoncou.html), [zonsor](4gl_Zonsor.html).

  

[Index](index.html)  [Home](getting-started_home.html)