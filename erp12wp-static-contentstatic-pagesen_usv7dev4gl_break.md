[Index](index.html)  [Home](getting-started_home.html)

Break

This instruction is used to exit loops in scripts.

# Syntax

```
Break INTEGER_EXPRESSION
Break
```

* **`INTEGER_EXPRESSION`** is an expression returning the number of nested loops you will exit:
  + If no integer expression is given, the value is 1.
  + If the value is 0, nothing is done. The Break instruction can then be used with a single condition (such as `A=B`). If the condition is verified, the expression value is 1; and if not, the expression value is 0, and therefore no exit is done.

# Examples

```

  # This calculation loop continues as long as the expected precision is not reached, or if the condition
  # OUT_OF_RANGE becomes true (CHECK_DATA must returns 0 or 1 only)
  Repeat
    OUT_OF_RANGE=Func CHECK_DATA(DATA_ARRAY)
    Break OUT_OF_RANGE
    PRECISION=Func STEP_N(DATA_ARRAY)
  Until PRECISION<EXPECTED

  # This calculation loop continues as long as the expected precision is not reached, or if the condition
  # OUT_OF_RANGE becomes true (CHECK_DATA returns 0 if OK and any other error code if not ok)
  PRECISION=1
  While PRECISION>=EXPECTED
    OUT_OF_RANGE=Func CHECK_DATA(DATA_ARRAY)
    Break (OUT_OF_RANGE<>0)
    PRECISION=Func STEP_N(DATA_ARRAY)
  Wend


  # Multi-level database request
  # RESULT gives the final result of a computation that uses values stored in a database table
  # Stops if CODE is found equal to an EXIT_CODE value, if SUBCODE is found equal to EXIT_SUBCODE value,
  #       if ID is found equal to EXIT_ID value, or if AMOUNT is equal to EXIT_AMOUNT
  # Skips to the next (CODE,ID) group if CATEGORY is found equal to a SKIP_CATEGORY value, 

  Local Decimal RESULT
  Local File MYTABLE [MYT] Order By Key READ_KEY=[MYT]CODE;[MYT]SUBCODE;[MYT]CATEGORY;[MYT]ID

  For [MYT]READ_KEY(1) : # Loop on distinct CODE values
    Break [MYT]CODE=EXIT_CODE             : # Exit from the loop
    For [MYT]READ_KEY(2)                  : # Loop on distinct SUBCODE values for a given CODE value
      Break 2*([MYT]SUBCODE=EXIT_SUBCODE) : # Exit from the 2 nested loops if condition is true
      For [MYT]READ_KEY(3)                : # Loop on distinct CATEGORY values for a given (CODE,SUBCODE) pair
        Break CATEGORY=SKIP_CATEGORY      : # Exit from a unique level to go to the next (CODE,SUBCODE) pair
        For [MYT]READ_KEY(4)              : # Loop on distinct ID for a given (CODE,SUBCODE,CATEGORY) set
          If [MYT]ID=EXIT_ID
            Break 4                       : # Exit from all the nested loops
          Endif
          For [MYT]READ_KEY               : # Loop on all the records for a given (CODE,SUBCODE,CATEGORY,ID) set
            Break 5*(AMOUNT=EXIT_AMOUT)    : # Exit from all loops if condition is true
            RESULT=Func COMPUTATION(RESULT,[MYT]AMOUNT) : # Performs the computation
          Next
        Next
      Next
      # This is the point where the execution continues if we skip the category
    Next
  Next


  # Test a condition for values found in a 2 dimensions matrix
  # The loop is interrupted if the value is found.
  For I=1 to dim(MATRIX,1)
    For J=1 to dim(MATRIX,2)
      If MATRIX(I,J)=VECTOR(I+J)
        Break 2
      Endif
    Next J
  Next I
```

# Description and comments

The instruction Break can be used for any [For](4gl_for.html) / [Next](4gl_next.html) loop, [While](4gl_while.html) / [Wend](4gl_wend.html) loop, and [Repeat](4gl_repeat.html) / [Until](4gl_until.html) loops.

The exit is done at the end of the corresponding loop.

# See also

[For](4gl_for.html), [To](4gl_to.html), [Step](4gl_step.html), [Next](4gl_next.html), [While](4gl_while.html), [Wend](4gl_wend.html), [Repeat](4gl_repeat.html), [Until](4gl_until.html).

  

[Index](index.html)  [Home](getting-started_home.html)