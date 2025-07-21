[Index](index.html)  [Home](getting-started_home.html)

Currlen

`currlen` is a numeric variable in the [G] class associated with a table declared by the [File](4gl_file.html) instruction. It can be assigned to define the number of key components used for a [Read](4gl_read.html) operation when the key is not mentioned and defined by `currind`.

# Syntax

```
[G:ABV]currlen
```

* `ABV` is the abbreviation used to open the table.

# Example

```
# The MYTABLE table has several indexes.
# The first one is an index MY0 composed by 3 components (string CODE, date MYDATE, and value NUMVAL).

Local File MYTABLE [MYT]

# The following instructions:
  [G:MYT]currind=1 : [G:MYT]currlen=1 : Read [MYT]="ABC"

# Are equivalent to:
  Read [MYT]MY0(1)="ABC"

# The following instructions:
  [G:MYT]currind=1 : [G:MYT]currlen=2 : Read [MYT]="ABC" ; date$

# Are equivalent to:
  Read [MYT]MY0(2)="ABC" ; date$
```

# See also

[File](4gl_file.html), [Read](4gl_read.html), [For](4gl_for.html), [currind](4gl_currind.html).

  

[Index](index.html)  [Home](getting-started_home.html)