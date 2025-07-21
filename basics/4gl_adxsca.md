[Index](index.html)  [Home](getting-started_home.html)

Adxsca

`adxsca` is an internal string variable that stores characters used by formatting functions.

# Comment

Most of the use cases of the characters in this string are now deprecated.  
The only remaining use case is [format$](4gl_format$.html), that uses:

* The thousands separator used for numbers (the 3rd character).
* The decimal separator used for decimal formatting (the 4th character).
* The overflow character used for decimal formatting when the number of digits before the separator exceeds the number of positions (the 5th character).
* The padding character used for decimal formatting when the "\*" option is used (the 6th character).

# Examples

```
Local Char THOU_SEP(1),DEC_SEP(1),OVER_CHAR(1),PADD_CHAR(1)

  THOU_SEP="," : DEC_SEP="." : OVER_CHAR="*" : PADD_CHAR="#" : Gosub SET_ADXSCA
  STRING1=format$("N3:8.4",1000*pi)       : # STRING1 contains "    3,141.5926"
  STRING2=format$("N3*:8.4",1000*pi)      : # STRING2 contains "####3,141.5926"
  STRING3=format$("N3:8.4",10^9*pi)       : # STRING3 contains "*********.****"

  THOU_SEP="." : DEC_SEP=" " : OVER_CHAR="!" : PADD_CHAR="*" : Gosub SET_ADXSCA
  STRING1=format$("N3:8.4",1000*pi)       : # STRING1 contains "    3 141,5926"
  STRING2=format$("N3*:8.4",1000*pi)      : # STRING2 contains "****3 141,5926"
  STRING3=format$("N3:8.4",10^9*pi)       : # STRING3 contains "!!!!!!!!!,!!!!"
  End

$SET_ADXSCA
  adxsca=left$(adxsca,2)+THOU_SEP+DEC_SEP+OVER_CHAR+PADD_CHAR+right$(adxsca,7)
Return
```

# See also

[format$](4gl_format$.html).

  

[Index](index.html)  [Home](getting-started_home.html)