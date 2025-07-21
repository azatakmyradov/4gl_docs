[Index](index.html)  [Home](getting-started_home.html)

Time$

This function returns the current time, as given from the system, as a string using the `hh:mm:ss` format. This time is obtained from the process server and is the local time (in the timezone of the server).

# Syntax

```
time$
```

# Example

```
# First example: let's get my time in the process server time zone
Local Char MY_TIME(8)
MY_TIME=time$


# Second example: what is the time zone offset (in hours) of my process server?
Local Char MY_TIME(8), ZERO_TIME(8)
Local Integer OFFSET

  MY_TIME=time$: ZERO_TIME=mid$(num$(datetime$),12,8)
  OFFSET= 3600 * (val(left$(MY_TIME,2))-val(left$(ZERO_TIME,2)))
&       +   60 * (val(mid$(MY_TIME,4,2))-val(mid$(ZERO_TIME,4,2)))
&       +         val(mid$(MY_TIME,7,2))-val(mid$(ZERO_TIME,7,2))
  OFFSET=arr(OFFSET/3600,0.5) : # Let's take in account a one-second difference it the clock switched
```

# Comment

If you need to access the current time in UTC (in Greenwitch zone), the formula `mid$(num$(datetime$),12),8` returns the right value in the format `hh:mm:ss`.

# See also

[Date](4gl_date.html), [DateTime definition](4gl_glossary-datetime.html), [Datetime$](4gl_datetime$.html), [time$](4gl_time$.html), [DateTime](4gl_datetime.html), [gdatetime$](4gl_gdatetime$.html).

  

[Index](index.html)  [Home](getting-started_home.html)