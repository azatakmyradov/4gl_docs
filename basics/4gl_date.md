[Index](index.html)  [Home](getting-started_home.html)

Date

This keyword declares a date variable where the value is within the range from [1/1/1600] to [31/12/9999], plus a null date [0/0/0].

# Syntax

```
Local    Date NAME
Local    Date NAME(DIMENSIONS)
Variable Date NAME(DIMENSIONS)
Value    Date NAME(DIMENSIONS)
Const    Date NAME(DIMENSIONS)
```

* `NAME` is the name of the declared variable.
* `DIMENSIONS` can be:
  + A single numeric value DIM, which means that we have an array with an index range from 0 to DIM-1.
  + A range of numeric values INDEX1..INDEX2. The index varies between INDEX1 and INDEX2.
  + Several indexes or index ranges separated by a comma. For multiple dimension arrays, up to four dimensions are possible.

Several variable declarations can be done on the same line, separated by a comma.

[Local](4gl_local.html) declarations create the variables in the current local variable class that is not seen by nested or calling subprograms. The [Call](4gl_call.html) / [Subprog](4gl_subprog.html) and [func](4gl_func.html) / [Funprog](4gl_funprog.html) insulate the local variables as well as the calls of method by [fmet](4gl_fmet.html).

[Const](4gl_const.html), [Variable](4gl_variable.html), and [Value](4gl_value.html) declarations state the arguments sent by a [Call](4gl_call.html), [func](4gl_func.html), or [fmet](4gl_fmet.html). With these syntaxes, the dimensions and the index ranges can be omitted wherever the parentheses are present. The dimension and index ranges are defined by the calling program.

# Example

```
# Direct declarations
Local Date TODAY, TOMORROW, YESTERDAY : # Local date variables
Local Date PERIOD_LIMITS(1..60) : # An array of 60 dates values

# A sub-program sending dates and returning a result
Funprog SEND_DATES(MYDATES)
Variable Date MYDATES(,) : # A 2 dimensions matrix of dates is sent as reference
...
End SEND_STATUS

# A sub-program storing dates
Subprog STORE_VALUES(APPOINTMENT_DATES)
Value Date APPOINTMENT_DATES(1..5) : # An array of 5 elements is sent (a copy is done when passing the arguments)
...
End
```

# Operators and dates

The standard arithmetic operators can be used to compare dates. These operators include >, >=, =<, <, +, -, += and -=.

```
Local Date TEST_DATE
Local Char TEST_CHAR

TEST_DATE = [31/01/2014]                    # TEST_DATE = 20140131      (Date format)
TEST_CHAR = TEST_DATE                       # TEST_CHAR = "20140131"    (String format - implicit data type conversion)
TEST_DATE > date$                           # Is 20140131 > date$ ? Either true or false depending on date
                                            #   All other comparison operators work
TEST_DATE += 50                             # Add 50 days to TEST_DATE (Note upper limit=[31/12/9999])
TEST_DATE -= 75                             # Subtract 75 days from TEST_DATE (Note lower limit=[01/01/1600])
TEST_DATE = "140131"                        # Convert string to date using adxdcs year
TEST_CHAR = num$(TEST_DATE)                 # TEST_CHAR = "[31/01/2014]"
```

# Functions and dates

# Implicit data type conversion

The date data type will implicitly convert two string formats to a valid date. The two string formats are "YYYYMMDD" and "YYMMDD". In the format "YYMMDD" that the pivot year variable [adxdcs](4gl_adxdcs.html) is used to determine the century.

```
<pre><code>
Local Date MY_DATE         # Declare date
MY_DATE = "20170630"       # String YYYYMMDD date
MY_DATE = "170630"         # String YYMMDD date
</pre></code>
```

  
Both conversions translate to date 20170630 as the pivot year [adxdcs](4gl_adxdcs.html) is equal to 1950. This means all dates in YYMMDD format with YY equal to or greater than 50 translate to years starting in 1900 and YY less than 50 translates to years starting in 2000 during the data type conversion.

# See also

[Global](4gl_global.html), [Local](4gl_local.html), [Variable](4gl_variable.html), [Value](4gl_value.html), [Const](4gl_const.html), [Tinyint](4gl_tinyint.html), [Shortint](4gl_shortint.html), [Integer](4gl_integer.html), [Float](4gl_float.html), [Double](4gl_double.html), [Decimal](4gl_decimal.html), [Char](4gl_char.html), [Clbfile](4gl_clbfile.html), [Blbfile](4gl_blbfile.html), [Uuident](4gl_uuident.html), [Datetime](4gl_datetime.html), [Instance](4gl_instance.html).

  

[Index](index.html)  [Home](getting-started_home.html)