[Index](index.html)  [Home](getting-started_home.html)

Addmonth

`addmonth` allows you to add a given number of months to a date.

# Syntax

```
   addmonth( DATE_EXPR, INTEGER_EXPR )
```

* `DATE_EXPR` is an expression returning a date.
* `INTEGER_EXPR` is an integer expression returning a number of the month, which can be positive or negative.

# Examples

```
   # Previous month
    PREV_MONTH = addmonth(date$,-1)

   # Next year
    NEXT_YEAR = addmonth(date$,12)

   # End of month
    NEXT_MONTH = addmonth([31/01/2013],1) : # Returns [28/2/2013]

   # What will be the day in one month ?
    DAY_NAME = day$(addmonth(date$,1))

   # Due date computation
    DUE_DATE = addmonth(gdat$(INVOICE_DAY,INVOICE_MONTH,INVOICE_YEAR),DELAY)
```

# Description

The function `addmonth` adds a number of months to a date. The number of months can be positive or negative and be greater than 12 (the year will be increased if necessary).

If the date value has a day number that is over the number of days for the result month, the last day of the month is returned.

The type of result is [Date](4gl_date.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | One of the arguments has an incorrect type. |
| 56 | Incorrect date. |

# See also

[day](4gl_day.html), [day$](4gl_day$.html), [month$](4gl_month$.html), [year](4gl_year.html), [dayn](4gl_day$.html), [nday](4gl_nday.html), [nday$](4gl_nday$.html), [date$](4gl_date$.html), [datesyst](4gl_datesyst.html), [gdat$](4gl_gdat$.html), [eomonth](4gl_eomonth.html).

  

[Index](index.html)  [Home](getting-started_home.html)