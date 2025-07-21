[Index](index.html)  [Home](getting-started_home.html)

Touuid

This keyword converts a canonical UUID string to its UUID value.

# Syntax

```
Touuid(str)
```

# Example

```
MYUUID=Touuid(â12345678-9abc-def0-1234-567890abcdefâ) : # Constant UUID (!!)
MYUUID=Touuid(CANONICAL_UUID) : # Transforms the string CANONICAL_UUID
```

# Comments

Use the [num$](../4gl/num$.md) function to transform from UUID to canonical string:

```
MYUUID=Touuid(num$(Getuuid))
```

Is equivalent to:

```
MYUUID=Getuuid
```

# See also

[UUID](4gl_glossary-uuid.html), [Uuident](4gl_uuident.html), [Nulluuid](4gl_nulluuid.html), [Getuuid](4gl_getuuid.html)

  

[Index](index.html)  [Home](getting-started_home.html)