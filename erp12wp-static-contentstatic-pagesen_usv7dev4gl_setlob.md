[Index](index.html)  [Home](getting-started_home.html)

Setlob

`Setlob` allows you to assign a CLOB data with a string variable array and vice versa.

# Syntax

```
  Setlob VARIA1 With VARIA2
```

* `VARIA1` can have one of the following syntaxes:

  + `VARIA`.
  + `VARIA`(`INDEX_LIST`).
* `VARIA2` can have one of the following syntaxes:

  + `VARIA`.
  + `VARIA`(`INDEX_LIST`).
  + `VARIA`(`INDEX_RANGE`).

Where:

* `VARIA` is a variable name that can be prefixed with a class.
* `INDEX_LIST` is a list of `INDEX` separated by commas. The number of elements on the list must be the same as the number of dimensions of `VARIA`.
* `INDEX_RANGE` is a range of `INDEX` separated by `..`.
* `INDEX` is an expression that returns an index value.

# Examples

```
  # Let's assign TEXT array with the content of a clob (stored in the database table [MYT])
  Local Char TEXT (250)(1..100)
  Setlob TEXT With [F:MYT]CLOB

  # Let's assign only the second line with the content of the clob
  Local Char TEXT (250)(1..100)
  Setlob TEXT(2) With [F:MYT]CLOB

  # Let's assign the clob with the content of all the lines in TEXT.
  Local Char TEXTE (250)(1..100)
  Setlob [F:MYT]CLOB With TEXT(1..100)
```

# Description

`Setlob` allows you to perform an assignment between two variables:   
\* One must be of type [Char](4gl_char.html).   
\* The other of type [Clbfile](4gl_clbfile.html).

The first parameter describes the element that is assigned. The second element describes the origin of the assignment.

Both parameters can be arrays of variables. If no dimension is given, all the elements in the array are considered.

If the second parameter is an array, the origin can be:   
\* The whole array.   
\* A subarray given by a range of indexes.   
\* A unique element given by the corresponding index.

When the transfer is done from a CLOB to a [Char](4gl_char.html) array, the CLOB is cut in chunks of 'N' characters, where 'N' is the maximum character string in the array.

When a variable is set by a CLOB that contains RTF, all the texts including attributes are copied.

# Associated errors

| Error code | Description |
| --- | --- |
| 6 | Variable does not exist. |
| 7 | Incorrect index. |

# See also

[Char](4gl_char.html), [Clbfile](4gl_clbfile.html).

  

[Index](index.html)  [Home](getting-started_home.html)