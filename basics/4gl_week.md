[Index](index.html)  [Home](getting-started_home.html)

Week

`week` returns the day number (0 to 53) from a date.

# Syntax

```
   week(DATE_EXPR)
```

* `DATE_EXPR` is an expression returning a date.

# Examples

```
   # What is the week number today?
    CURRENT_WEEK = week(date$)

   # What week was the "Bastille Day" ?
    TWENTY_NINE=day([14/07/1789]) : # returns 29
```

# Description

`week` returns the week number of a valid date.

The type of result is [Integer](4gl_integer.html).

When the date is a null date ([0/0/0]), the function returns 0.

The weeks are numbered from 0 to 53. The calculation mode is the following:

* A week starts on Monday (day 1) and ends on Sunday (day 7).
* The first week of the year is the week that contains the first Thurday of the year. If the first day of the year is Friday, Saturday, or Sunday, a week numbered 0 exists from first of January until the first Sunday.

This method corresponds to the ISO 8601 norm, except that week 0 does not exist in the norm (the last week number of the previous year is used). If the ISO value of week must be returned, the following formula should be used:

```
# Iso week for MY_DATE
  ISO_WEEK=week(MY_DATE)+week(gdat$(31,12,year(MY_DATE)-1))*(week(MY_DATE)=0)
```

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The argument is not a date. |
| 56 | The date is incorrect. |

# See also

[month](4gl_month.html), [year](4gl_year.html), [month$](4gl_month$.html), [day](4gl_day.html), [day$](4gl_day$.html), [eomonth](4gl_eomonth.html), [gdat$](4gl_gdat$.html), [dayn](4gl_day$.html), [nday](4gl_nday.html), [date$](4gl_date$.html), [datesyst](4gl_datesyst.html), [Date](4gl_date.html).

  

[Index](index.html)  [Home](getting-started_home.html)