[Index](index.html)  [Home](getting-started_home.html)

Lobsize

`lobsize` returns the size (in bytes) used for the storage of BLOB or CLOB variable.

# Syntax

```
   lobsize(BLOB_CLOB)
```

* `BLOB_CLOB` is a CLOB or BLOB variable.

# Examples

```
   # How much space spent for a clob?
   Local Clbfile MY_CLOB(0)
   MY_SIZE=lobsize(MY_CLOB) : # Returns 1016 (stores 508 characters)
   My_CLOB=string$(50,space$(10))+space$(9) : # Assign a 509 character string
   MY_SIZE=lobsize(MY_CLOB) : # Returns 66550 (MY_CLOB has been automatically enlarged)

   Local Clbfile MY_CLOB(1)
   MY_SIZE=lobsize(MY_CLOB) : # Returns 2040

# Here I is an integer value between 0 and 10
   Local Clbfile MY_CLOB(I)
   MY_SIZE=lobsize(MY_CLOB) : # Returns 2^(10+I)-8
```

# Description

`lobsize` returns the size (in bytes) used to store a BLOB or a CLOB variable. The type of result is [Integer](4gl_integer.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a CLOB or BLOB variable. |

# See also

[len](4gl_len.html).

  

[Index](index.html)  [Home](getting-started_home.html)