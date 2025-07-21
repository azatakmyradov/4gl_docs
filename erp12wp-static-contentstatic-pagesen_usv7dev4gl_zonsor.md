[Index](index.html)  [Home](getting-started_home.html)

zonsor

`zonsor` is a system variable that contains the name of the last field entered when an input in a mask is performed.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   [S]zonsor
   zonsor
```

# Examples

```
# Example in object management
# The button "a" is activated
# then, after the execution of the action, we give back the hand to the last field entered

# Button definition
$DEFBOUT
NBTEX += 1 : CBOUT(NBTEX) = "a"
TEX(NBTEX) = "a button"
Return

# Button execution
$EXEBOUT
Case REP
    When "a" : Gosub HANDLE_BUTTON_A : zonsui = zonsor
Endcase
Return
```

# Description

`zonsor` is an alphanumeric variable that contains the name of the last field inputted.

# See also

[Affzo](4gl_Affzo.html), [Diszo](4gl_Diszo.html), [Effzo](4gl_Effzo.html), [Envzo](4gl_Envzo.html), [Grizo](4gl_Grizo.html), [zc](4gl_Zc.html), [zonsui](4gl_Zonsui.html), [zoncou](4gl_Zoncou.html).

  

[Index](index.html)  [Home](getting-started_home.html)