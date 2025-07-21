[Index](index.html)  [Home](getting-started_home.html)

zonsui

`zonsui` is a system variable that can be assigned during a control called during an input in a mask in order to change the order of input by reassigning the next field to be inputted.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   [S]zonsui
   zonsui
```

# Examples

```
# Let's control the current field
# If the value is not in the range [0,100], let's stay on the current field without displaying an error
$C_FIELD
If (zc>100) or (zc<0)
    zonsui = "FIELD"
Endif
End

# Control on a grid.
# If there is an error, return to the previous line on the same field.
$C_FIELD
  Gosub CTRL_CONSISTENCY
  If ERROR_FOUND
    zonsui = "FIELD(" + num$(max(nolign-2,0)) + ")"
  Endif
End

# If this code is executed during the input on a grid that has BASTAB as bottom-line variable, return to 1st line in input mode
# If this code is executed during the input on a field that does not belong to the screen, return to 1st line in command mode
zonsui = "BSTAB"

# If this code is executed during the input on a grid that has BASTAB as bottom-line variable, return to last line in input mode
# If this code is executed during the input on a field that does not belong to the screen, return to last line in command mode
Subprog APRES_BSTAB
zonsui = "BSTAB" + "(" + num$(max(0, BSTAB)) + ")"
End
```

# Description

`zonsui` is an alphanumeric variable that contains the next field to be inputted (if not empty). By default, it contains the empty string "" when the control, init or help label is reached. When the value is empty, the next field in the mask order is accessed.

# Comments

* If `zonsui` contains a field name that cannot be entered, the first following enterable field will be accessed.
* `zonsui` can set the next field in another mask or on another rank.
* If during an input check validation of a field has to be prevented, without sending a "beep" to the screen, simply assign to `zonsui` the name of the current field on which the check is made. This may be done by assignment, for non-dimensioned zones:

`zonsui` = `zoncou`

* If the field belongs to an array, you can write:
  `zonsui = zoncou+"(" + num$(index) + ")"`
* Setting `mkstat` to 2 will have the same effect.

# See also

[Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html), [zc](4gl_Zc.html), [zoncou](4gl_Zoncou.html), [zonsor](4gl_Zonsor.html).

  

[Index](index.html)  [Home](getting-started_home.html)