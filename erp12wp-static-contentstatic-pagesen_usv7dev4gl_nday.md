[Index](index.html)  [Home](getting-started_home.html)

Nday$

`nday$` returns a date from the number of days between the [1/1/1600] and the date.

# Syntax

```
   nday$(EXP_NUM)
```

* `EXP_NUM` is an expression returning an integer value.

# Examples

```
  # What is the date that corresponds to the 150,000th day since 1/1/1600 ?
  Local Date N_DATE1, N_DATE2
  N_DATE1 = nday$(150000)
  N_DATE2 = [1/1/1600]+150000
  # N_DATE1 and N_DATE2 have the same value (equal to [08/09/2010]).
```

# Description

`nday$` transforms a number of days in a date. The type of result is [Date](4gl_date.html).

`nday$(EXPR_NUM)` can be replaced by `[1/1/1600]+EXPR_NUM`.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | The argument is not an integer. |
| 56 | The resulting date is incorrect (EXPR\_NUM not in [-1,3068036] range). |

# See also

[day](4gl_day.html), [year](4gl_year.html), [month](4gl_month.html), [month$](4gl_month$.html), [day$](4gl_day$.html), [gdat$](4gl_gdat$.html), [dayn](4gl_day$.html), [nday](4gl_nday.html), [date$](4gl_date$.html), [datesyst](4gl_datesyst.html), [Date](4gl_date.html).

  

[Index](index.html)  [Home](getting-started_home.html)