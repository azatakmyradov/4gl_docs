[Index](index.html)  [Home](getting-started_home.html)

Disable

`Disable` allows to disable buttons and/or links present at a bottom of a screen or on the menu bar of a function.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
  Disable LIST_OF_BUTTON_CODE
```

LIST\_OF\_BUTTON\_CODE is a list of integer values representing buttons or links, separated by a comma. For some predefined button, global variables are usable.

# Examples

```
# Disable "Create" and "Save" actions in the "File" sub-menu
  Disable GSTACRE, GSTAENR

# Could be written with the corresponding values (but using glbal variables is preferable in this case)
  Disable 93, 92

# Disable buttons specific to a given function
  Disable GSTABOU+1, GSTABOU+2

# Let's call a dialog box and enable/disable some specific buttons
# depending on a condition
Local Dlgbox Mask ABC button mess(15,198,1), mess(101,198,1)
&                     coded   GSTABOU+1, GSTABOU+2       
Local Integer OK

  Boxact [ABC]
  Gosub CONDITION : # Sets OK to true or false
  If OK Then Enable GSTABOU+1, GSTABOU+2
  Else       Disable GSTABOU+1, GSTABOU+2
  Endif
Boxinp [ABC] using ANSWER
```

# Description and comments

`Disable` is used to disable the use of buttons and/or menu items. It is used before the input in a dialog box.

# Comment

In standard object management, `Disable` is mostly used in the SETBOUT action, and most of the status usable with this instruction are defined with global variables.

The standard subprogram SETBOUT from script GESECRAN encapsulates the use of `Disable` for the most frequent status and should preferably be used, like in the following example:

```
# Let's disable the "Create" and "Save" actions (like the first example given above
Local Integer ETABOU(1..GNBBOU)
ETABOU (GCREE) = 0
ETABOU (GENRE) = 0
Call SETBOUT(ETABOU) From GESECRAN
```

# See also

[Enable](4gl_Enable.html), [Grizo](4gl_Grizo.html), [status](4gl_Status.html).

  

[Index](index.html)  [Home](getting-started_home.html)