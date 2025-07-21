[Index](index.html)  [Home](getting-started_home.html)

Eomonth

`eomonth` returns the date of the last day of the month in the year for the date given in the parameter.

# Syntax

```
   eomonth(DATE_EXPR)
```

* `DATE_EXPR` is an expression returning a date value.

# Examples

```
  # Last date of the current month
  Local Date LAST_DATE
  LAST_DATE=eomonth(date$)

  # Returns [31/1/2013]
  Local Date LAST_JANUARY
  LAST_JANUARY=eomonth([5/1/2013])
```

# Description

`eomonth` returns the last day of a month for the date given as a parameter. The type of result is [Date](4gl_date.html).

When the date is a null date ([0/0/0]), the function returns a null date.

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The argument is not a date. |
| 56 | Not valid date. |

# See also

[day](4gl_day.html), [month$](4gl_month$.html), [month](4gl_month.html), [year](4gl_year.html), [day$](4gl_day$.html), [nday](4gl_nday.html), [date$](4gl_date$.html), [datesyst](4gl_datesyst.html), [gdat$](4gl_gdat$.html), [Date](4gl_date.html).

  

[Index](index.html)  [Home](getting-started_home.html)