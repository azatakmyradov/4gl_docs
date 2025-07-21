[Index](index.html)  [Home](getting-started_home.html)

Aweek

`aweek` returns the first day of a week number for the year.

# Syntax

```
  aweek(EXPR_WEEK,EXPR_YEAR)
```

* `EXPR_WEEK` is an integer expression that returns the week number.
* `EXPR_YEAR` is an integer expression that returns the year number between 1600 and 9999, or between 0 and 99.

# Examples

```
   # Let's give the date that corresponds to the first Wednesday of the current week.
    WEDN_DATE = aweek(37,year(date$))+2

   # Other examples
    DATE1=aweek(-1,2013) : # Corresponds to [17/12/2012]
    DATE2=aweek(0,16) : # Corresponds to [04/01/2016] if adxdcs is greater than 1916
```

# Description

The function `aweek` calculates the date of the first day (Monday) for a week number in a year. The type of the result is [Date](4gl_date.html).

The week is numbered from 0 to 53. The calculation mode follows the NF ISO 8601 norm and is as follows:

* A week starts on Monday (day 1) and ends on Sunday (day 7).
* The first week of a year is the week that contains the first Thursday of the year. If the first day of the year is a Friday, a Saturday, or a Sunday, a week numbered 0 exists that starts the first of January and ends the next Sunday.
* When the year is only two digits, the year used depends on the value of [adxdcs](4gl_adxdcs.html).
* If a negative value of the week is given, the calculation goes back to the previous week of the previous year.

# Associated errors

| Error | Description |
| --- | --- |
| 10 | The argument is not a string. |
| 56 | Incorrect data values (year not in the acceptable range). |

# See also

[Date](4gl_date.html), [week](4gl_week.html), [day](4gl_day.html), [day$](4gl_day$.html), [month](4gl_month.html), [year](4gl_year.html), [nday](4gl_nday.html), [nday$](4gl_nday$.html), [adxdcs](4gl_adxdcs.html).

  

[Index](index.html)  [Home](getting-started_home.html)