[Index](index.html)  [Home](getting-started_home.html)

B64decode

This function decodes a base 64 string into a BLOB (Binary Large Object). It returns the number of bytes written to the BLOB. An error 26 is displayed if the input is invalid.

# Syntax

```
LENGTH=B64Decode(SOURCE_CLOB, DEST_BLOB)
```

* `DEST_BLOB` has type `Blbfile`.
* `CLOB_SOURCE` has type `Clbfile` or `Char`.
* `LENGTH` has type `Integer`.

# Examples

```
# Decode a base 64 CLOB into a BLOB
# If an error occurs, return -1
Funprog DECODE(SOURCE, DESTINATION)
Const Clbfile SOURCE
Variable BlbFile DESTINATION
Local Integer I
  Onerrgo ERROR_FOUND
  I=B64Decode(SOURCE,DESTINATION)
  End I
$ERROR_FOUND
  End -1
```

# See also

[b64Encode](4gl_b64encode.html), [strEncode](4gl_strencode.html), [strDecode](4gl_strdecode.html)

  

[Index](index.html)  [Home](getting-started_home.html)