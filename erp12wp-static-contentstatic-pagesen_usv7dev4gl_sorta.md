[Index](index.html)  [Home](getting-started_home.html)

Sorta

`Sorta` is used to sort arrays of single-dimensioned variables.

# Syntax

```
Sorta ARRAY_LIST
Sorta NUMBER ARRAY_LIST
Sorta ARRAY_LIST Order By EXPRESSION_LIST
Sorta NUMBER ARRAY_LIST Order By EXPRESSION_LIST
Sorta ARRAY_LIST ASCDES
Sorta NUMBER ARRAY_LIST ASCDES
Sorta ARRAY_LIST Order By EXPRESSION_LIST ASCDES
Sorta NUMBER ARRAY_LIST Order By EXPRESSION_LIST ASCDES
```

* `NUMBER` is an integer expression that gives the number of positions to be sorted. It must be strictly positive. If not given by the syntax, all the elements will be sorted.
* `ARRAY_LIST` is a list of arrays variable (at least one) separated by commas.
* `EXPRESSION_LIST` is a list of expressions using elements of the arrays with the `[S]indice` system variable used as the current index.
* `ASCDES` is the [Asc](4gl_asc.html) or [Desc](4gl_desc.html) keyword (ascending or descending order). The ascending order is used by default. This option is used on all expression lists or on all the columns.

# Example

You have three arrays called COMPOSER(1..11), FIRST\_NAME(1..11), and BIRTH\_YEAR(1..11). In this example, you can see the original order and the final order after the `Sorta` instruction, depending on the syntax:

|  |  |
| --- | --- |
| ``` Sorta 10 BIRTH_YEAR, COMPOSER, FIRST_NAME ``` | |
| Original order | Sorting order |
| | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | HAENDEL | Georg | 1685 | | 2 | BACH | Johann | 1685 | | 3 | STRAUSS | Johann | 1804 | | 4 | BEETHOVEN | Ludwig | 1770 | | 5 | SCHUBERT | Frantz | 1797 | | 6 | WAGNER | Richard | 1813 | | 7 | STRAUSS | Johann | 1825 | | 8 | STRAUSS | Richard | 1864 | | 9 | BERG | Alban | 1885 | | 10 | MOZART | Wolfgang | 1756 | | 11 |  |  | 0 | |  
  
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | BACH | Johann | 1685 | | 2 | HAENDEL | Georg | 1685 | | 3 | MOZART | Wolfgang | 1756 | | 4 | BEETHOVEN | Ludwig | 1770 | | 5 | SCHUBERT | Frantz | 1797 | | 6 | STRAUSS | Johann | 1804 | | 7 | WAGNER | Richard | 1813 | | 8 | STRAUSS | Johann | 1825 | | 9 | STRAUSS | Richard | 1864 | | 10 | BERG | Alban | 1885 | | 11 |  |  | 0 | |  

  
|  
 ``` Sorta BIRTH_YEAR, COMPOSER, FIRST_NAME ``` | |  

  
|  
 Original order | Sorting order |  

  
|  
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | HAENDEL | Georg | 1685 | | 2 | BACH | Johann | 1685 | | 3 | STRAUSS | Johann | 1804 | | 4 | BEETHOVEN | Ludwig | 1770 | | 5 | SCHUBERT | Frantz | 1797 | | 6 | WAGNER | Richard | 1813 | | 7 | STRAUSS | Johann | 1825 | | 8 | STRAUSS | Richard | 1864 | | 9 | BERG | Alban | 1885 | | 10 | MOZART | Wolfgang | 1756 | | 11 |  |  | 0 | |  
  
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 |  |  | 0 | | 2 | BACH | Johann | 1685 | | 3 | HAENDEL | Georg | 1685 | | 4 | MOZART | Wolfgang | 1756 | | 5 | BEETHOVEN | Ludwig | 1770 | | 6 | SCHUBERT | Frantz | 1797 | | 7 | STRAUSS | Johann | 1804 | | 8 | WAGNER | Richard | 1813 | | 9 | STRAUSS | Johann | 1825 | | 10 | STRAUSS | Richard | 1864 | | 11 | BERG | Alban | 1885 | |  

  
|  
 ``` Sorta 10 COMPOSER,FIRST_NAME,BIRTH_YEAR Order By COMPOSER(indice+1), -BIRTH_YEAR(indice+1), FIRST_NAME(indice+1) ``` | |  

  
|  
 Original order | Sorting order |  

  
