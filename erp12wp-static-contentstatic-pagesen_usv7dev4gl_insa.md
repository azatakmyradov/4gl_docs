[Index](index.html)  [Home](getting-started_home.html)

Insa

`Insa` is used to insert elements from single-sized arrays, from an index.

# Syntax

```
  Insa START ARRAY_LIST
  Insa START, NUMBER ARRAY_LIST
  Insa START, NUMBER, LIMIT ARRAY_LIST
```

* `START` is an integer expression that gives the index in the arrays from which the insertions are made. It cannot exceed the highest index and the smallest index available in the array list.
* `NUMBER` is an integer expression that gives the number of positions to be inserted. It must be strictly positive. If not given by the syntax, '1' will be used.
* `LIMIT` is an integer expression that gives the index in the arrays where the insertion ends. `LIMIT` cannot exceed the highest index and the smallest index available in the array list.
* `ARRAY_LIST` is a list of arrays variable (at least one) separated by commas.

Examples

Let's imagine we have three arrays called COMPOSER(1..11), NAME(1..11), and BIRTH\_YEAR(1..11), that have at the beginning the following values:

| Index | NAME | FIRSTNAME | BIRTH YEAR |
| --- | --- | --- | --- |
| 1 | BUXTEHUDE | Dietrich | 1637 |
| 2 | BACH | Johann Sebastian | 1685 |
| 3 | MOZART | Wolfgang Amadeus | 1756 |
| 4 | BEETHOVEN | Ludwig | 1770 |
| 5 | SCHUBERT | Frantz | 1797 |
| 6 | WAGNER | Richard | 1813 |
| 7 | STRAUSS | Richard | 1864 |
| 8 | SCHOENBERG | Arnold | 1874 |
| 9 | BERG | Alban | 1885 |
| 10 | STOCKHAUSEN | Karlheintz | 1928 |
| 11 |  |  | 0 |

After execution of:

```
Insa 1,2 COMPOSER, NAME, BIRTH_YEAR
```

  
The result will be the following. The last element of the list is lost because we had only one position that was empty at the end of the array:

| Index | NAME | FIRSTNAME | BIRTH YEAR |
| --- | --- | --- | --- |
| 1 |  |  | 0 |
| 2 |  |  | 0 |
| 3 | BUXTEHUDE | Dietrich | 1637 |
| 4 | BACH | Johann Sebastian | 1685 |
| 5 | MOZART | Wolfgang Amadeus | 1756 |
| 6 | BEETHOVEN | Ludwig | 1770 |
| 7 | SCHUBERT | Frantz | 1797 |
| 8 | WAGNER | Richard | 1813 |
| 9 | STRAUSS | Richard | 1864 |
| 10 | SCHOENBERG | Arnold | 1874 |
| 11 | BERG | Alban | 1885 |

Let's now execute the following instruction on the previous result:

```
Insa 6,2,10 COMPOSER, NAME, BIRTH_YEAR
```

| Index | NAME | FIRSTNAME | BIRTH YEAR |
| --- | --- | --- | --- |
| 1 |  |  | 0 |
| 2 |  |  | 0 |
| 3 | BUXTEHUDE | Dietrich | 1637 |
| 4 | BACH | Johann Sebastian | 1685 |
| 5 | MOZART | Wolfgang Amadeus | 1756 |
| 6 |  |  | 0 |
| 7 |  |  | 0 |
| 8 | BEETHOVEN | Ludwig | 1770 |
| 9 | SCHUBERT | Frantz | 1797 |
| 10 | WAGNER | Richard | 1813 |
| 11 | BERG | Alban | 1885 |

# Description and comments

`Insa` is used to insert elements (by default 1) from a set of single-sized arrays.

In every table, the elements are shifted to the end of the table (this is the default value for `LIMIT`) by a number of positions equal to `NUMBER`. The last `NUMBER` elements in the table are lost, and elements with null values are inserted from the `START` position (null dates, 0 for numeric values, and empty strings).

When `LIMIT` has a value that is smaller than the lowest limit of the arrays, elements from the `START` position to the `LIMIT` (inclusively) are shifted, the array elements after `LIMIT` are not shifted, and the `NUMBER` elements from position `LIMIT-NUMBER+1` to `LIMIT` are lost.

# Associated errors

|  |  |
| --- | --- |
| 8 | At least one of the indexes is outside the limits of one of the arrays. |
| 10 | START, NUMBER, or LIMIT are not numeric values. |
| 50 | NUMBER is less or equal to 0. |
| 55 | At least one of the arrays is not single sized. |

# See also

[Sorta](4gl_sorta.html), [Dela](4gl_dela.html).

  

[Index](index.html)  [Home](getting-started_home.html)