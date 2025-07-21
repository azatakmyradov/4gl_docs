[Index](index.html)  [Home](getting-started_home.html)

Year

`year` returns the year number (1600 to 9999) from a date.

# Syntax

```
   year(DATE_EXPR)
```

* `DATE_EXPR` is an expression returning a date.

# Examples

```
   # What is the year number today?
    CURRENT_DAY = year(date$)

   # Which year was the "Bastille Day" ?
    LONG_AGO=day([14/07/1789]) : # 1789
```

# Description

`year` returns the day number of a valid date, including the century.

When the date is a null date ([0/0/0]), the function returns 0.

The type of result is [Integer](4gl_integer.html).

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The argument is not a date. |
| 56 | The date is incorrect. |

# See also

[day](4gl_day.html), [month](4gl_month.html), [week](4gl_week.html), [month$](4gl_month$.html), [day$](4gl_day$.html), [gdat$](4gl_gdat$.html), [dayn](4gl_day$.html), [nday](4gl_nday.html), [date$](4gl_date$.html), [datesyst](4gl_datesyst.html), [Date](4gl_date.html).

  

[Index](index.html)  [Home](getting-started_home.html)