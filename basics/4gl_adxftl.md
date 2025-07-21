[Index](index.html)  [Home](getting-started_home.html)

Adxftl

`adxftl` is a variable used to set a read grouping factor in a number of records.

This information is managed by the [For](4gl_for.html) instruction to optimize the database access time.

# Syntax

```
adxftl
```

The method `adxftl` functions as follows:

* When its value is 1 or less, the instruction [For](4gl_for.html) works without grouping.
* When its value is equal to N greater than 1, the instruction [For](4gl_for.html) transfers blocks of N records from the database.

When a [Read](4gl_read.html) loop is executed with record-grouping, the number of back and forth movements between the database and the engine are reduced.

You should avoid [Read](4gl_read.html) operations within a [For](4gl_for.html) loop to keep the full benefit of this optimization. If the [Read](4gl_read.html) is done on tables that are linked to the main table inwhich the [For](4gl_for.html) is performed, it is possible to use a [Link](4gl_link.html) instruction that has good performances especially if the join is a strict join (with the ~= operator).

In most cases, a recommended value for `adxftl` is 10, which gives a good optimization of the read operations without creating an overhead when reading small tables.

The engine does not carry out any read optimizing on tables including CLOBs or BLOBs.

# Example

```
  # Recommended value
  adxftl=10
```

# See also

[For](4gl_for.html), [Read](4gl_read.html), [adxwrb](4gl_adxwrb.html).

  

[Index](index.html)  [Home](getting-started_home.html)