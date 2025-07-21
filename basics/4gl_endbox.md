[Index](index.html)  [Home](getting-started_home.html)

Endbox

`Endbox` displays a popup windows with a serious error message.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Endbox MESSAGE_LIST
   Endbox MESSAGE_LIST Titled TITLE
   Endbox MESSAGE_LIST Titled TITLE Sleep TIME
   Endbox MESSAGE_LIST Sleep TIME
```

* `MESSAGE_LIST` is a list of string expressions separated by commas. The content of each string is displayed on a different line.
* `TITLE` is a string expression that contains the title of the popup that appears.
* `TIME` is an integer expression that gives a time-out before the popup closes automatically. If not given, the popup closes only when a click is done on the `OK` button.

# Examples

```
# The computation failed because no valid entry is there
 Call COMPUTATION(FORMULA,RESULT, ERROR)
 If ERROR=4
   Endbox "The following formula couldn't be computed",FORMULA Titled "Computation Error" Sleep 10
 Endif
```

# Description

`Endbox` behaves as `Errbox`, but the popup looks different (exclamation mark on a red bar).  
This instruction should be used only to display blocking / fatal errors.

# See also

[Errbox](4gl_Errbox.html), [Infbox](4gl_Infbox.html), [Qstbox](4gl_Qstbox.html), [Selbox](4gl_Selbox.html), [Wrnbox](4gl_Wrnbox.html)

  

[Index](index.html)  [Home](getting-started_home.html)