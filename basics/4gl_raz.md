[Index](index.html)  [Home](getting-started_home.html)

Raz

`Raz` allows you to set variables or variable classes to null values.

# Syntax

```
   Raz LIST_OF_CLAVAR
```

* `LIST_OF_CLAVAR` is a list of `CLASS` and/or `VARNAME` separated by commas.
* `CLASS` is a class name that must exist, such as [F:ABBR] for a table with the `ABBR` abbreviation, [L] for the local class, and [V] for the global class.
* `VARNAME` is a variable name that can be prefixed by a class and followed by an index value in the format (`IND_LIST`), where IND\_LIST is a list of index expressions separated by a comma. The number of elements in the list must correspond to the number of dimensions of the variable.

If an array variable is given without an index, all the indexes are erased.

# Examples

```
   # Set to zero all the local variables
   Raz [L]

   # Set to zero an element of a 2 dimensional array
   Raz MATRIX(1,5)

   # Set to zeo a list of variables and the buffer class of a table
   Raz I,J,K,[F:MYCUST], MY_DATE
```

# Description

`Raz` allows you to erase, or to reset to "null values" a class, or an array, element in an array, or a variable.

Although there is no real "null value" managed by the engine, the following value is set depending on the data type:

| Data type | Value set by Raz |
| --- | --- |
| [Char](../4gl/char.md), [Clbfile](../4gl/clbfile.md) | empty string " " |
| [TinyInt](../4gl/tinyint.md), [Shortint](../4gl/shortint.md), [Integer](../4gl/integer.md), [Decimal](../4gl/decimal.md), [Float](../4gl/float.md), [Double](../4gl/double.md) | 0 |
| [Date](4gl_date.html) | [0/0/0] |
| [Blbfile](4gl_blbfile.html) | null (0 byte) blob |
| [Datetime](4gl_datetime.html) | 0000-00-00T00:00:00Z |
| [Uuident](4gl_uuident.html) | 00000000-0000-0000-0000-000000000000 (nulluuid) |
| [Instance](4gl_instance.html) | Null |

# Associated errors

| Error code | Description |
| --- | --- |
| 6 | Variable does not exist. |
| 7 | Class does not exist. |

# See also

[Kill](4gl_kill.html).

  

[Index](index.html)  [Home](getting-started_home.html)