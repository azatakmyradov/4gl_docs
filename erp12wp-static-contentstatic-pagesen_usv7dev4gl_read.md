[Index](index.html)  [Home](getting-started_home.html)

Read

Use `Read` to get data from a table or a join through a SQL select instruction based on the value of an index key previously defined or a temporary index.

# Syntax

```
   Read [CLASS] KEY READ_MODE KEYVAL_LIST
```

* `CLASS` is the abbreviation of the table or join in which the read is done. The `[CLASS]`element is optional.
* `KEY` is the optional description of the key defined on the table or the join. If not given, the default key defined by [G][currind](4gl_currind.html) value is used. It has one of the following formats:
  + `KEYNAME`: Where `KEYNAME` is the name of a key that is defined for the table, or that comes from an [Order By](4gl_order-by.html) Key `KEYNAME`=... clause.
  + `KEYNAME`(`INDEX_VALUE`): Where `INDEX_VALUE` is an expression that gives the number of components of the key (all by default) used in conjunction with the `READ_MODE`.
* `KEYVAL_LIST` is an optional list of `KEYVAL` expressions separated by semicolons. Every expression is evaluated and used as a condition on the different components of the key. The data type of the expressions must match with the data types of the corresponding key segments.
* `READ_MODE` is also optional. It is one of the keywords given by the next array. `READ_MODE` is mandatory if a `KEYVAL` segment is given. Although `KEYVAL` is never mandatory, only some `READ_MODE` accept key values. This is summarized by the [read mode table](#readmode).

# Examples

```
   #  A single read operation. The table is BPCUSTOMER [BPC], the may key is BPC0 (one segment of key)
   Read [BPC]BPC0="JOHNDOE" : # Reads a single record

   # Read the line #1000 of a sales order (table SORDERP [SOP], index SOP3 (order number/order line))
   Local File SORDERP [SOP]
   Read [SOP]SOP3=[L]MYORDER;1000

   # Read the first line of a sales order (table SORDERP [SOP], index SOP3 (order number/order line))
   Local File SORDERP [SOP]
   Read [SOP]SOP3(2)>=[L]MYORDER;0

   # Read the first line of a sales order
   Local File SORDERP [SOP]
   Filter [SOP] Where SOHNUM=[L]MYORDER
   Read [SOP]SOP3 First

   # Read the last line of the last sales order before the current sales order
   Local File SORDERP [SOP]
   Read [SOP]SOP3(2)>=[L]MYORDER;0 : # The first line of the current sales order is online
   Read [SOP]SOP3 Prev : # The previous line is now online
```

# Description and comments

Use `Read` to perform read operation on tables or joins according to various modes listed on the grid below. If no key value is specified for the modes that require one ( **<**, **>**, **<=**, **>=**, **=** ), the current value of the variables of class [F] corresponding to the file is used.

| Read mode | Is a value possible? | Data read |
| --- | --- | --- |
| ``` First ``` | no | The first line in the index order. |
| ``` Last ``` | no | The last line in the index order. |
| ``` Prev ``` | no | The previous line, compared to the last read line, in the index order. |
| ``` Next ``` | no | The next line, compared to the last read line, in the index order. |
| ``` Curr ``` | no | The current line (the last read line). |
| ``` < ``` | yes | The last line, in index order, that has a key value strictly less than the given value. |
| ``` <= ``` | yes | The last line, in index order, that has a key value less than or equal to the given value. |
| ``` = ``` | yes | A line that has a key value equal to the given value. |
| ``` >= ``` | yes | The first line, in index order, that has a key value greater than or equal to the given value. |
| ``` > ``` | yes | The first line, in index order, that has a key value strictly greater to the given value. |

The keys that can be used in `Read` are:

* When reading a table using the abbreviation defined in the [File](4gl_file.html) instruction (explicitly or implicitly):
  + The key defined by the [Order By](4gl_order-by.html) clause of the [File](4gl_file.html) or [Filter](4gl_filter.html).
  + One of the keys defined in the table definition.
* When reading a join with the link ([Link](4gl_link.html)) abbreviation:
  + The key defined by the [Order By](4gl_order-by.html) clause of the [File](4gl_file.html) or [Filter](4gl_filter.html).
  + The key defined by the [Order By](4gl_order-by.html) clause of the [File](4gl_file.html) of the main table (if there is one).
  + One of the keys defined in the main file definition.

The default values when elements are omitted in the Read syntax are:  
\* For the abbreviation of the table, the table used by default is the first in the default table list. Thus, it is the table defined as [Default](4gl_default.html) [File](4gl_file.html) (the first declared in the last [File](4gl_file.html) instruction by default). The same default value is used if the abbreviation given is `[F]`.   
\* For the key name, the key used by default is the current key. Its number is provided by the [currind](4gl_currind.html) system variable.  
\* For the read mode that is omitted, the default read mode is the `Curr` mode.  
\* For key segment values that are omitted when necessary, the current [F] class values are taken.

The [fstat](4gl_fstat.html) variable returns a status after any database operation. The following values can be returned after `Read`:

| fstat value | Description |
| --- | --- |
| 0 | Read operation was successful. |
| 2 | When using **<=** or **>=** mode, the line found does not correspond to the exact value of key given but it is strictly greater or smaller. |
| 4 | When using **Prev** or **Next** mode, no line was found. |
| 5 | When using **<**, **<=**, **=**, **>=**, **>=** or **Curr** mode, no line was found. |

After a successful read (for example, if [fstat](4gl_fstat.html) is 0 or equal to 2), the variables of the class [F] corresponding to the table contain the values of the recording read. This line becomes the current recording of the file. Otherwise, nothing is modified.

## Notes:

### Partial Keys

Reading a line, by giving a partial key components list value, sets the [G][currlen](4gl_currlen.html) variable with the number of key components used during this read operation. Note that another read done without details on the key reuses the same component. To read again with the whole key component, you can either give a complete syntax or set [currlen](4gl_currlen.html) to 0 (default value which means tat the whole key is used).

Strictly greater or strictly less takes into account the number of key component.

To illustrate these points, for a three-segment component key called MYKEY, the following value list is used:

| Line | Key component 1 | Key component 2 | Key component 3 |
| --- | --- | --- | --- |
| #1 | A | B | C |
| #2 | A | B | D |
| #3 | A | C | A |
| #4 | A | C | B |
| #5 | A | D | E |
| #6 | B | A | D |

Let's imagine the table class is empty (a [Raz](4gl_raz.html) operation has been done). The lines returned are the following, considering that MYKEY is a key that has 3 components comp\_1, comp\_2, comp\_3 (of course, the Read will return only one record, but a [For](4gl_for.html) after a [Filter](4gl_filter.html) including the read mode would return several lines):

| Read mode | Lines returned | SQL equivalent | Comment |
| --- | --- | --- | --- |
| MYKEY **First** | 1 | Select return first row according to the order by given | If no order by given in Read and File, first key is used by default |
| MYKEY(1)**>** "A" | 1 | select ... where comp\_1 >"A" |  |
| MYKEY(2)**>** "A" | 1 | select ... where comp\_1 >"A" | Even if 2 components of keys are specified, only the first one has a filtering constraint |
| MYKEY(2)**>** "A";"B" | 4 | select where  (comp\_1="A" and comp\_2>"B")  or (comp\_1>"A") | The first clause is indicating that the set of values such as "A";"C" and "A";"D" are included in the results and the second clause indicates any comp\_1>"A" is included, such as "B", "C", "D", etc. |
| MYKEY(3)**>** "A";"B" | 4 | select where (comp\_1="A" and comp\_2>"B") or (comp\_1>"A") | The same before no value is given for the third component. |
| MYKEY(3)**>** "A";"B";"C" | 5 | select where  (comp\_1="A" and comp\_2="B" and comp\_2>"C")  or (comp\_1="A" and comp\_2>"B")  or (comp\_1>"A") | This uses all 3 index components. In the first clause, values such as "A";"C";"anything", "A";"D";"anything" will be returned. From the second clause, all values such as "A";"B";"D", "A";"B";"E", etc. are returned |

### Performance considerations

`Read` is useful when a single line needs to be read. When several lines are accessed, the use of the [For](4gl_for.html) instruction is preferable for performance reasons:  
\* A `Read` instruction sends a SQL request and performs a "fetch operation" to get the data. If several read operations are performed, the analysis of the SQL request is costly.  
\* A `For` instruction sends a SQL request, and then performs several "fetch operations" when data is requested.

Some `Read` syntax orders make it necessary to browse nearly the entire table and is therefore costly. For example, the **>=** and **<=** modes on keys with several components. The table presented in the section about partial key emphasizes well this situation, that can bring to several request when "or" are used in whrere clauses. This is even the case for 2 components.

Let's consider this example, where MYKEY is a two-components (KEY1,KEY2) key:

`Read MYKEY >= value1;value2` reads two types of lines:

* Those with KEY1=value1 and KEY2 >= value2.
* Those with KEY1>value1, KEY2 having any value.

Very often, only the first line type is relevant for the development partner. The request also gets the second type, even if the fetch operation is done only on a line from the first set.

In that case, it is much quicker to execute:

```
Filter [ABV] Where KEY1=value1 & KEY2>= value2 Order by MYKEY
Read [ABV]CLE First
```

# Associated errors

| Error code | Description |
| --- | --- |
| 7 | The table has not been opened. |
| 8 | The number of key components exceeds the number of segments for the key. |
| 21 | The key does not exist. |
| 22 | Incorrect read mode. |

# See also

[Look](4gl_look.html), [Readlock](4gl_readlock.html), [File](4gl_file.html), [Link](4gl_link.html), [Filter](4gl_filter.html), [Columns](4gl_columns.html), [For](4gl_for.html), [Rewrite](4gl_rewrite.html), [RewriteByKey](4gl_rewritebykey.html), [Delete](4gl_delete.html), [DeleteByKey](4gl_deletebykey.html), [Update](4gl_update.html), [Look](4gl_look.html), [Write](4gl_write.html), [fstat](4gl_fstat.html), [currind](4gl_currind.html), [currlen](4gl_currlen.html).

  

[Index](index.html)  [Home](getting-started_home.html)