[Index](index.html)  [Home](getting-started_home.html)

If

`If` is used to perform tests in a script.

# Syntax

```
  If NUMERIC_EXPRESSION
    list_of_instructions_if
  Endif

  If NUMERIC_EXPRESSION
    list_of_instructions_if
  Else
    list_of_instructions_else
  Endif

  If NUMERIC_EXPRESSION
    list_of_instructions_if
  Elsif NUMERIC_EXPRESSION
    list_of_instructions_elsif
  Endif

  If NUMERIC_EXPRESSION
    list_of_instructions_if
  Elsif NUMERIC_EXPRESSION
    list_of_instructions_elsif
  Else
    list_of_instructions_else
  Endif
```

# Examples

```
# First example
  If I=1
    # Line executed if I=1
  Else
    # Line executed if I is not equal to 1
  Endif

# Second example
  If find(CHOICE,"YES","SURELY","CERTAINLY","PERHAPS","MAYBE","POSSIBLY")
    # If CHOICE is in the values listed, find returns the rank in the list and this branch will be executed
  Else
    # If CHOICE is out of the list, find returns 0 and this branch will be executed
  Endif

# More complex alternative
If I=1
  # Line executed if I=1
Elsif I=2 or I=1
  # Line executed only if I=2 (the first branch has been executed if I=1)
Elsif func STRANGE(I)=3
  # Line executed if the condition is fulfilled. Take care, I might have been modified by Funprog STRANGE
Elsif I=1 or I=3
  # Line executed if I was not equal to 1 and 2, if the condition STRANGE(I)=3 was false,
  # buf if I is equal to 1 or 3 after execution of STRANGE Subprog
Else
  # Line executed in all other cases
Endif
```

# Description and comments

* If the value of NUMERIC\_EXPRESSION is nonzero, `list_of_instructions_if` is executed.
* If optional [Elsif](4gl_elsif.html) conditions are present, the condition found after every [Elsif](4gl_elsif.html) is evaluated, and the `list_of_instructions_elsif` found after the first [Elsif](4gl_elsif.html) for which NUMERIC\_EXPRESSION is nonzero will be executed.
* If the optional [Else](4gl_else.html) is present, `list_of_instructions_else` is executed if the value of the expression in all the [Elsif](4gl_elsif.html) conditions is zero.
* NUMERIC\_EXPRESSION must be of arithmetic or logical type.
* In all forms of the `If` statement, the expression is evaluated, including all unexpected results if a [Funprog](4gl_funprog.html) is called. After execution of the instructions found in the right branch of the [If](4gl_if.html)/[Elsif](4gl_elsif.html)/[Else](4gl_else.html)/[Endif](4gl_endif.html) nesting structure, the instruction following the [Endif](4gl_endif.html) instruction is executed, except if a [Break](4gl_break.html), [End](4gl_end.html), or [Goto](4gl_goto.html) function is executed in the branch.

# See also

[Else](4gl_else.html), [Elsif](4gl_elsif.html), [Endif](4gl_endif.html).

  

[Index](index.html)  [Home](getting-started_home.html)