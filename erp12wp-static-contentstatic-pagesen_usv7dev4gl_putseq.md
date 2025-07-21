[Index](index.html)  [Home](getting-started_home.html)

Putseq

`Putseq` writes data on a binary file opened by [Openo](4gl_openo.html) or [Openio](4gl_openio.html).

# Syntax

```
   Putseq INTEGER_EXPR, VAR_LIST
   Putseq INTEGER_EXPR, VAR_LIST Using [CLASS]
```

* `INTEGER_EXPR` is an integer expression that provides the number of elements to be written.
* `VAR_LIST` is a list of VAR separated by commas.
* `VAR` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX_LIST)`, where `INDEX_LIST` is a list of `N` integer values that provides the indexes of the element in the array.
* `N` must be equal either to `dim(VARIABLE_NAME,0)` or to `dim(VARIABLE_NAME,0)-1`. For arrays, the index list must give all the index values, except maybe the last one. If the last value is omitted, all the elements obtained for the values available for this index will be used.
* `[CLASS]` is the abbreviation that has been used to open the file.

# Examples

```
  # First example: let's write strings in a binary file
  # The lines will have a constant length of 10
  # They will be padded by 0
  Local Schar WORDS(5)(1..10)
  WORDS(1)="ONE":WORDS(2)="TWO": WORDS(3)="THREE":WORDS(4)="FOUR":WORDS(5)="FIVE":WORD(6)="SIX"
  WORDS(9)="NINE":WORDS(10)="TEN"
  Openo "MYFILE",0      Using [DMP]
  Iomode adxium 50      Using [DMP] : # ascii
  Putseq 6,WORDS        Using [DMP]
  Putseq 2,WORDS(9..10) Using [DMP]
  Openo            Using [DMP]
  # The file contains now 30 caracters that are the following (null representing a null character):
  # 'O','N','E','null','null','T','W','O','null','null','T','H','R','E','E','F','O','U','R','null',
  # 'F','I','V','E','null','S','I','X','null','null','N','I','N','E','null','T','E','N','null','null'

  # Second example: let's write a blob in a file
  Putseq 1,MYBLOB : # The exact size of the blob will be written

  # Third example: let's append an array of Long integers in a file
  # These long integer are written on four bytes
  # We stop the writing operation when a null integer is found
  Subprog WR_INT(FILE_NAME,INTEGER_ARRAY)
  Value Char FILE_NAME()
  Const Integer INTEGER_ARRAY(1..)
  Local Integer I
    # Count the number of elements to be written
    Repeat I+=1 Until I>dim(INTEGER_ARRAY) or INTEGER_ARRAY(I)=0
    I-=1
    Openo FILE_NAME,-1 Using [INTG]
    Putseq I,INTEGER_ARRAY Using [INTG]
    Openo Using [INTG]
  End

  # Fourth example: Write a multi-dimensional arrays of Integers
  Local Integer ARRAY(1..5,1..10,1..5,1..4)
  Call FILL_ARRAY(ARRAY)
  Openo "dumpfile",0
  # If the whole array needs to be written:
  # Putseq NUMBER,ARRAY will fail (only one unspecified dimension can be given)
  # Let's perform loops
  For I=1 to dim(ARRAY,1)
    For J=1 to dim(ARRAY,2)
      For K=1 to dim(ARRAY,3)
        Putseq dim(ARRAY,4),ARRAY(I,J,K)
      Next K
    Next J
  Next I
  Seek 0
  # Now everything is flushed
```

# Description

`Putseq` allows creating ASCII or binary files that have any content.

`Putseq` writes a number of elements provided by the first argument on the list, by using the variables until the number of elements to be written are reached. An element is either a single variable or an element of an array.

The elements are written on the file in the internal format of the data as argument. The following table of arrays provides the format and the number of bytes written according to the data type used:

| Data type | Format | Number of bytes written |
| --- | --- | --- |
| [TinyInt](4gl_tinyint.html) | byte | 1 byte |
| [Schar](4gl_schar.html) | Characters on one byte in ASCII(padded with zeros). | N bytes where N is the maximum size of the string. |
| [Shortint](4gl_shortint.html) | Short integer in big Endian format. | 2 bytes. |
| [Date variable](4gl_date.html) | Number of days since the [31/12/1599] as an integer in big Endian format. | 4 bytes. |
| [Date when defined in an [F] class](4gl_date.html) | Number of days since the [31/12/1599] as a 3-bytes integer in big Endian format. | 3 bytes. |
| [Decimal value with format N.M when defined in an [F] class.](4gl_decimal.html) | Number in a BCD format that corresponds to the C-ISAM format. | (N+M+E+3)/2 bytes, where E is 0 if M is even, and 1 if M is odd. |
| [Decimal value when defined as a variable](4gl_decimal.html) | Number in a BCD format that corresponds to the C-ISAM format with the maximum precision. | 16 bytes. |
| [Char](4gl_char.html) | Character string in UCS2 format. | 2\*N bytes where N is the maximum size of the character string. |
| [Clbfile](4gl_clbfile.html) | The contents of the clob padded by zeros. | N bytes where N is the maximum size of the CLOB (N=1024 if the Clbfile has a (0) dimension, 2048 if Clbfile has a (1) dimension, and so forth). |
| [Blbfile (binary data)](4gl_blbfile.html) | The exact content of the BLOB. | The exact size of the BLOB. |
| [Uuident (unique id)](4gl_uuident.html) | UUID in canonical format. | 16 bytes. |
| [Datetime](4gl_datetime.html) | Date time stored as an integer in big Endian. | 8 bytes. |

# Comments

The function [adxseek](4gl_adxseek.html)(1) or [adxseek](4gl_adxseek.html)("CLASS") if the file has been opened with a class name, gives the position, in bytes from the beginning of the file, where the next write operation will be done. The return value will be incremented every time a `Putseq` is performed. Its value is **-1** if no file has been opened for writing.

As the write operation is buffered, the file might be completely updated only when the file is closed by [(Openo]] or [Openio](4gl_openio.html). It is therefore possible to flush the writing operation by using `Seek 0` or `Seek 0 Using [CLASS]`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | INTEGER\_EXPR is not an integer expression. |
| 24 | Error during write execution. |
| 44 | No more space on device. |
| 55 | Too many unspecified dimension given on variables written. |
| 65 | File too large (writing limits exceeded). |

# See also

[Getseq](4gl_getseq.html), [Rdseq](4gl_rdseq.html), [Wrseq](4gl_wrseq.html), [adxseek](4gl_adxseek.html), [Seek](4gl_seek.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html).

  

[Index](index.html)  [Home](getting-started_home.html)