[Index](index.html)  [Home](getting-started_home.html)

Dela

`Dela` is used to delete elements from single-sized arrays, from a given index.

# Syntax

```
  Dela START ARRAY_LIST
  Dela START, NUMBER ARRAY_LIST
  Dela START, NUMBER, LIMIT ARRAY_LIST
```

* `START` is an integer expression that gives the index in the arrays from which the deletions are made. It cannot exceed the highest index or fall short of the smallest index available in the array list.
* `NUMBER` is an integer expression that gives the number of indexes to be deleted. It must be strictly positive. If not given by the syntax, '1' will be used.
* `LIMIT` is an integer expression that gives the index in the arrays where the deletion ends. `LIMIT` cannot exceed the highest index and the smallest index available in the array list.
* `ARRAY_LIST` is a list of arrays variable (at least one), separated by commas.

Examples:

Let's imagine we have three arrays called COMPOSER(1..10), NAME(1..10), and BIRTH\_YEAR(1..10) that have at the beginning the following values:

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

After execution of:

```
Dela 1 COMPOSER, NAME, BIRTH_YEAR
```

  
The result will be the following. The empty lines at the end of the arrays are not listed:

| Index | NAME | FIRSTNAME | BIRTH YEAR |
| --- | --- | --- | --- |
| 1 | BACH | Johann Sebastian | 1685 |
| 2 | MOZART | Wolfgang Amadeus | 1756 |
| 3 | BEETHOVEN | Ludwig | 1770 |
| 4 | SCHUBERT | Frantz | 1797 |
| 5 | WAGNER | Richard | 1813 |
| 6 | STRAUSS | Richard | 1864 |
| 7 | SCHOENBERG | Arnold | 1874 |
| 8 | BERG | Alban | 1885 |
| 9 | STOCKHAUSEN | Karlheintz | 1928 |

Let's now execute the following instruction on the previous result:

```
Dela 2,3 COMPOSER, NAME, BIRTH_YEAR
```

  
The result will become:

| Index | NAME | FIRSTNAME | BIRTH YEAR |
| --- | --- | --- | --- |
| 1 | BACH | Johann Sebastian | 1685 |
| 2 | WAGNER | Richard | 1813 |
| 3 | STRAUSS | Richard | 1864 |
| 4 | SCHOENBERG | Arnold | 1874 |
| 5 | BERG | Alban | 1885 |
| 6 | STOCKHAUSEN | Karlheintz | 1928 |

Let's now execute the following instruction on the previous result:

```
Dela 3,2,5 COMPOSER, NAME, BIRTH_YEAR
```

  
The result will become:

| Index | NAME | FIRSTNAME | BIRTH YEAR |
| --- | --- | --- | --- |
| 1 | BACH | Johann Sebastian | 1685 |
| 2 | WAGNER | Richard | 1813 |
| 3 | BERG | Alban | 1885 |
| 4 |  |  | 0 |
| 5 |  |  | 0 |
| 6 | STOCKHAUSEN | Karlheintz | 1928 |

Let's now execute the following instruction on the previous result:

```
Dela 6,1 COMPOSER, NAME, BIRTH_YEAR
```

  
The result will become:

| Index | NAME | FIRSTNAME | BIRTH YEAR |
| --- | --- | --- | --- |
| 1 | BACH | Johann Sebastian | 1685 |
| 2 | WAGNER | Richard | 1813 |
| 3 | BERG | Alban | 1885 |

# Description and comments

`Dela` is used to delete elements (by default 1) from a set of single-sized arrays.

In every table, the elements are shifted from the end of the table (this is the default value for `LIMIT`) by a number of positions equal to `NUMBER`. The last `NUMBER` elements in the table are set to null values (0 for numeric values, null date for dates, and empty character strings for strings).

When `LIMIT` has a value that is smaller than the lowest limit of the arrays, elements from the `START` position to the `LIMIT` (inclusively) are shifted, the array elements after `LIMITS` are not shifted, and the `NUMBER` elements from position `LIMIT-NUMBER+1` to `LIMIT` are then set to null values.

# Associated errors

|  |  |
| --- | --- |
| 8 | At least one of the indexes is outside the limits of one of the arrays. |
| 10 | START, NUMBER, or LIMIT are not numeric values. |
| 50 | NUMBER is less or equal to 0. |
| 55 | At least one of the arrays is not single sized. |

# See also

[Sorta](4gl_sorta.html), [Insa](4gl_insa.html).

  

[Index](index.html)  [Home](getting-started_home.html)