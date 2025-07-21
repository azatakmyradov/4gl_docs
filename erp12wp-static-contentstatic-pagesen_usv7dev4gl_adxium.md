[Index](index.html)  [Home](getting-started_home.html)

Adxium

`Adxium` is a numeric value that defines the coding method used for writing or reading character strings in a text file by the instructions [Wrseq](4gl_wrseq.html) and [Rdseq](4gl_rdseq.html).

# Syntax

```
adxium
Iomode adxium EXPRESSION Using [ABBREVIATION]
```

* **`EXPRESSION`** is an alphanumeric expression returning the value of the separator.
* **`ABBREVIATION`** is the abbreviation that has been used to open the file by [Openi](4gl_openi.html), [Openo](4gl_openo.html), or [Openio](4gl_openio.html).

# Comments

Note that this is a global value for all the files opened. Using the [Iomode](4gl_iomode.html) instruction gives you the control on every file opened; which is preferable.

The values that are associated with adxium are the following:

* **50** corresponds to an ASCII file.
* **122** corresponds to an UCS2 file. Every character takes 2 bytes in the file.
* Any other value corresponds to a UTF8 file. This coding is identical to ASCII for the classic characters (those less than 128), and a more complex coding on 2, 3 even 4 bytes for the other characters.

By default, `Adxium` is set to a coding in UTF8.

# Examples

```
# Let's read a text file generated in UCS2 with CR+LF at the end of every line
# And let's write the result in a UTF8 coded file with LF at the end of every line

Subprog COPY_FROM_UCS2_TO_UTF8(INPUT_FILE,OUTPUT_FILE)
Value Char INPUT_FILE(), OUTPUT_FILE()

Local Char BUFFER(250) : # The lines must not exceed 250 characters

  Openi INPUT_FILE Using [INP]
  Iomode adxifs '' Using [INP]
  Iomode adxirs chr$(13)+chr$(10) Using [INP]
  Iomode adxium 122 Using [INP] : # UCS2

  Openo OUTPUT_FILE Using [OUT]
  Iomode adxifs '' Using [OUT]
  Iomode adxirs chr$(10) Using [OUT]
  Iomode adxium 0 Using [OUT] : # UTF8

  Repeat
     Rdseq BUFFER Using [INP]
     If fstat
        If BUFFER<>""
           Wrseq BUFFER; Using [OUT]
        Endif
     Else
        Wrseq BUFFER Using [OUT]
     Endif
   Until fstat

   Openo Using [OUT]
   Openi Using [INP]
End
```

# See also

[adxifs](4gl_adxifs.html), [adxirs](4gl_adxirs.html), [Rdseq](4gl_rdseq.html), [Wrseq](4gl_wrseq.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html).

  

[Index](index.html)  [Home](getting-started_home.html)