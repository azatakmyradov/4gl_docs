[Index](index.html)  [Home](getting-started_home.html)

Rdseq

`Rdseq` reads data from a text file opened by [Openi](4gl_openi.html) or [Openio](4gl_openio.html).

# Syntax

```
   Rdseq VAR_LIST
   Rdseq VAR_LIST Using [CLASS]
```

* `VAR_LIST` is a list of VAR separated by commas.
* `VAR` can be either a single variable name, or an element in an array with the syntax `VARIABLE_NAME (INDEX_LIST)`, where `INDEX_LIST` is a list of `N` integer values that gives the indexes of the elements in the array.
* `N` must be equal either to `dim(VARIABLE_NAME,0)` or to `dim(VARIABLE_NAME,0)-1`. For arrays, the index list must give all the index values, except maybe the last one. If the last one is omitted, all the elements obtained for the values available for this index are used.
* `[CLASS]` is the abbreviation that has been used to open the file.

# Examples

```
  # First example: let's read words separated by commas in a text file
  # The lines separator is LF
  # They are padded by 0
  Local Schar WORDS(5)(1..20)
  Openi "MYFILE",0       Using [DMP]
  Iomode adxium 50       Using [DMP] : # ascii
  Iomode adxirs chr$(10) Using [DMP] : # LF
  Iomode adxifs ","      Using [DMP] : # word separator
  Rdseq WORDS        Using [DMP]
  Openi            Using [DMP]

  # Second example: let's read a blob in a file
  Rdseq MYBLOB 

  # Third example: read a multi-dimensional arrays of Integers
  Local Integer ARRAY(1..5,1..10,1..5,1..4)
  Openi "dumpfile",0
  # If the whole array needs to be read:
  # Rdeq NUMBER,ARRAY will fail (only one unspecified dimension can be given)
  # Let's perform loops
  For I=1 to dim(ARRAY,1)
    For J=1 to dim(ARRAY,2)
      For K=1 to dim(ARRAY,3)
        Rdseq ARRAY(I,J,K,1..dim(ARRAY,4))
      Next K
    Next J
  Next I
```

# Description

`Rdseq` allows reading ASCII files.

`Rdseq` reads from a file and fills the elements on the list until the end of line defined by [adxirs](4gl_adxirs.html) is reached. Every element is separated from the next element by [adxifs](4gl_adxifs.html). If the end of line is reached before all the elements are set, the remaining elements are set to null values.

The elements are transformed from text format (according to [adxium](4gl_adxium.html) value) to the variables listed.

# Comments

If the file is opened with a class name, the function [adxseek](4gl_adxseek.html)(0) (or [adxseek](4gl_adxseek.html)("CLASS")) gives the position (in bytes, from the beginning of the file) where the next read operation is done. The return value is incremented each time a `Rdseq` is performed. Its value is -1 if no file is opened for reading.

The system variable [fstat](4gl_fstat.html) is set to 1 if the read operation reached the end of the file.

The variables that could not be assigned because the end of file was reached or because the number of elements given is reached are set to null values.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | INTEGER\_EXPR is not an integer expression. |
| 55 | Too many unspecified dimensions given on variables written. |

# See also

[Putseq](4gl_putseq.html), [Getseq](4gl_getseq.html), [Wrseq](4gl_wrseq.html), [adxseek](4gl_adxseek.html), [Seek](4gl_seek.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html).

  

[Index](index.html)  [Home](getting-started_home.html)