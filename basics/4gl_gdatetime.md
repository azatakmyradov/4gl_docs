[Index](index.html)  [Home](getting-started_home.html)

Gdatetime$

This function converts a datetime string in canonical format to a DateTime value.

The canonical string **must** be formatted as follows on 20 characters:

```
YYYY-MM-DDThh:mm:ssZ
```

  
Where:

* YYYY: 4 digit year
* MM: 2 digit month (01-12)
* DD: 2 digit day of the month (01-31)
* hh: 2 digit hour (00-23)
* mm: 2 digit minute (00-59)
* ss: 2 digit second (00-59)

The values are expressed in GMT timezone and the string is terminated by a `Z` which stands for GMT.

# Syntax

```
gdatetime$(str)
```

# Examples

A simple example:

```
MYDATETIME=gdatetime$("2012-10-03T07:55:30Z") : # Constant DateTime
MYDATETIME=gdatetime$(DATETIME_STR) : # Transforms the string DATETIME_STR
```

A complex example with more data types:

```
# This example gets the current timestamp and converts it to a datetime.
# It is equivalent to the single instruction MY_DATETIME=datetime$ !!!

# First we declare some variables
Local Decimal MY_TIMESTAMP
Local Date MY_DATE
Local Integer MY_TIME
Local Char MY_CHAR_DATETIME(20)
Local DATETIME MY_DATETIME 

  # timestamp$ gives the number of milliseconds since January 1, 1970, as a string.
  # We store it in a decimal (Integer would be out of range).
  MY_TIMESTAMP=val(timestamp$)

  # Compute the date.
  MY_DATE=[1/1/1970]+int(MY_TIMESTAMP/(24*3600*1000))

  # Compute the number of seconds since the beginning of the day.
  MY_TIME=mod(MY_TIMESTAMP/1000,24*3600)

  # Format the canonical string.
  MY_CHAR_DATETIME = format$("D:4Y[-]2M[-]2D[T]",MY_DATE)
&                  + format$("N0:2#",int(MY_TIME/3600))
&                  + ":" + format$("N0:2#",int(mod(MY_TIME,3600)/60))
&                  + ":" + format$("N0:2#",int(mod(MY_TIME,60)))+"Z"

  # Now convert it to a datetime value
  MY_DATETIME=gdatetime$(MY_CHAR_DATETIME)
```

# Comments

The [num$](../4gl/num$.md) function converts in the other direction, from dateTime to canonical string:

```
MY_DATETIME=gdatetime$(num$(datetime$))
```

This is equivalent to:

```
MY_DATETIME=datetime$
```

If the input string has an invalid format, gdatetime$ returns a null datetime and no error is created. For example:

```
BAD_DATETIME1=gdatetime$(left$(num$(datetime$),19)) : # A character is missing (20 characters expected)
BAD_DATETIME=2gdatetime$("Hello world") : # Obviously not a datetime!!!
STRING1=num$(BAD_DATETIME1)
STRING2=num$(BAD_DATETIME2)
# STRING1 and STRING2 are both "0000-00-00T00:00:00Z"
```

# See also

[Datetime definition](4gl_glossary-datetime.html), [datetime$](4gl_datetime$.html), [Datetime](4gl_datetime.html)

  

[Index](index.html)  [Home](getting-started_home.html)