[Index](index.html)  [Home](getting-started_home.html)

Month$

`month$` returns the month name in the current language from a date.

# Syntax

```
   month$(EXP_DATE)
```

* `EXP_DATE` is an expression returning a date.

# Examples

```
   # Returns "July" if connected in English
   Local Char JULY(20)
   JULY=month$([14/07/1789])

   # What is the current month name?
   Local Char CURR_MONTH(20)
   CURR_MONTH = month$(date$)
```

# Description

`month$` returns the month name from a date. The type of result is [Char](4gl_char.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not a date. |
| 56 | The date is incorrect. |

# See also

[day](4gl_day.html), [year](4gl_year.html), [month](4gl_month.html), [day$](4gl_day$.html), [gdat$](4gl_gdat$.html), [dayn](4gl_day$.html), [nday](4gl_nday.html), [nday$](4gl_nday$.html), [date$](4gl_date$.html), [datesyst](4gl_datesyst.html), [Date](4gl_date.html).

  

[Index](index.html)  [Home](getting-started_home.html)