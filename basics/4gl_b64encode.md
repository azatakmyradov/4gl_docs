[Index](index.html)  [Home](getting-started_home.html)

B64encode

This function encodes binary data stored in a BLOB (Binary Large Object) as a base 64 string. It returns the number of characters written to the string.

# Syntax

```
LENGTH=B64Encode(SOURCE_BLOB, DEST_CLOB)
```

* `SOURCE_BLOB` has type `Blbfile`.
* `DEST_CLOB` has type `Clbfile` or `Char`.
* `LENGTH` has type `Integer`.

# Example

```
# Write BLOB into a base 64 CLOB
Funprog DECODE(SOURCE, DESTINATION)
Const Blbfile SOURCE
Variable ClbFile DESTINATION
Local Integer I
  I=B64Encode(SOURCE,DESTINATION)
  End I
```

# See also

[b64Decode](4gl_b64decode.html), [strEncode](4gl_strencode.html), [strDecode](4gl_strdecode.html)

  

[Index](index.html)  [Home](getting-started_home.html)