[Index](index.html)  [Home](getting-started_home.html)

Strdecode

This function transforms a UTF8 or ASCII encoded character string (based on the parameter given) into a UCS2 format. It returns the number of character found in the destination.

# Syntax

```
STRING_LENGTH=StrDecode(STRING_SOURCE,STRING_DESTINATION,TYPE)
```

* "STRING\_SOURCE" and "STRING\_DESTINATION" have been declared by using an `Clbfile` or a `Char` declaration.
* "TYPE" has been declared by using an `Integer` declaration.
* The possible values for "TYPE" are:
  + **50 :** ascii to UCS2 transformation.
  + **122 :** UCS2 to UCS2 transformation (void transformation).
  + **0 :** UTF8 to UCS2 transformation.

Any other given value will trigger an error.

# Example

```
# Let's transcode a character string from one format to another
# SOURCE_FORMAT should be "ASCII", "UCS2",or "UTF8"
# DESTINATION_FORMAT should be "ASCII", "UCS2",or "UTF8"
Funprog TRANSCODE(SOURCE, SOURCE_FORMAT, DESTINATION,DESTINATION_FORMAT)
Const Clbfile SOURCE
Variable ClbFile DESTINATION
Const Char SOURCE_FORMAT,DESTINATION_FORMAT
Local Integer I

# Let's first look if the format is the same
  If toupper(SOURCE_FORMAT)=toupper(DESTINATION_FORMAT)
    DESTINATION=SOURCE
    End len(DESTINATION)
  Endif

# Now let's use one or two transcodings
  Case toupper(SOURCE_FORMAT)-toupper(DESTINATION_FORMAT)
    When "ASCII UCS2" : I=strDecode(SOURCE,DESTINATION,50)
    When "UTF8 UCS2"  : I=strDecode(SOURCE,DESTINATION,0)
    When "UCS2 ASCII" : I=strEncode(SOURCE,DESTINATION,50)
    When "UCS2 UTF8"  : I=strEncode(SOURCE,DESTINATION,0)
    When Default      : Local Integer ISIZE
                        ISIZE=max(0,int(1+log(max(1,len(SOURCE)+1))/log(2))-9)
                        Local Clbfile INTERMEDIATE(ISIZE)
                        Case toupper(SOURCE_FORMAT)-toupper(DESTINATION_FORMAT)
                           When "ASCII UTF8" : I=strDecode(SOURCE,INTERMEDIATE,50)
                                               I=strEncode(INTERMEDIATE,DESTINATION,0)
                           When "UTF8 ASCII" : I=strDecode(SOURCE,INTERMEDIATE,0)
                                               I=strEncode(INTERMEDIATE,DESTINATION,50)
                           When Default      : # Unknown conversion
                                               End -1
                         Endcase
  Endcase
End I
```

# See also

[B64Decode](4gl_b64decode.html), [B64Encode](4gl_b64encode.html), [strEncode](4gl_strencode.html)

  

[Index](index.html)  [Home](getting-started_home.html)