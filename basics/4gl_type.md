[Index](index.html)  [Home](getting-started_home.html)

Type

`type` returns an integer value representing the data type of a variable.

# Syntax

```
type(VARIA)
```

* `VARIA` is a Sage X3 variable.

| Type of variable | Value returned | Declaration keyword used for this type |
| --- | --- | --- |
| Variable that does not exist | -1 | none |
| Tiny integer in (0,255) range | 1 | [Tinyint](4gl_tinyint.html) |
| Short integer in (-32768,32767) range | 2 | [Shortint](4gl_shortint.html) |
| Date in [1/1/1600], [31/12/9999] range | 3 | [Date](4gl_date.html) |
| Long integer (4 bytes) | 4 | [Integer](4gl_integer.html) |
| Floating point number(server dependent, and obsolete) | 5 | [Float](4gl_float.html) |
| Double floating point number(server dependent, and obsolete) | 6 | [Double](4gl_double.html) |
| Decimal number (32 digits precision) | 7 | [Decimal](4gl_decimal.html) |
| Character string of maximum length equal to L | 10+L | [Char](4gl_char.html) |
| Binary object (BLOB) | 522 | [Blbfile](4gl_blbfile.html) |
| Long character object (CLOB) | 523 | [Clbfile](4gl_clbfile.html) |
| Reference to an instance | 524 | [Instance](4gl_instance.html) |
| [Unique ID](4gl_glossary-uuid.html) | 525 | [Uuident](4gl_uuident.html) |
| Date time | 526 | [Datetime](4gl_datetime.html) |

# Example

```
# This function  returns a string describing the variable sent and its contents
Funprog FORMATTED_VALUE(VARIA)
Local Integer TYP

  TYP=type(VARIA)
  Case TYP:
    When -1: End "The variable doesn't exist"
    When 1 : End "Tiny integer"-format$("N:3#",VARIA)
    When 2 : End "Short integer"-format$("N:6#",VARIA)
    When 3 : End "Date"-format$("D:4Y[-]2M[-]2D",VARIA)
    When 4 : End "Long integer"-format$("N:11#",VARIA)
    When 5 : End "Floating number"-format$("N:12F",VARIA)
    When 6 : End "Double Floating number"-format$("N:12F",VARIA)
    When 7 : End "Decimal"-format$("N:32F",VARIA)
    When 522 : End "Binary object"
    When 523 : If len(VARIA)<100 : End "Long string of"-num$(len(VARIA))-"characters:"+left$(varia,100)
               Else End "(long string of"-num$(len(VARIA))-"characters starting with:"+left$(VARIA,20)+"..."
               Endif
    When 524 : If VARIA=NULL 
                 End "Null instance reference"
               Else
                 End "Instance of "+VARIA.Objecttype
               Endif
    When 525 : End "UUID"-num$(VARIA)
    When 526 : End "Date time"-num$(VARIA)
    When Default : If TYP>10 and TYP<266
                     End "String of"-num$(TYP-10)-"characters maximum with a length of"-num$(len(VARIA))
&                        +string$(len(VARIA)<=20,":"-VARIA)+string$(len(VARIA)>20," starting with:"-left$(VARIA,20)+"...")
                   Endif
  Endcase
End "Unknown type"
```

# Comment

A common test used to verify that a variable exists is done by the following condition:

```
  If type(VARIA)>0
     # The variable exists
  Else
     # The variable doesn't exist
  Endif
```

# See also

[Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Date](4gl_date.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)