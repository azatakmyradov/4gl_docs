[Index](index.html)  [Home](getting-started_home.html)

Sum

This function is used to perform an addition of numeric elements or a concatenation of string elements. It works on a list of elements that can be:  
\* Expressions.  
\* Arrays or sub-arrays of an array.  
\* Properties in an array of references.

# Syntax

```
sum(ELEMENT_LIST)
```

* `ELEMENT_LIST` is a list of `ELEMENTS` separated by commas.
* `ELEMENTS` can be:
  + Any expression.
  + An array identified by its name. All elements in the array will be considered.
  + A sub-array identified by an index value or an index range defined by the syntax `FIRST_INDEX`..`LAST_INDEX`. If several dimensions exist, the index range or the index values must be given for all dimensions.
  + A property in an array of child instances defined by the syntax `INSTANCE(FIRST_INDEX..LAST_INDEX).PROPERTY`.
* `FIRST_INDEX` and `LAST_INDEX` are integer value returning an index value in an array.
* `INSTANCE` is the name of an array of instances (class or representation).

# Examples

```
# Performs a sum for a list of totaled values
RESULT=sum(15*3,pi,PRICE*2)

# Concatenation in arrays
# Let's declare a matrix of 5 rows and 3 columns
Local Char MATRIX(3)(1..5,8..10)
# Additional variables 
Local Char STRING1(100),STRING2(100),STRING3(100),STRING4(100)
Local Integer NBDIM, FIRST_1, FIRST_2,LAST_1,LAST_2, I, J
# Let's get the dimensions
   NBDIM=dim(MATRIX,0) : # Returns 2
   FIRST_1=dim(MATRIX,-1) : LAST_1=FIRST_1+dim(MATRIX,1)-1 :  # Returns 1 and 5
   FIRST_2=dim(MATRIX,-2) : LAST_2=FIRST_2+dim(MATRIX,2)-1 :  # Returns 8 and 10
# Let's fill the array with A1, A2, A3... B1, B2, B3... elements
  For I=FIRST_1 to LAST_1
    For J=FIRST_2 to LAST_2
      MATRIX(I,J)=num$(1+I-FIRST_1)+chr$(65+J-FIRST_2)+" "
    Next J
  Next I
# Let's perform sums
 STRING1=sum(MATRIX) : # Returns "1A 2A 3A 4A 5A 1B 2B 3B 4B 5B 1C 2C 3C 4C 5C"
 STRING2=sum(MATRIX(2..3,10)): : # Returns "2C 3C"
 STRING3=sum(MATRIX(1..3,FIRST_2..LAST_2)) : # Returns "1A 2A 3A 1B 2B 3B 1C 2C 3C"
 STRING4=sum(MATRIX(FIRST_1..LAST_1,9..10)) : # Returns "1B 2B 3B 4B 5B 1C 2C 3C 4C 5C"

# Sum on a children instances
  MYORDER.GRANDTOTAL=sum(  MYORDER.LINES(1..maxtab(MYORDER.LINES)).PRICE,
&                          MYORDER.TAXES(1..3).AMOUNT,  MYORDER.FREIGHT    ) 

# Sum where no element is considered
NOTHING=sum(MY_ARRAY(1..0)) : # Returns 0 because the range from 1 to 0 has no element
```

# Comments

[Decimal](4gl_decimal.html), [integer](4gl_integer.html), [floating](4gl_float.html) point, and [double](4gl_double.html) variables may be mixed for a numerical total.

If one of the arguments in the function is an array variable without specifying index or range of indexes, all the variable elements are used. The index or range of indexes specified determines the elements to be considered.

If a range of indexes is given such that there is no element to consider, the result returned is 0 or an empty string, depending on the type of variable.

The type of result depends on the type of argument:

* **Concatenation of strings:** the result is a Char type.
* **Numerical total:** the result is:
  + ***An Integer type*** if there are only integers to be accumulated.
  + ***Double*** if there is at least one double precision element to be accumulated.
  + ***Decimal***.

# Associated errors

| Error code | Description |
| --- | --- |
| 8 | Range error for indexes. |
| 10 | The indexes given are not numeric. |
| 50 | Type mismatch in the list of expressions. |
| 55 | Too many dimensions given for an argument. |

# See also

[find](4gl_find.html), [max](4gl_max.html), [min](4gl_min.html), [uni](4gl_uni.html), [prd](4gl_prd.html), [avg](4gl_avg.html), [var](4gl_var.html).

  

[Index](index.html)  [Home](getting-started_home.html)