[Index](index.html)  [Home](getting-started_home.html)

Nulluuid

This keyword represents the ***null*** UUID constant.

# Syntax

```
Nulluuid
```

# Example

`Nulluuid` is used in assignments and test expressions.

```
MY_UUID=Nulluuid : # Valid but null value
If MY_UUID=Nulluuid : MY_UUID=Getuuid : Endif : # Assign a UUID if it was a null one
```

# Comments

`Nulluuid` is equivalent to `Touuid(â00000000-0000-0000-0000-000000000000â)`.

# See also

[UUID](4gl_glossary-uuid.html), [Uuident](4gl_uuident.html), [Touuid](4gl_touuid.html), [Getuuid](4gl_getuuid.html).

  

[Index](index.html)  [Home](getting-started_home.html)