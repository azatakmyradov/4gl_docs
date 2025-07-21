[Index](index.html)  [Home](getting-started_home.html)

Avg

This function is used to compute the average value of a list of numeric elements. It works on a list of elements that can be:  
\* Expressions.  
\* Arrays or sub-arrays of an array.  
\* Properties in an array of references.

# Syntax

```
avg(element_list)
```

* `element_list` is a list of `elements` separated by commas.
* `elements` can be:
  + Any expression.
  + An array identified by its name. All elements in the array will be considered.
  + A sub-array identified by an index value or an index range defined by the syntax `first_element`..`last_element`. If several dimensions exist, the index range or the index values must be given for all dimensions.
  + A property in an array of child instances defined by the syntax `instance(first_element..last_element).property`.

# Examples

```
# Computes the average value of a list of computed values
MY_RATE=max(CURRENT_CURRENCY_RATE, AVERAGE_COMPOUND_RATE, LEGAL_RATE)

# average value on a matrix of values
# We have NB_SALESREP sales representative in our department (NB_SALESREP<20)
Local Decimal TURNOVER(1..12,1..20), AVERAGE_TURNOVER
Local Integer MONTH, SALESREP_ID
  # Fill the array
  For MONTH=1 To 12
     For SALESREP_ID=1 To NB_SALESREP
       TURNOVER(MONTH,SALESREP_ID)=func GET_FIGURES(MONTH, SALESREP_ID)
     Next SALESREP_ID
  Next MONTH
  # Find out the average turnover
  AVERAGE_TURNOVER=avg(TURNOVER(1..12,1..NB_SALESREP))
```

# Comments

[Decimal](4gl_decimal.html), [integer](4gl_integer.html), [floating point](4gl_float.html), and [double variables](4gl_double.html) variables may be mixed.

If one of the arguments in the function is an array variable without specifying index or range of indexes all the variable elements are used. The specified index or range of indexes determines the elements to be considered.

At least one element must be present on the list. If a range of indexes is given such as there is no element to consider, a "division per zero" error is raised.

# See also

[sum](4gl_sum.html), [prd](4gl_prd.html), [max](4gl_max.html), [min](4gl_min.html).

  

[Index](index.html)  [Home](getting-started_home.html)