|  
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | HAENDEL | Georg | 1685 | | 2 | BACH | Johann | 1685 | | 3 | STRAUSS | Johann | 1804 | | 4 | BEETHOVEN | Ludwig | 1770 | | 5 | SCHUBERT | Frantz | 1797 | | 6 | WAGNER | Richard | 1813 | | 7 | STRAUSS | Johann | 1825 | | 8 | STRAUSS | Richard | 1864 | | 9 | BERG | Alban | 1885 | | 10 | MOZART | Wolfgang | 1756 | | 11 |  |  | 0 | |  
  
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | BACH | Johann | 1685 | | 2 | BEETHOVEN | Ludwig | 1770 | | 3 | BERG | Alban | 1885 | | 4 | HAENDEL | Georg | 1685 | | 5 | MOZART | Wolfgang | 1756 | | 6 | SCHUBERT | Frantz | 1797 | | 7 | STRAUSS | Richard | 1864 | | 8 | STRAUSS | Johann | 1825 | | 9 | STRAUSS | Johann | 1804 | | 10 | WAGNER | Richard | 1813 | | 11 |  |  | 0 | |  

|  
 ``` Sorta 10 COMPOSER,FIRST_NAME,BIRTH_YEAR Order By FIRST_NAME(indice+1),NAME(indice+1),-BIRTH_YEAR(indice+1) Desc ``` | |  

  
|  
 Original order | Sorting order |  

  
|  
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | HAENDEL | Georg | 1685 | | 2 | BACH | Johann | 1685 | | 3 | STRAUSS | Johann | 1804 | | 4 | BEETHOVEN | Ludwig | 1770 | | 5 | SCHUBERT | Frantz | 1797 | | 6 | WAGNER | Richard | 1813 | | 7 | STRAUSS | Johann | 1825 | | 8 | STRAUSS | Richard | 1864 | | 9 | BERG | Alban | 1885 | | 10 | MOZART | Wolfgang | 1756 | | 11 |  |  | 0 | |  
  
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | MOZART | Wolfgang | 1756 | | 2 | WAGNER | Richard | 1813 | | 3 | STRAUSS | Richard | 1864 | | 4 | BEETHOVEN | Ludwig | 1770 | | 5 | BACH | Johann | 1685 | | 6 | STRAUSS | Johann | 1804 | | 7 | STRAUSS | Johann | 1825 | | 8 | HAENDEL | Georg | 1685 | | 9 | SCHUBERT | Frantz | 1797 | | 10 | BERG | Alban | 1885 | | 11 |  |  | 0 | |

# Comments

* The `Sorta` instruction is used to sort single-dimension elements of arrays. If the number of elements is not specified, the sort is performed on a number of elements defined by the smallest dimension of the arrays present.
* The `Sorta` instruction does not work on collections in class instances.
* The sort is ascending by default. However, it is possible to sort an array on a numeric field in descending order by multiplying this field by -1.
* When there is no [Order By](4gl_order-by.html) clause, the sort is performed in the order of the first array. If elements in this array are equal, it will be performed in the order of the second array, and so forth for all the arrays to be sorted.
* If an [Order By](4gl_order-by.html) clause is specified, the sort is done in the order of the first expression, the second if some values are the same, and so forth.
* The algorithms used make the sort non-conservative. This means that if elements in the ordering expressions are the same for two index values, you cannot know in which order they will appear in the results for other arrays.
* The `[S]indice` value starts with 0. Thus, if an array that has an index starting with 1 is sorted with an expression, this expression must use `indice+1` and not `indice`.

Example of unexpected result when `indice` is used for arrays starting at index 1:

|  |  |
| --- | --- |
| ``` Sorta 5 COMPOSER,FIRST_NAME, BIRTH_YEAR Using -BIRTH_YEAR(indice),COMPOSER(indice) ``` | |
| Original order | Sorting order |
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | HAENDEL | Georg | 1685 | | 2 | BACH | Johann | 1685 | | 3 | STRAUSS | Johann | 1804 | | 4 | BEETHOVEN | Ludwig | 1770 | | 5 | SCHUBERT | Frantz | 1797 | |  
  
 | # | COMPOSER | FIRST\_NAME | BIRTH\_YEAR | | --- | --- | --- | --- | | 1 | BEETHOVEN | Ludwig | 1770 | | 2 | SCHUBERT | Frantz | 1797 | | 3 | STRAUSS | Johann | 1804 | | 4 | BACH | Johann | 1685 | | 5 | HAENDEL | Georg | 1685 | |

The reason is that the array was sorted in the order of the following expressions:

* For `SCHUBERT` (line 2 before the sort), `-BIRTH_YEAR(1)` is -1804
* For `SCHUBERT` (line 5 before the sort), `-BIRTH_YEAR(4)` is -1770
* For `STRAUSS` (line 3 before the sort), `-BIRTH_YEAR(2)` is -1685 and `FIRST_NAME(2)` is "Johann"
* For `BACH` (line 2 before the sort), `-BIRTH_YEAR(1)` is -1685 and `FIRST_NAME(1)` is "Georg"
* For `BEETHOVEN` (line 1 before the sort), `-BIRTH_YEAR()` is undefined (0 by default)

# Associated errors

| Error code | Description |
| --- | --- |
| 8 | Incorrect index value. |
| 10 | NUMBER is not a numeric expression. |
| 50 | NUMBER is negative. |

# See also

* [Insa](4gl_insa.html)
* [Dela](4gl_dela.html)

  

[Index](index.html)  [Home](getting-started_home.html)