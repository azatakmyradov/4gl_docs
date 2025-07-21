[Index](index.html)  [Home](getting-started_home.html)

Adxseek

`adxseek` returns the position of the read / write pointers on sequential files.

# Syntax

```
adxseek(INTEGER_EXPR)
adxseek (STRING_EXPR)
```

* `INTEGER_EXPR` is an expression returning an integer (can only be 0 or 1).
* `STRING_EXPR` is an expression returning a character string.

# Examples

```
# Subprogram copying a file containing text lines (end of line is line feed)
# Copy every line in the new file preceded by the position in the original file (in bytes)
# Ignore a final line if not followed by line feed
# Return the size of the file copied at the end
Subprog COPYFILE(PATH1,PATH2,FILE_SIZE)
Variable Char PATH1(),PATH2()
Variable Integer FILE_SIZE
Local Integer I
Local Char BUFFER(250)

  Openi PATH1,0
  Openo PATH2,0
  adxifs = '' : adxirs = chr$(10) : I = 1
  Repeat
    I=adxseek(0)    
    Rdseq BUFFER
    If fstat=0
      Wrseq "["+num$(I)+"]";
      Wrseq BUFFER
    Endif
  Until fstat=0
  I=adxseek(1)
  Openi : Openo
End I

# The same program, but with an abbreviation set on both open (INP for input, OUT for output)
Subprog COPYFILE(PATH1,PATH2,FILE_SIZE)
Variable Char PATH1(),PATH2()
Variable Integer FILE_SIZE
Local Integer I
Local Char BUFFER(250)

  Openi PATH1,0 Using [INP]
  Openo PATH2,0 Using [OUT]
  Iomode adxifs '' Using [INP] : Iomode adxirs chr$(10) Using [INP]
  Iomode adxifs '' Using [OUT] : Iomode adxirs chr$(10) Using [OUT]

  Repeat
    I=adxseek("INP")    
    Rdseq BUFFER Using [INP]
    If fstat=0
      Wrseq "["+num$(I)+"]"; Using [OUT]
      Wrseq BUFFER Using [OUT]
    Endif
  Until fstat=0
  I=adxseek("OUT")
  Openi Using [INP] : Openo Using [OUT]
End I
```

# Description

When a file is opened without abbreviation, the read pointer, that is the position difference in (bytes) between the beginning of the file and the place where the next information is read, is returned by `adxseek(0)`. If no file is opened, `adxseek(0)` returns 0.

For a file opened without abbreviation, the write pointer, that is the position difference in (bytes) between the beginning of the file and the place where the next information is written, is returned by `adxseek(1)`. If no file is opened, `adxseek(1)` returns 0.

If [Openio](4gl_openio.html) has been used without abbreviation, `adxseek(0)` and `adxseek(1)` have always the same value.

For a file opened with the `[abbrev]` abbreviation, the read or write pointer is retrieved by `adxseek("abbrev")`.

The `adxseek(0)` or `adxseek("abbrev")` if the file is opened in read mode, can be modified:  
- By a read operation ([Rdseq](4gl_rdseq.html), [Getseq](4gl_getseq.html)).  
- By a [Seek](4gl_seek.html) operation.

The `adxseek(1)` or `adxseek("abbrev")` can be modified if the file is opened in write mode:  
- By a write operation ([Wrseq](4gl_wrseq.html), [Putseq](4gl_putseq.html)).  
- By a [Seek](4gl_seek.html) operation only if the file is opened in read/write mode ([Openio](4gl_openio.html)).

These variables cannot be modified by an assignment.

# See also

[Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html), [Seek](4gl_seek.html), [Rdseq](4gl_rdseq.html), [Wrseq](4gl_wrseq.html), [Getseq](4gl_getseq.html), [Putseq](4gl_putseq.html), [Iomode](4gl_iomode.html), [adxifs](4gl_adxifs.html), [adxirs](4gl_adxirs.html).

  

[Index](index.html)  [Home](getting-started_home.html)