[Index](index.html)  [Home](getting-started_home.html)

Then

`Then` is a keyword that can be used between the condition in the [If](4gl_if.html) statement and the [next](4gl_next.html) statement. It is completely optional: an instruction separator such as the colon or new line is also available.

# Example

```
If I=1 Then J=2 Else J=3 : Endif
```

\*\*can be replaced by:\*\*

```
If I=1 : J=2 Else J=3 : Endif
```

\*\*or\*\*

```
If I=1
  J=2
Else J=3
Endif
```

  

[Index](index.html)  [Home](getting-started_home.html)