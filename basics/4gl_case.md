[Index](index.html)  [Home](getting-started_home.html)

Case

`Case` is used to provide an alternative control structure based on the value of a given expression.

# Syntax

```
 Case EXPRESSION
    When EXPRESSION_LIST
      INSTRUCTIONS
    ...
    When Default
      INSTRUCTIONS
 Endcase
```

\* `EXPRESSION\_LIST` is a list of expressions (at least one) separated by commas.
\* `EXPRESSION` is an expression that is evaluated and compared to the values found by calculating successively the expressions in EXPRESSION\_LIST for the following `When EXPRESSION\_LIST` instructions. The instructions found after the first matching `When` instruction are executed, and then the execution resumes after the `Endcase` instruction.

The `When Default` is optional; if present, it must be the last `When` instruction of the `Case`. The instructions placed after it will be executed only if no matching expression was found in all the `When` instruction following the `Case`.

# Examples

```
 # Depending on the value of CHOICE, a particular action will be performed.
 # If "R" is chosen, nothing is done.
    Case toupper(CHOICE)
           When "E","D" :  Gosub DELETION
           When "Q","S" :  Goto QUIT
           When "R"
           When "M"     :  Gosub MODIFICATION
           When Default : Gosub HELP
    Endcase


   # Alternative on the expression date$-NUMBER_OF_DAYS that is compared to
   # other variables or complex expressions
   # For all the other cases, as there is no "When Default" instruction, nothing will be executed
   #
    Case date$-NUMBER_OF_DAYS
           When [29/05/1959]
                   RESULT="This is my birthday"
           When [18/06/1944],[08/05/1945],[11/11/1918]
                   RESULT= "This was a historical date"
                   RESULT+=" ("+format$(D:DD[/]MM[ ]4Y",date$-NUMBER_OF_DAYS)+")"
           When date$
                   RESULT "We are today"
                   Gosub ACTIONS_TODAY
    Endcase
```

# Description and comments

* `Case` is used to allow alternatives within a script based on the value of an expression that will be compared to lists of values.
* At most, one alternative is executed (a `Case` is the same as [If] â¦ [Elsif] â¦ [Else] â¦ [Endif]). If there is no `When Default` instruction and if no value matches the expression, no instruction in the `Case` will be executed.
* No instruction can be placed within the `Case` and the first `When` (not even a comment).
* When no instructions are found between a `When` and the next `When`instruction, no instruction will be executed if the first `When` matches the `Case`, unlike languages such as C. In order to execute the same instructions for several values, you have to put them in a list that follows the `When` instruction.

# Errors

| Code | Description |
| --- | --- |
| 10 | An expression found in a list cannot be compared to the expression following the Case (the data types are not compatible). |

# See also

[When](4gl_when.html), [Endcase](4gl_endcase.html), [If](4gl_if.html), [Then](4gl_then.html), [Else](4gl_else.html), [Endif](4gl_endif.html).

  

[Index](index.html)  [Home](getting-started_home.html)