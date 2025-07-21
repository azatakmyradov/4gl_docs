[Index](index.html)  [Home](getting-started_home.html)

Timestamp$

`timestamp$` returns a string value containing a time stamp, which is the number of milliseconds elapsed since the first of January 1970, at 00:00:00 time GMT.

# Syntax

```
  timestamp$
```

# Example

```
  Local decimal D
  Local Decimal T : # Cannot be an integer because timestamp value is greater the 2^32
  Local Integer T1
  Local Char MY_TIME(8)
  T=val(timestamp$)
  T1=mod(T,3600*24*1000)/1000 : # modulo the number of milliseconds in a day
  MY_TIME=format$("N0:2",int(T1/3600))+":"+format$("N0:2",int(mod(T1,3600)/60))+":"+format$("N0:2",mod(T1,60))
  # Now, MY_TIME contains the GMT hour in hh:mm:ss format
```

# Description

`timestamp$` returns a timestamp in ASCII format.

# Associated errors

No error associated.

# See also

[time$](4gl_time$.html), [datetime$](4gl_datetime$.html), [date$](4gl_date$.html), [gdatetime$](4gl_gdatetime$.html).

  

[Index](index.html)  [Home](getting-started_home.html)