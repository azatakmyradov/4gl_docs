[Index](index.html)  [Home](getting-started_home.html)

Xgetchar

This function extracts the Nth character of a CHAR or CLOB variable. This function runs much faster than the usual functions such as `mid$` or `seg$` when managing large CLOB data.

# Syntax

```
EXTRACTED_CHARACTER=Xgetchar(CLOB_SOURCE,POSITION)
```

* **CLOB\_SOURCE** has been declared by using a `Clbfile` or a `Char` declaration.
* **POSITION** has been declared by using an `Integer` declaration.
* **EXTRACTED\_CHARACTER** has been declared by using a `Clbfile` or a `Char` declaration.

# Example

```
# Find the 10th character in a CLOB
Local Clbfile PI_CHAR(0)
Local Char CHAR10

  PI_CHAR=num$(pi) : # contains "3.14158265358979323846264338328"
  CHAR10=Xgetchar(PI_CHAR,10) : # Returns "5"
```

  

[Index](index.html)  [Home](getting-started_home.html)