[Index](index.html)  [Home](getting-started_home.html)

Seek

`Seek` allows you to move the read pointer on a file opened by [Openi](4gl_openi.html) or [Openio](4gl_openio.html).  
When a null value is sent, it also allows you to flush the [write](4gl_write.html) operation performed on a file opened by [Openo](4gl_openo.html) or [Openio](4gl_openio.html).

# Syntax

```
  Seek POSITION MOVE_EXPR
  Seek MOVE_EXPR
  Seek POSITION MOVE_EXPR Using [CLASS]
  Seek MOVE_EXPR Using [CLASS]
```

* `POSITION` can be one of the following combination of keywords:
  + `Last` `-`: to give a position from the end position of the file.
  + `First` `+`: to give a position from the beginning of the file.
  + `Curr` `+`: to give a relative position ahead of the current position in the file.
  + `Curr` `-`: to give a relative backward position compared to the current position in the file.
* `MOVE_EXPR` is an expression that gives the position in bytes.
* `[CLASS]` is the class abbreviation used to open the file. If it is not given, the file opened without abbreviation is considered.

# Examples

```
   # Let's open a file and read 10 bytes every 20 bytes
    SChar BUFFERS(10)(MAXLINES)
    Openi "MYFILE"
    fstat = 0 : I = 0
    Repeat
       Getseq 1, BUFFERS(I) : I += 1
       Seek 10
    Until fstat <> 0 or I >= MAXLINES
    Openi

   # Let's rewrite the 50 last bytes of a file
    Tinyint BUFFER(50)
    Openio "MYFILE"
    Seek Last - 50
    Getseq 50, BUFFER
   # ..  BUFFER is modified
    Seek Last - 50
    Putseq 50, BUFFER
    Openio

   # When 2 files are opened:
   # Let's rewrite the 50 last bytes of the second file with the first 50 bytes of the first file
    Tinyint BUFFER(50)
    Openi "MYFILE1" Using [YYY]
    Openio "MYFILE2" Using [ZZZ]
    Getseq 50, BUFFER Using [YYY]
    Seek Last - 50 Using [ZZZ]
    Putseq 50, BUFFER Using [ZZZ]
    Openio Using [ZZZ]
    Openi Using [YYY]

   # Write 1 byte with "flush" on a file opened without abbreviation
    Putseq 1, MY_BYTE
    Seek 0
```

# Description

`Seek` allows you to move the read or read/write pointer when a file is opened by [Openi](4gl_openi.html) or [Openio](4gl_openio.html). The move can be done relatively at:   
\* The beginning of the file.   
\* The current position.   
\* The end of the file.

On some special files (devices), you may not perform a `Seek` operation and will therefore receive an error.

The `Seek 0` syntax flushes the write buffer when the file has been opened by [Openo](4gl_openo.html) or [Openio](4gl_openio.html). It is important, because the write operation is buffered. This syntax can be used on any abbreviation linked to a sequential file (on a file opened by [Openi](4gl_openi.html), nothing will happen).

# Comments

The function [adxseek](4gl_adxseek.html)(0) or [adxseek](4gl_adxseek.html)("CLASS") (for a file opened with the `[CLASS]` abbreviation) allows you to know the current position on the file (in bytes) relatively to the beginning. If no file has been opened, a -1 value is returned.

This function is updated even if you are unable to perform a `Seek` on the file because it is a special file. In this case, it counts the number of bytes that have been written since the opening of the file.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | Non numeric value for MOVE\_EXPR. |
| 24 | No file opened in read or read/write mode. |
| 50 | Non integer value for MOVE\_EXPR. |
| 57 | Unable to perform a Seek operation on this file. |

# See also

[Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html), [Getseq](4gl_getseq.html), [Rdseq](4gl_rdseq.html), [Putseq](4gl_putseq.html), [Wrseq](4gl_wrseq.html), [adxifs](4gl_adxifs.html), [adxirs](4gl_adxirs.html), [adxium](4gl_adxium.html), [adxmso](4gl_adxmso.html).

  

[Index](index.html)  [Home](getting-started_home.html)