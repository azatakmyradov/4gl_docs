[Index](index.html)  [Home](getting-started_home.html)

Min

This function is used to calculate the minimum for a list of elements such as dates, numeric values, or string values. It works on a list of elements that can be:  
\* Expressions.  
\* Arrays or sub-arrays of an array.  
\* Properties in an array of references.

# Syntax

```
min(ELEMENT_LIST)
```

\* `ELEMENT\_LIST` is a list of `ELEMENTS` separated by commas.
\* `ELEMENTS` can be:
\* Any expression.
\* An array identified by its name. All elements in the array will be considered.
\* A sub-array identified by an index value or an index range defined by the syntax `FIRST\_INDEX`..`LAST\_INDEX`. If several dimensions exist, the index range or the index values must be given for all dimensions.
\* A property in an array of child instances defined by the syntax `INSTANCE(FIRST\_INDEX..LAST\_INDEX).PROPERTY`.
\* `FIRST\_INDEX` and `LAST\_INDEX` are integer value returning an index value in an array.
\* `INSTANCE` is the name of an array of instances (class or representation).

# Examples

```
# Calculates the min for a list of computed values
MY_RATE=min(CURRENT_CURRENCY_RATE, AVERAGE_COMPOUND_RATE, LEGAL_RATE)

# Is there a unique delivery date for a sales order?
 If max(MYORDER.LINES(1..maxtab(MYORDER.LINES)).DELIVERYDATE<>min(MYORDER.LINES(1..maxtab(MYORDER.LINES)).DELIVERYDATE)
   MESSAGE="We have to ship the order lines at different dates"
 Else
   MESSAGE="All the lines can be delivered at the same date"
 Endif

# Maximum and minimum on a matrix of values
# We have NB_SALESREP sales representative in our department (NB_SALESREP<20)
Local Decimal TURNOVER(1..12,1..20), BEST_TURNOVER, WORST_TURNOVER
Local Integer MONTH, SALESREP_ID
  # Fill the array
  For MONTH=1 To 12
     For SALESREP_ID=1 To NB_SALESREP
       TURNOVER(MONTH,SALESREP_ID)=func GET_FIGURES(MONTH, SALESREP_ID)
     Next SALESREP_ID
  Next MONTH
  # Find out the best and the worst turnover
  BEST_TURNOVER=max(TURNOVER(1..12,1..NB_SALESREP))
  WORST_TURNOVER=min(TURNOVER1..12,1..NB_SALESREP))
```

# Comments

[Decimal](4gl_decimal.html), [integer](4gl_integer.html), [floating](4gl_float.html) point, and [double](4gl_double.html) variables may be mixed for a numerical minimum.

If one of the arguments in the function is an array variable without specifying index or range of indexes, all the variable elements are used. The specified index or range of indexes determines the elements to be considered.

If a range of indexes is given such that there is no element to consider, the result returned is the highest possible value such as a string of 255 values of 65535 code in UCS2, [31/12/9999], or highest numeric value depending on the type of variable.

The type of result depends on the type of argument:

* **Minimum of strings:** the result is a [Char](4gl_char.html) type.
* **Numerical minimum :** the result is a [Decimal](4gl_decimal.html) type.
* **Minimum of dates:** the result is a [Date](4gl_date.html) type.

# See also

[sum](4gl_sum.html), [prd](4gl_prd.html), [avg](4gl_avg.html), [max](4gl_max.html).

  

[Index](index.html)  [Home](getting-started_home.html)