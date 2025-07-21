[Index](index.html)  [Home](getting-started_home.html)

zoncou

`zoncou` is a system variable that contains the name of the current field during a control called when an input in a mask is performed.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   [S]zoncou
   zoncou
```

# Examples

```
# Control on a grid (this label can be called on any field of the grid
# If there is an error, return to the previous line on the same field.
$CONTROL
  Gosub CTRL_CONSISTENCY
  If ERROR_FOUND
    zonsui = zoncou+"(" + num$(max(nolign-2,0)) + ")"
  Endif
End
```

# Description

`zoncou` is an alphanumeric variable that contains the name of the current field inputted. It is available on any control, init or help action.

# Comments

`zoncou` does not contain the current index on arrays. `indice` (0-based) or `nolign` (1-based) can give this information.

* If during an input check validation of a field has to be prevented, without sending a "beep" to the screen, simply assign to `zonsui` the name of the current field on which the check is made by using `zoncou`:

`zonsui` = `zoncou`

* If the field belongs to an array, you can write:
  `zonsui = zoncou+"(" + num$(index) + ")"`

# See also

[Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html), [zc](4gl_Zc.html), [zonsui](4gl_Zonsui.html), [zonsor](4gl_Zonsor.html).

  

[Index](index.html)  [Home](getting-started_home.html)