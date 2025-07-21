[Index](index.html)  [Home](getting-started_home.html)

Append

`Append` allows to concatenate a char or CLOB value to a char or CLOB variable.

# Syntax

```
  Append VAR1, EXPRESSION2
```

\* \*\*`VAR1`\*\* is a variable with one of the following syntaxes:
\* VARIABLE\_NAME
\* VARIABLE\_NAME (INDEX\_EXPRESSION\_LIST)
\* \*\*`EXPRESSION2`\*\* is an expression returning a string or a CLOB.
\* \*\*`INDEX\_EXPRESSION\_LIST`\*\* is a list of expressions returning an integer used when "VARIABLE\_NAME" corresponds to an array. It gives the current index in the array. The number of elements on the list must correspond to the number of dimensions of the array.

# Examples

```
  # Example 1
  Local Clbfile FIELD1
  Local Char FIELD2
  FIELD1="A"
  FIELD2="2"
  APPEND FIELD1, FIELD2
  # Now FIELD1 contains "A2"

  # Example 2
  Local Clbfile FIELD1
  Local Clbfile FIELD2
  FIELD1="A"
  FIELD2="2"
  APPEND FIELD1, FIELD2
  # Now FIELD1 contains "A2"

  # Example 3
  Local Char FIELD1
  FIELD1="A"
  APPEND FIELD, "2"
  # Now FIELD1 contains "A2"
```

# Description

`Append` allows to concatenate a string or CLOB value to an existing string or CLOB.

From a functional point of view, `Append A,B` is equivalent to **A+=B** if 'A' and 'B' are strings or CLOBs.

Execution is fast especially if you build long strings stored in CLOBs.

# Associated errors

None

# See also

[Clbfile](4gl_clbfile.html), [Char](4gl_char.html), [Schar](4gl_schar.html).

  

[Index](index.html)  [Home](getting-started_home.html)