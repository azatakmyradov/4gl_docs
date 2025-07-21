[Index](index.html)  [Home](getting-started_home.html)

Strencode

This function transforms a UCS2 encoded character string into another format that is given by an additional parameter. It returns the number of character found in the destination.

# Syntax

```
CODECODE CODEsh
STRING_LENGTH=StrEncode(STRING_SOURCE,VAR_DESTINATION,TYPE)
```

* "STRING\_SOURCE" has been declared by using a `Clbfile` or a `Char` declaration.
* "VAR\_DESTINATION" have been declared by using a `Clbfile`, a `Blbfile` or a `Char` declaration.
* "TYPE" has been declared by using an `Integer` declaration.
* The possible values for "TYPE" are:
  + **50 :** ascii transformation.
  + **122 :** UCS2 transformation.
  + **0 :** UTF8 transformation.

Any other given value will trigger an error.

# Example

```
CODECODE CODEsh
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

# Let's create a blob containing an ascii text
# The Clbfile text is always stoed in memory in UCS2 format
Local Clbfile TEXT(0)
Local Blbfile BLOB_TEXT(0)
Local Integer I
TEXT="This is a text"+chr$(10)+"with several lines"+chr$(10)+"including accents"+"I asked for an 'Ã  la carte menu'"
I=strEncode(TEXT,BLOB_TEXT,50)
```

# See also

[B64Decode](4gl_b64decode.html), [B64Encode](4gl_b64encode.html), [strDecode](4gl_strdecode.html)

  

[Index](index.html)  [Home](getting-started_home.html)