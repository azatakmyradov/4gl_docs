[Index](index.html)  [Home](getting-started_home.html)

Getseq

`Getseq` reads data from a binary file opened by [Openi](4gl_openi.html) or [Openio](4gl_openio.html).

# Syntax

```
   Getseq INTEGER_EXPR, VAR_LIST
   Getseq INTEGER_EXPR, VAR_LIST Using [CLASS]
```

* `INTEGER_EXPR` is an integer expression that provides the number of elements to be read.
* `VAR_LIST` is a list of VAR separated by commas.
* `VAR` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX_LIST)`, where `INDEX_LIST` is a list of `N` integer values that gives the indexes of the element in the array.
* `N` must be equal to `dim(VARIABLE_NAME,0)` or to `dim(VARIABLE_NAME,0)-1`. For arrays, the index list must provide all the index values, except for the last one. If the last one is omitted, all the elements obtained for the values available for this index will be used.
* `[CLASS]` is the abbreviation that has been used to open the file.

# Examples

```
  # First example: let's read strings in a binary file
  # The lines have a constant length of 10
  # They are padded by 0
  Local Schar WORDS(5)(1..20)
  Openi "MYFILE",0      Using [DMP]
  Getseq 5,WORDS        Using [DMP]
  Getseq 3,WORDS(8..12) Using [DMP]
  Openi            Using [DMP]
  # Only the indexes 1 to 5, and 8 to 10 have been read.
  # The indexes 11 and 12 have been set to empty strings

  # Second example: let's red a blob in a file
  Getseq 1,MYBLOB 

  # Third example : Read a multi-dimensional arrays of Integers
  Local Integer ARRAY(1..5,1..10,1..5,1..4)
  Openi "dumpfile",0
  # If the whole array needs to be read:
  # Getseq NUMBER,ARRAY will fail (only one unspecified dimension can be given)
  # Let's perform loops
  For I=1 to dim(ARRAY,1)
    For J=1 to dim(ARRAY,2)
      For K=1 to dim(ARRAY,3)
        Getseq dim(ARRAY,4),ARRAY(I,J,K)
      Next K
    Next J
  Next I
```

# Description

`Getseq` allows reading ASCII or binary files that have any content.

`Getseq` reads from a file and fills a number of elements given by the first argument on the list and by using these variables until the number of elements to be filled is reached. An element is either a single variable or an element of an array.

The elements are transferred from the file into the variable based on the format of the data given as an argument. The following array provides the format and the number of bytes written according based on the data type used, as indicated in the following table:

| Data type | Format | Number of bytes read |
| --- | --- | --- |
| [TinyInt](4gl_tinyint.html) | Byte. | 1 byte. |
| [Schar](4gl_schar.html) | Characters on one byte in ASCII (padded with zeros). | N bytes where N is the maximum size of the string. |
| [Shortint](4gl_shortint.html) | Short integer in big Endian format. | 2 bytes. |
| [Date variable](4gl_date.html) | Number of days since the [31/12/1599] as an integer in big Endian format. | 4 bytes. |
| [Date when defined in a [F] class](4gl_date.html) | Number of days since the [31/12/1599] as a 3-byte integer in big Endian format. | 3 bytes. |
| [Decimal value with format N.M when defined in a [F] class](4gl_decimal.html) | Number in a BCD format that corresponds to the C-ISAM format. | (N+M+E+3)/2 bytes, where E is 0 if M is even and 1 if M is odd. |
| [Decimal value when defined as a variable](4gl_decimal.html) | Number in a BCD format that corresponds to the C-ISAM format with the maximum precision. | 16 bytes. |
| [Char](4gl_char.html) | Character string in UCS2 format. | 2\*N bytes where N is the maximum size of the character string. |
| [Clbfile](4gl_clbfile.html) | The contents of the CLOB padded by zeros. | N bytes where N is the maximum size of the CLOB (N=1024 if the Clbfile has a (0) dimension, 2048 if Clbfile has a (1) dimension, and so forth). |
| [Blbfile (binary data)](4gl_blbfile.html) | The exact content of the BLOB. | The exact size of the BLOB. |
| [Uuident (unique id)](4gl_uuident.html) | UUID in canonical format. | 16 bytes. |
| [Datetime](4gl_datetime.html) | Date time stored as an integer in big Endian format. | 8 bytes. |

# Comments

The function [adxseek](4gl_adxseek.html)(0) or [adxseek](4gl_adxseek.html)("CLASS"), if the file has been opened with a class name, gives the position (in bytes, from the beginning of the file) where the next read operation will be done. The return value will be incremented every time a `Getseq` is performed. Its value is '-1' if no file has been opened for reading.

The system variable [fstat](4gl_fstat.html) is set to '1' if the read operation reached the end of the file.

The variables that cannot be assigned because the end of the file was reached or the number of elements is reached, are set to null values.

If the number of elements to be read is bigger than the total number of elements given as argument, no error occurs.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | INTEGER\_EXPR is not an integer expression. |
| 55 | Too many unspecified dimensions on variables written. |

# See also

[Putseq](4gl_putseq.html), [Rdseq](4gl_rdseq.html), [Wrseq](4gl_wrseq.html), [adxseek](4gl_adxseek.html), [Seek](4gl_seek.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html).

  

[Index](index.html)  [Home](getting-started_home.html)