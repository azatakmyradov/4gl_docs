[Index](index.html)  [Home](getting-started_home.html)

Prd

This function is used to calculate the multiplication for a list of numeric elements. It works on a list of elements that can be:  
\* Expressions.  
\* Arrays or sub-arrays of an array.  
\* Properties in an array of references.

# Syntax

```
prd(ELEMENT_LIST)
```

* `ELEMENT_LIST` is a list of `ELEMENTS` separated by commas.
* `ELEMENTS` can be:
  + Any expression.
  + An array identified by its name. All elements in the array will be considered.
  + A sub-array identified by an index value or an index range defined by the syntax `FIRST_INDEX`..`LAST_INDEX`. If several dimensions exist, the index range or the index values must be given for all dimensions.
  + A property in an array of children instances defined by the syntax `INSTANCE(FIRST_INDEX..LAST_INDEX).PROPERTY`.
* `FIRST_INDEX` and `LAST_INDEX` are integer value returning an index value in an array.
* `INSTANCE` is the name of an array of instances (class or representation).

# Examples

```
# Calculates the average value for a list of computed values
FINAL_PRICE=prd(INITIAL_PRICE, COMPANY_MARKUP, SALESREP_MARKUP)

# product on a matrix of values
# We have NB_SALESREP sales representative in our department (NB_SALESREP<20)
Local Decimal COEFFICIENTS(1..12), INITIAL_VALUE, FINAL_VALUE
Local Integer MONTH
  # Fill the array
  For MONTH=1 To 12
     COEFFICIENT(MONTH)=func GET_COEFF(MONTH)
  Next MONTH
  INITIAL_VALUE=func GET_INITIAL_VALUE

  # Find out the final value after a year
  FINAL_VALUE=prd(INITIAL_VALUE, COEFFICIENT(1..12))
```

# Comments

[Decimal](4gl_decimal.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [TinyInt](4gl_tinyint.html), and [Shortint](4gl_shortint.html) data type variables may be mixed.

If one of the arguments in the function is an array variable without specifying index or range of indexes, all the variable elements are used. The specified index or range of indexes determines the elements to be considered.

If a range of indexes is given such that there is no element to consider, the result returned is 1.

# See also

[sum](4gl_sum.html), [avg](4gl_avg.html), [max](4gl_max.html), [min](4gl_min.html).

  

[Index](index.html)  [Home](getting-started_home.html)