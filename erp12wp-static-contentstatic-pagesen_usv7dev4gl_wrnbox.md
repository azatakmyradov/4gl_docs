[Index](index.html)  [Home](getting-started_home.html)

Wrnbox

`Wrnbox` displays a popup windows with an information message.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Wrnbox MESSAGE_LIST
   Wrnbox MESSAGE_LIST Titled TITLE
   Wrnbox MESSAGE_LIST Titled TITLE Sleep TIME
   Wrnbox MESSAGE_LIST Sleep TIME
```

* `MESSAGE_LIST` is a list of string expressions separated by commas. The content of each string is displayed on a different line.
* `TITLE` is a string expression that contains the title of the popup that appears.
* `TIME` is an integer expression that gives a time-out before the popup closes automatically. If not given, the popup closes only when a click is done on the `OK` button.

# Examples

```
# The computation failed because no valid entry is there
 Call COMPUTATION(FORMULA,RESULT, ERROR)
  If ERROR=1
    Wrnbox "The following formula has been computed",FORMULA,
&          "with the following result",num$(RESULT)
&   Titled "Warning" Sleep 60
  Endif
```

# Description

`Wrnbox` behaves as `Endbox`, but the popup looks different (exclamation mark on a yellow bar).  
This instruction should be used only to display warning messages.

# See also

[Endbox](4gl_Endbox.html), [Errbox](4gl_Errbox.html), [Infbox](4gl_Infbox.html), [Qstbox](4gl_Qstbox.html), [Selbox](4gl_Selbox.html).

  

[Index](index.html)  [Home](getting-started_home.html)