[Index](index.html)  [Home](getting-started_home.html)

Sigma

`sigma` allows you to perform the sum of a series of numeric expressions and the concatenation of a series of expressions returning strings. These expressions depend on an index value that varies between two values with a step of 1.

# Syntax

```
(1)   sigma(VAR_NAME = START_INDEX, END_INDEX, EXPRESSION)
(2)   sigma(START_INDEX, END_INDEX, EXPRESSION)
```

* `VAR_NAME` is the name of the variable, optionally prefixed by a class identifier `[CLASS]`.
* `START_INDEX` is a numeric expression that returns the starting value for the addition loop.
* `END_INDEX` is a numeric expression that returns the ending value for the addition loop.
* `EXPRESSION` is an expression that usually includes `VAR_NAME` (syntax 1) or `indcum` (syntax 2), system variable used by default as current index for the loop.

# Examples

```
   # Let's compute the latin alphabet (uppercase)
    ALPHABET = sigma(I=1,26,chr$(64+I))
   # At the end of the loop, the value of I is 27

   # Let's create a random string containing uppercase letters (in this case, non indcum is used!) 
    RANDOM_STRING=sigma(1,MAXL,chr$(65+int(rnd(25))))

   # Let's compute the sum of the squares from 1 to N
     SQUARE_SUM = sigma(I=1,N,I*I)
   # The same function with indcum
     SQUARE_SUM = sigma(1,N,indcum*indcum )
   # The same result without sigma...
     SQUARE_SUM = N*(N+1)*(N+2)/6

   # Double sum
    DOUBLE_SUM = sigma(I=1,N, sigma(J=1,I,J*J))
   # Can be written with the following statements (but it is less effective)
    DOUBLE_CUM=0
    For I=1 To N
      For J=1 To I
        DOUBLE_CUM+=J*J
      Next J
    Next I
```

# Description

`sigma` allows you to calculate the sum of an expression that depends on an index varying by steps of one between two values. This function works also on character strings, where the summation is performed as a string concatenation.

If the index interval is such that no loop is performed (for example, `sigma(I=1,0,I)`), the result returned is 0, even if the expression is a string expression.

The type of result depends on the type of arguments:

* If the expression is a string, the type of result is:
  + [Char](4gl_char.html) if the length is 255 or less,
  + [Clbfile](4gl_clbfile.html) otherwise.
* If the expression is numeric, the type of result is:
  + [Integer](4gl_integer.html) if only integers are cumulated and if the total does not exceed the range of integer values.
  + [Double](4gl_double.html) if a floating point expression is used,
  + [Decimal](4gl_decimal.html) otherwise.

# Comment

[indcum](4gl_indcum.html) is an integer variable: thus it is usable only if it varies in an integer interval (between -2^31 and 2^31-1). If `sigma` expressions need to be nested, it is necessary to use an index variable that is not `indcum`.

If the variable loop given does not exist, it is created with the [Decimal](4gl_decimal.html) data type.

The final value for the index variable corresponds to the first value that comes out of the range of the loop.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The index given is not numeric. |

# See also

[sum](4gl_sum.html), [indcum](4gl_indcum.html), [For](4gl_for.html), [Next](4gl_next.html), [Step](4gl_step.html).

  

[Index](index.html)  [Home](getting-started_home.html)