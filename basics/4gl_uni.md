[Index](index.html)  [Home](getting-started_home.html)

Uni

`uni` allows you to verify if there are duplicated values in a list of variables or expressions that can have any type (numeric, string CLOB, dates, UUIDs, or datetime).

# Syntax

```
   uni(ELEMENT_LIST)
```

* `ELEMENT_LIST` is a list of `ELEMENTS` separated by commas.
* `ELEMENTS` can be:
  + Any expression.
  + An array identified by its name. All elements in the array are considered.
  + A subarray identified by an index value or an index range defined by the syntax `FIRST_INDEX`..`LAST_INDEX`. If several dimensions exist, the index range or the index values must be given for all dimensions.
  + A property in an array of child instances defined by the syntax `INSTANCE(FIRST_INDEX..LAST_INDEX).PROPERTY`.
* `FIRST_INDEX` and `LAST_INDEX` are integer value returning an index value in an array.
* `INSTANCE` is the name of an array of instances (class or representation).

The expressions must have comparable types:  
\* [Date](4gl_date.html) types can be compared with [Date](4gl_date.html) and [Datetime](4gl_datetime.html) types.  
\* [Decimal](4gl_decimal.html) types can be compared with [TinyInt](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), and [Double](4gl_double.html) types.  
\* [Char](4gl_char.html) can be compared with [Schar](4gl_schar.html) and [Clbfile](4gl_clbfile.html) types.

# Examples

```
   # Are there duplicated values in the list? After execution, I contains 3
    I=uni(24, 15, 24, 1, 2, 3, pi, 4, 5)

   # Control of a collection where no duplicate values must exist on the CODE column
   I = uni(this.LINES(1..maxtab(this.LINES)).CODE)
   If I
     J = find(this.LINES(I).CODE,this.LINES(1..maxtab(this.LINES)).CODE)
     [L]ASTATUS=Fmet this.ASETERROR("","Duplicate code"-this.LINES(I).CODE-"at lines"-num$(I)-"and"-num$(J),[V]CST_AERROR)
   Endif
```

# Description

`uni` allows you to verify if at least a duplicate value is present on a list of values. `uni` returns the rank of the first duplicate value on the list, and returns 0 if no duplicate value is found. For example:

* If the two first values of the list are equal, `uni` returns 2.
* If the first and the third values of the list are equal, or if the second and the third values are equal, `uni` returns 3.

If one of the arguments is an array variable, all the elements are considered, except if an index or an index range is given to limit the indexes.

If an index interval is given so that no value is included (for example, `uni(ARRAY(1..0))`, the result returned is 0.

When an element in an array of instances is considered (for example, `MYINSTANCE(1..N).PROPERTY`), the elements in the array that are not allocated (the values of I for which `MYINSTANCE(I)`equals `Null`) are counted even if there is no `PROPERTY` value assigned. This means that the following code is valid:

```
 # Works even if all LINES instances are not defined in the MYINSTANCE.LINE array
 I=uni(MYINSTANCE.LINES(1..maxtab(MYINSTANCE.LINES)).PROPERTY)
 If I
   DUPLICATE_VALUE=MYINSTANCE.LINES(I).PROPERTY
   J=find(DUPLICATE_VALUE,MYINSTANCE.LINES(1..maxtab(MYINSTANCE.LINES)).PROPERTY)
   SAME_DUPLICATE_VALUE=MYINSTANCE.LINES(J).PROPERTY
 Endif
```

  
The type of result for`uni` is [Integer](4gl_integer.html). Note that `uni` can never return 1.

# Associated errors

| Error code | Description |
| --- | --- |
| 8 | Range error for indexes. |
| 10 | The indexes given are not numeric. |
| 50 | Type mismatch on the list of expressions. |
| 55 | Too many dimensions given for an argument. |

# See also

[find](4gl_find.html), [max](4gl_max.html), [min](4gl_min.html), [sum](4gl_sum.html), [prd](4gl_prd.html), [avg](4gl_avg.html), [var](4gl_var.html).

  

[Index](index.html)  [Home](getting-started_home.html)