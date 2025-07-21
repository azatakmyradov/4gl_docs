[Index](index.html)  [Home](getting-started_home.html)

Qstbox

`Qstbox` displays a popup windows with a message including a question. The user clicks on Yes or No to answer to the question.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

```
   Qstbox MESSAGE_LIST Using ANSWER
   Qstbox MESSAGE_LIST Titled TITLE Using ANSWER
   Qstbox MESSAGE_LIST Titled TITLE Using ANSWER Sleep TIME
   Qstbox MESSAGE_LIST Using ANSWER Sleep TIME
```

* `MESSAGE_LIST` is a list of string expressions separated by commas. The content of each string is displayed on a different line.
* `TITLE` is a string expression that contains the title of the popup that appears.
* `TIME` is an integer expression that gives a time-out before the popup closes automatically. If not given, the popup closes only when a click is done on a possible answer button.
* `ANSWER` is an variable that gives the answer to the question. The possible values are 1 (Yes) or 2 (No). No default value can be given before calling this function. If a time-out occurs, 2 is sent back.

# Examples

```
# If the computation returns a small value without error, ask for continuing
 Local Integer CONT
 Call COMPUTATION(FORMULA,RESULT, ERROR)
  If ERROR=0 and RESULT<10
    Qstbox "The following formula has been computed",FORMULA,
&          "with a small result (equal to "+num$(RESULT)+")",
&          "Do you wish to continue the process?"
&   Titled "Do you really want to continue?" Using CONT Sleep 60
    If CONT= 1
      Call NEXT_COMPUTATION
    Endif
  Endif
```

# Description

`Qstbox` behaves as `Infbox`, but the popup looks different ("?" symbol on a blue bar).  
This instruction should be used only to display a message followed by a yes/no question.

# See also

[Endbox](4gl_Endbox.html), [Errbox](4gl_Errbox.html), [Infbox](4gl_Infbox.html), [Selbox](4gl_Selbox.html), [Wrnbox](4gl_Wrnbox.html)

  

[Index](index.html)  [Home](getting-started_home.html)