[Index](index.html)  [Home](getting-started_home.html)

Gdat$

`gdat$` returns a date from a day, month, and year.

# Syntax

```
   gdat$(EXPR_DAY,EXPR_MONTH,EXPR_YEAR)
```

* `EXPR_DAY`, `EXPR_MONTH`, and `EXPR_YEAR` are integer expressions returning the day, month, and year number.
* `EXPR_YEAR` must be in the [1600,9999] range, or in the [0,99] range. The pivot date used to determine the century is given by [adxdcs](4gl_adxdcs.html)).

# Examples

```
   # Let's compute the date in 6 month
    DATE_6M = gdat$(day(date$), month(date$)+6, year(date$))
   # The formula is equivalent to :
    DATE_6M = addmonth(date$,6)

   # Let's find the last day of the previous month
    LAST_MONTH_DAY = gdat$(0, month(date$), year(date$))
   # The formula is equivalent to :
    LAST_MONTH_DAY = eomonth(gdat$(1, month(date$)-1, year(date$)))

   # How many days in the current month?
    DAYS_NB = day(gdat$(0, month(date$)+1, year(date$)))
   # The formula is equivalent to :
    DAYS_NB = day(eomonth(date$))
```

# Description

`gdat$` calculates a date from its three components. If a month out of the [1,12] range is given, the month is recalculated on modulo 12 basis and the year is adjusted accordingly. The same adjustment is done for days if a negative day number or a number over the maximum day number of the month is given.

If the year is two digits, the [adxdcs](4gl_adxdcs.html) value is used as a pivot value to define a century. The only exception is `gdat$(0,0,0)`, which returns the null date.

The result has a [Date](4gl_date.html) type.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | At least one of the arguments is not numeric. |
| 56 | Invalid date. |

# See also

[day](4gl_day.html), [day$](4gl_day$.html), [month](4gl_month.html), [month$](4gl_month$.html), [year](4gl_year.html), [dayn](4gl_day$.html), [nday](4gl_nday.html), [date$](4gl_date$.html), [datesyst](4gl_datesyst.html), [Date](4gl_date.html), [eomonth](4gl_eomonth.html), [adxdcs](4gl_adxdcs.html).

  

[Index](index.html)  [Home](getting-started_home.html)