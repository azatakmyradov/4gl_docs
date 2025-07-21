[Index](index.html)  [Home](getting-started_home.html)

Format$

`format$` is a function that formats a value to return a formatted string value.

# Syntax

```
   format$(STRING_EXPR,EXPR)
```

* `STRING_EXPR` is a string expression giving the format used.
* `EXPR` is the expression giving the value to be formatted.

# Examples

```
   LETTER_SENTENCE = format$("D:[Created in Paris, ]9M[ ]2D[, ]YYYY", date$)
   CHTOTAL = format$("N3Z:[USD]12.2", sum(AMOUNTS))
```

# Description

`format$` returns the value defined by `EXPR` formatted as a string value according to the format defined by `STRING_EXPR`.

The result has a [Char](4gl_char.html) type.

# Syntaxes available for a format

A format is a character string that has two segments separated by a colon:

* The first segment starts with a string that defines the type of expression, and can be followed by additional characters representing formatting options.
* The second segment is the formatting string.

## Data types

The data types available are the following:

* **K** defines a character string format.
* **N** defines a number format.
* **D** defines a date format.
* **LAnnn**, where ***nnn*** is a number, defines a local menu format (***nnn*** being the local menu ID).

## Options

Additional options can be present:

| Applicable format type | Option | Description | Example | Result (spaces displayed ~) |
| --- | --- | --- | --- | --- |
| All | z | When the expression is null or empty, spaces are returned even for the embedded comments. | format$("N:9.2[ Euros]",0) format$("Nz:9.2[ Euros]",0) | "~~~~~~~~ 0.00~Euros" "~~~~~~~~~~~~~~~~~" |
| B | Replace the comments in the format by spaces. | format$("NB:9.2[ Euros]",3.14) | "~~~~~~~~3~14~~~~~~" |
 **String formats** | v | Suppression of spaces. Must be followed by a number (0 to 5) that corresponds to the option sent to the [vireblc](../4gl/vireblc.md) function used. **Note: **This is the only case where the resulting string can be shorter than the length given by the format.**** | format$("Kv2:15X","~~ABC~DEF~~") | "ABC~DEF" || A | Disables the uppercase/lowercase transformation and considers that a character with the wrong case is invalid. | format$("KA:4A","abcd") format$("K:4A","abcd") | "~~~~" "ABCD" |
| **Numeric formats** **Note:** The decimal separator is given by the 4th character of the variable [adxsca](../4gl/adxsca.md). | D | Display the sign at the end of the number. | format$("ND:5.2",-pi) format$("ND:5.2",pi) | "~~~~3.14-" "~~~~3.14" |
| + | Displays only the positive numbers (displays 0 if the number is negative). | format$("N+:5.2",1.5) format$("N+:5.2",-1.5) | "~~~~1.50" "~~~~0.00" |
| - | Displays the sign even if the number is positive. | format$("ND-:5.2",-pi) format$("ND-:5.2",pi) format$("N-:5.2",pi) format$("N-:5.2",pi) | "~~~~3.14-" "~~~~3.14+" "~~~-3.14" "~~~+3.14" |
| \* | Padding of numbers with a character defined by the 6th character of [adxsca](../4gl/adxsca.md) (usually the asterisk). | format$("N\*:5.2",-pi) format$("N\*:5.2",pi) | "\*\*\*-3.14" "\*\*\*\*3.14" |
| 0 | Padding of numbers with zeros. | format$("N0:5.2",pi). | "00003.14" |
| 3 | The digits before the decimal separators are grouped by 3. The character used to separate the groups of digits is the 3rd character of the system variable [adxsca](../4gl/adxsca.md). | format$("N3:8.2",10^6\*pi) | "~3,141,592.65" (If the separator is a comma) |
 **Note:** If the number has more significant decimals than the number given in the format, the digits in excess are not displayed; if the number of digits before the decimal separator is too big, the digits are replaced by an "overflow" character (the 5th character of [adxsca](../4gl/adxsca.md)). For example, format$("N:5.2", 10000\*pi) will return "\*\*\*\*\*.\*\*". | | | || **Date formats** | Z | Null dates authorized. | format$("DZ:DD[/]MM[/]YY",[0/0/0]) | "~~/~~/~~" |
| **Local menu formats** |  | Local menu description. | format$("LA14:20X",1) | "Supervisor~~" |

## Formatting string

This string includes the character used to display the string and embedded comments.

The comments can be everywhere in the string. They are delimited by square brackets. For example:

* `format$("D:[The ]DD[th Of ]MMMMMMMMM[, ]YYYY",[5/12/2013])` will return "The 5th Of December, 2013".

Every character of the formatting string corresponds to a position. Numbers can be given to repeat a position. For example, "3X5A" is equivalent to "XXXAAAAA".  
The formatting characters define the set of characters allowed at the formatting place. For example, '#' represents a digit, and 'X' any character. The following table provides the corresponding value:

Code | Usable with | Corresponds to || X | K formats | Any printable character. |
| # | K or N formats | Digit (0 to 9). The default type if a repetition factor is followed by ".". For example, "5.2" is equivalent to 5#.2# |
| . | N formats | Decimal placeholder. |
| F | N formats | Floating number. For example, format$("N:7F",pi) will return "3.14159". |
| A | K formats | Uppercase character. Lowercase are transformed except if the A option has been set. |
| a | K formats | Lowercase character. Uppercase are transformed except if the A option has been set. |
| L | K formats | Letters (a-Z, A-Z). |
| B | K formats | Uppercase character or digits. Lowercase are transformed except if the A option has been set. |
| b | K formats | Lowercase character or digits. Uppercase are transformed except if the A option has been set. |
| C | K formats | Letters (a-Z, A-Z) or digits. |
| H | K formats | Hexadecimal digits (0-8-9,A-F). |
| D | D formats | Day of a date. If more than two positions are given, the name of the day is displayed. |
| M | D formats | Month of a date. If two positions are given, the number of the month (01 to 12) is returned. If three positions are given, the three characters English abbreviation of the month is returned. If more than three positions are given, the name of the month, truncated to the number of positions, is returned. |
| Y | D formats | Year of a date. |
| h | D formats | Hour. |
| m | D formats | Minutes. |
| s | D formats | Seconds. |

Additional format position types can be defined with the variables [adxtuc](4gl_adxtuc.html), [adxtut](4gl_adxtut.html), and [adxtul](4gl_adxtul.html).

## Comments

* The ' **#** ' and ' **F** ' codes are usable with ' **K** ' types only if the string to be displayed contains only digits. For example, `format$("K:10#","3.141592") will return "~~~~~~~~~~" (10 spaces), because the ' **.** ' is not a digit.
* When a value does not match a format, the result is a string filled with spaces.
* For the dates, some standard formats exist, linked to the current connection language. They are coded "DD1", "DD2", "DD3", and "DD4". For example, the order and the language depend on the locale parameters:
  + format$("DD1",[1/1/2013]) will return "01/01".
  + format$("DD2",[1/1/2013]) will return "01/01/2013".
  + format$("DD3",[1/1/2013]) will return "01 January 2013".
  + format$("DD4",[1/1/2013]) will return "01 January 2013 15:20".
  + format$("DD5",[1/1/2013]) will return "01 January 2013 15:20:45".

# Deprecated options

"KT" and "KTD" type formats (recognition of X3 keywords, forbid X3 keywords in a string) are deprecated.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a string. |

# See also

[adxsca](4gl_adxsca.html), [adxtut](4gl_adxtut.html), [adxtul](4gl_adxtul.html), [adxtuc](4gl_adxtuc.html).

  

[Index](index.html)  [Home](getting-started_home.html)