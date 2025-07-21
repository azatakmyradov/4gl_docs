[Index](index.html)  [Home](getting-started_home.html)

Var

Use `var` to calculate the variance of a series of numeric values. It works on a list of elements that can be:  
\* Expressions.  
\* Arrays or subarrays of an array.  
\* Properties in an array of references.

# Syntax

```
sum(ELEMENT_LIST)
```

* `ELEMENT_LIST` is a list of `ELEMENTS` separated by commas.
* `ELEMENTS` can be:
  + Any expression.
  + An array identified by its name. All elements in the array are considered.
  + A subarray identified by an index value or an index range defined by the syntax `FIRST_INDEX`..`LAST_INDEX`. If several dimensions exist, the index range or the index values must be given for all dimensions.
  + A property in an array of child instances defined by the syntax `INSTANCE(FIRST_INDEX..LAST_INDEX).PROPERTY`.
* `FIRST_INDEX` and `LAST_INDEX` are integer value returning an index value in an array.
* `INSTANCE` is the name of an array of instances (class or representation).

# Examples

```
# Computes the variance of a list of computed values
RESULT=var(15*3,pi,PRICE*2)

# Variance on a children instances
  MYORDER.VARIANCE=var(MYORDER.LINES(1..maxtab(MYORDER.LINES)).PRICE,
&                          MYORDER.TAXES(1..3).AMOUNT,  MYORDER.FREIGHT)
```

# Description

`var` calculates the variance of a series, given by the following formula:

`(sx2-(sx*sx/n))/n`

Where:

* `sx2` is the sum of the squares of all the numbers in the series.
* `sx` is the sum of all the numbers in the series.
* `n` is the number of elements in the series.

If one of the arguments in the function is an array variable without specifying index or range of indexes, all the variable elements are used. The index or range of indexes specified determines the elements to consider.

If a range of indexes is given such as there is no element to consider in the whole list, the result is 0.

The type of result depends on the type of arguments, but it is usually [Decimal](4gl_decimal.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 8 | Range error for indexes. |
| 10 | The indexes given are not numeric. |
| 50 | At least one argument is not numeric. |
| 55 | Too many dimensions given for an argument. |

# See also

[find](4gl_find.html), [max](4gl_max.html), [min](4gl_min.html), [uni](4gl_uni.html), [prd](4gl_prd.html), [avg](4gl_avg.html), [sum](4gl_sum.html).

  

[Index](index.html)  [Home](getting-started_home.html)