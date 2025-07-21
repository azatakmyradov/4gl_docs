[Index](index.html)  [Home](getting-started_home.html)

Iomode

Use `Iomode` to assign a value to the different parameters associated with a sequential file opened by [Openi](4gl_openi.html), [Openio](4gl_openio.html), or [Openo](4gl_openo.html) when doing an abbreviation.

These parameter are [adxium](4gl_adxium.html), [adxifs](4gl_adxifs.html), and [adxirs](4gl_adxirs.html).

# Syntax

```
 Iomode adxifs STRING_EXPRESSION Using [ABBR]
 Iomode adxifs STRING_EXPRESSION Using [ABBR]
 Iomode adxium INTEGER_EXPRESSION Using [ABBR]
```

* `STRING_EXPRESSION` is an expression that returns a string value.
* `INTEGER_EXPRESSION` is an expression that returns an integer value.
* [`ABBR`] is the abbreviation used by [Openi](4gl_openi.html), [Openo](4gl_openo.html) or [Openio](4gl_openio.html).

# Examples

```
 # Read a file with CR+LF separator in ascii format
 # convert it in a file with LF separators in UTF8 format
 Subprog CONVERT (FILE_IN, FILE_OUT)
 Value Char FILE_IN(), FILE_OUT()

 Local Char LINE(250)

# Open the files
 Openi FILE_IN Using [IN]
 Openo FILE_OUT,0 Using [OUT]

# Set the parameters
 Iomode adxium 50                Using [IN]  : # ascii
 Iomode adxium 0                 Using [OUT] : # UTF8
 Iomode adxifs ''                Using [IN]  : # no field separator
 Iomode adxifs ''                Using [OUT] : # no field separator
 Iomode adxirs chr$(13)+chr$(10) Using [IN]  : # CRLF
 Iomode adxirs chr$(10)          Using [OUT] : # LF

# Copy loop
 Repeat
   Rdseq LINE Using [IN]
   If fstat=0
     Wrseq LINE Using [OUT]
   Endif
 Until fstat=0
 If LINE<>"" : Wrseq LINE Using [OUT] : Endif

# Close files
 Openi Using [IN] 
 Openo Using [OUT] 
End
```

# Comments

When opening a file without an abbreviation, the setting of the parameters is done directly by assignment of [adxifs](4gl_adxifs.html), [adxirs](4gl_adxirs.html), and [adxium](4gl_adxium.html). In this case, the use of `Iomode` is not necessary.

# Errors

No associated errors.

# See also

[Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html), [adxifs](4gl_adxifs.html), [adxirs](4gl_adxirs.html), [adxium](4gl_adxium.html).

  

[Index](index.html)  [Home](getting-started_home.html)