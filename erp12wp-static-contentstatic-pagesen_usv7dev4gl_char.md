[Index](index.html)  [Home](getting-started_home.html)

Char

This keyword declares a character string with a size limited to a value that cannot exceed 255 characters.

# Syntax

```
Local    Char NAME(LENGTH)
Local    Char NAME(LENGTH)(DIMENSIONS)
Variable Char NAME(LENGTH)(DIMENSIONS)
Value    Char NAME(LENGTH)(DIMENSIONS)
Const    Char NAME(LENGTH)(DIMENSIONS)
```

* `NAME` is the name of the variable declared.
* `LENGTH` is an integer value between 1 and 255 that defines the maximum length of the string.
* `DIMENSIONS` can be:
  + A single numeric value DIM (meaning that we have an array with an index range from 0 to DIM-1).
  + A range of numeric values INDEX1..INDEX2 (the index varies between INDEX1 and INDEX2).
  + Several indexes or index ranges separated by a comma . For multiple dimension arrays, up to four dimensions are possible.

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling sub-programs. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html) and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables, as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations declare the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted when the parenthesis are present (the dimension and index ranges are defined by the calling program).

# Example

```
# Direct declarations
Local Char MYTEXT(250), KEYWORDS(30)(1..100) : # 250 max character string, and an array of 30 char keywords
Local Char KEY_ARRAY(20)(1..10) : # An array of 10 character keys of 20 characters maximum.

# A sub-program sending a text and returning a result
Funprog SEND_TEXT(TEXT)
Variable Char TEXT()(,) : # A 2 dimensions matrix of character strings is sent as references
...
End SEND_STATUS

# A sub-program storing texts
Subprog STORE_TEXTS(TEXT)
Value Char TEXT()(1..3) : # An array of 3 elements is sent (a copy is done when passing the arguments)
...
End
```

# Comments

The dimension is the limit of the length allowed for the variable. Any attempt to assign a longer string or append characters over the limit defined by the length) will truncate the variable to the dimension.

The characters stored are double-byte characters. A [Schar](4gl_schar.html) declaration exists for single-byte characters, but its use is strongly discouraged.

There is still a Global declaration variable that exists for variables that have to be seen in the scope of a process execution, but its use is strongly discouraged.

# Implicit data type conversion

The Char data type will implicitly convert [Date](../4gl/date.md) and [Clbfile](../4gl/clbfile.md) to a Char

```
Local Char MY_CHAR(30)                 # Declare Char
Local Date MY_DATE
MY_DATE=[31/12/2099]
MY_CHAR = MY_DATE                      # MY_CHAR = "20991231"
...
Local Clbfile MY_CLOB
MY_CLOB=string$(3,"AB")                # MY_CLOB = "ABABAB"
MY_CHAR=CLOB                           # MY_CHAR = "ABABAB"
```

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Date](4gl_date.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)