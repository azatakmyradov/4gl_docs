[Index](index.html)  [Home](getting-started_home.html)

Chr$

`chr$` converts a numeric value into a string character having this value as a code.

# Syntax

```
   chr$(INTEGER_EXPR)
```

* `INTEGER_EXPR` is an integer expression with a value in the [0,65535] range.

# Examples

```
   # Let's get the latin upper case alphabet:
   Local Char ALPHABET(30)
   ALPHABET = sigma( I = 65, 90, chr$(I) )

   # Let's assign tab as fields separator and carriage return+line feed as record separator
   # in a script that reads an ascii file with the abbreviation [RD]
   Iomode adxifs chr$(9)           Using [RD]
   Iomode adxirs chr$(13)+chr$(10) Using [RD]
```

# Description

`chr$` returns a character with the UCS2 code corresponding to the argument. If the argument value is in [0,255] range, it corresponds to the ASCII table.

`chr$` is the reverse function of [ASCII](4gl_ascii.html).

When set to `chr$(0)`, `chr$` returns an empty string.

The result of this function has the [Char](4gl_char.html) type.

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The argument is not an integer number. |
| 55 | The argument value is not in the [0,65536] range. |

# See also

[ascii](4gl_ascii.html), [string$](4gl_string$.html), [adxium](4gl_adxium.html), [Iomode](4gl_iomode.html).

  

[Index](index.html)  [Home](getting-started_home.html)