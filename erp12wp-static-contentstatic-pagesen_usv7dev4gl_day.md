[Index](index.html)  [Home](getting-started_home.html)

Day$

`day$` returns a string that contains the name of the day (in the week) that corresponds to the date given as an argument. The result is given in the current connection language.

# Syntax

```
   day$(DATE_EXPRESSION)
   day$(INTEGER_EXPRESSION)
```

* `DATE_EXPRESSION` is an expression that returns a date value.
* `INTEGER_EXPRESSION` is an expression that returns an integer value.

# Examples

```
  # Which day was the Bastille Day?
  TUESDAY=day$([14/07/1789]) : # TUESDAY contains "Tuesday" if connected in English, "Mardi" if connected in French

  # Let's fill a string with the date in a sentence
  MYDATE="Today we are"-day$(date$)-month$(date$)-num$(day(date$))+","-num$(year(date$))
  # Returns a text like "Today we are Monday December 9, 2013"
```

# Description

`day$` returns the name of the day from a valid date. If a numeric argument is given, the result is the name of the day with the following:

1=Monday, 2=Tuesday... 7=Sunday.

If the number is not in the right [1,7] range, a 7 modulus calculation is done to bring it to the right range. For example, `day$(9)` is equal to `day$(2)`.

The result type is [Char](4gl_char.html).

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The argument is not a number. |

# See also

[day](4gl_day.html), [month$](4gl_month$.html), [month](4gl_month.html), [year](4gl_year.html), [dayn](4gl_day$.html), [nday](4gl_nday.html), [date$](4gl_date$.html), [Date](4gl_date.html).

  

[Index](index.html)  [Home](getting-started_home.html)