[Index](index.html)  [Home](getting-started_home.html)

Find

`find` searches for a value on a list of expressions or arrays of variables for a given type.

# Syntax

```
   find(SEARCHED_EXPR,SEARCH_LIST)
```

* `SEARCHED_EXPR` is an expression of any type that defines the value to search.
* `SEARCH_LIST` is a list separated by commas that can include:
  + Expressions that must have a consistent type with the type of `SEARCHED_EXPR` (numeric, string, date, datetime, and so forth).
  + Variables that can be arrays (all the elements of the array are considered).
  + Subarrays with the syntax `ARRAY_NAME` ( `START_INDEX`..`END_INDEX`). This works only on an array that has a single dimension.

# Examples

```
   # Test if I is equal to 1, 3, 5 or 6
    If find(I,1,3,4,6)<>0
      # I has one of the values listed
    Endif

   # Searches if the first element of the array is repeated in another index
   If find(MY_ARRAY)
     # The first index value of MY_ARRAY is present in another index of the array
   Endif

   # Let's replace a value by another value
   # the array IN gives the value that must be replaced
   # the array OUT gives the corresponding values
   I=find(INPUT_VALUE,IN) : # If I is not null, the rank is given
   If I>0
     OUTPUT_VALUE=OUT(dim(OUT,-1)+I-1) : # dim(OUT,-1) gives the first index value of OUT
   Endif

  # Let's perform an SQL sentence ... Where COLUMN in (value_list)
  Local File MY_TABLE where find (COLUMN,VALUE_LIST)<>0

  # Let's perform an SQL sentence ... Where COLUMN not in (value_list)
  Local File MY_TABLE where find (COLUMN,VALUE_LIST)=0
```

# Description

`find` searches a value on a list of values of any type. The result is the rank in the search, or 0 if the value is not found. The list of values must be comparable. It means that integer, tiny integer, decimal, floating point expressions, or variables can be mixed on a list; while strings with numeric expressions or dates cannot.

If one of the function arguments is an array, all the indexes are used except if a range is given to limit the number of values used. If the range causes no argument, the result is 0. For example, with an expression such as:

`find(RESULT,MY_ARRAY(1..0)`

`find` returns an [Integer](4gl_integer.html) value.

Using `find` in a SQL syntax allows you to implement the `in` or the `not in` operator. This is much more efficient than the `or` operator.

For example:

`File MYTABLE Where COLUMN=1 or COLUMN=3 or COLUMN=17`

Is less efficient than

`File MYTABLE Where find(COLUMN,1,3,17)<>0`

# Limit about find in Where clauses

The number of arguments that can be used in a `Where find` clause is limited, because the values are stored in a buffer that has a size of 32 KB.

This means practically:

* That up to 8000 values can be given if the column filtered is an integer
* That on a 10 character string that takes 2\*(10+1) bytes because of Unicode encoding, up to 1454 values can be given.

# Associated errors

| Error code | Description |
| --- | --- |
| 8 | Range errors on array indexes. |
| 10 | The argument is not numeric. |
| 50 | No value on the list (for example, find ARRAY(1..0)). |
| 55 | Too many dimensions. |

# See also

[max](4gl_max.html), [min](4gl_min.html), [sum](4gl_sum.html), [prd](4gl_prd.html),[avg](4gl_avg.html), [var](4gl_var.html), [uni](4gl_uni.html).

  

[Index](index.html)  [Home](getting-started_home.html)