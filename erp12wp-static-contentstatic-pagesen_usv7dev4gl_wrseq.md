[Index](index.html)  [Home](getting-started_home.html)

Wrseq

`Wrseq` writes string data on a binary file opened by [Openo](4gl_openo.html) or [Openio](4gl_openio.html).

# Syntax

```
   Wrseq  EXPR_LIST
   Wrseq  EXPR_LIST,
   Wrseq  EXPR_LIST Using [CLASS]
   Wrseq  EXPR_LIST, Using [CLASS]
```

* `EXPR_LIST` is a list of expressions separated by commas.
* `[CLASS]` is the abbreviation that is used to open the file.

# Examples

```
  # First example: let's write strings in a file
  # The lines are written in ascii mode with CR+LF as separators
  # We stop at the first empty line
  Local Char TEXT_LINES(100)(1..1000)
  Gosub FILL_TEXT
  Openo "mytext",0                Using [TXT]
  Iomode adxium 50                Using [TXT] : # ascii
  Iomode adxirs chr$(13)+chr$(10) Using [TXT] : # CRLF
  For I=1 to dim(TEXT_LINES)
    Break TEXT_LINES(I)=""
    Wrseq TEXTLINES(I) Using [TXT]
  Next I
  Openo using [TXT]

  # Second example: let's write a clob in a file (in UTF8)
   adxium=0 : # UTF8
   Wrseq MYBLOB : # The exact size of the blob will be written

  # Third example: let's write the content of a multi-dimensional array of integers in a file
  # These long integer are written as strings representing numeric values
  # Every line contains the list of the element in the last dimension
  Local Integer ARRAY(1..5,1..10,1..5,1..4)
  Call FILL_ARRAY(ARRAY)
  Openo "dumpfile",0
  # Let's perform loops
  For I=1 to dim(ARRAY,1)
    For J=1 to dim(ARRAY,2)
      For K=1 to dim(ARRAY,3)
        For L=1 to dim(ARRAY,4)
          Wrseq ARRAY(I,J,K,L),
        Next L
        Wrseq
      Next K
    Next J
  Next I
  Seek 0
  # Now everything is flushed
```

# Description

`Wrseq` allows creating text files with a format that can be ASCII or UTF8, depending on how [adxium](4gl_adxium.html) is set. UCS2 texts are not supported by `Wrseq`.

`Wrseq` writes every expression in a list separated by commas or semicolons. The expressions are written as a text representation of the data content (exactly like the [num$](4gl_num$.html) function).

When several expressions are given in a list, the separator set by [adxifs](4gl_adxifs.html) is written between the elements. When the list ends with a comma or a semicolon, the same field separator is used.

When the list given by `Wrseq` does not end with a comma or a semicolon, a record separator defined by [adxirs](4gl_adxirs.html) is written.

Both [adxifs](4gl_adxifs.html) and [adxirs](4gl_adxirs.html) can be set to an empty value. They are directly assigned if the file is opened without abbreviation; otherwise, they must be assigned with the [Iomode](4gl_iomode.html) instruction.

# Comments

The function [adxseek](4gl_adxseek.html)(1) or [adxseek](4gl_adxseek.html)("CLASS"), if the file is opened with a class name, gives the position (in bytes, from the beginning of the file) where the next write operation is done. The return value is incremented every time a `Wrseq` is performed. Its value is -1 if no file is opened for writing.

As the write operation is buffered, the file can be completely updated only when the file is closed by [(Openo]] or [Openio](4gl_openio.html). It is therefore possible to flush the writing operation by using `Seek 0` or `Seek 0 Using [CLASS]`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | INTEGER\_EXPR is not an integer expression. |
| 24 | Error during write execution. |
| 44 | No more space on device. |
| 55 | Too many unspecified dimension given on variables written. |
| 65 | File too large (writing limits exceeded). |

# See also

[Getseq](4gl_getseq.html), [Rdseq](4gl_rdseq.html), [Putseq](4gl_putseq.html), [adxseek](4gl_adxseek.html), [Seek](4gl_seek.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html).

  

[Index](index.html)  [Home](getting-started_home.html)