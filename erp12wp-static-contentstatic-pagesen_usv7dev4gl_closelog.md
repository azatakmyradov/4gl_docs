[Index](index.html)  [Home](getting-started_home.html)

Closelog

This function stops the Sage X3 engine log mode that opens a log file to be filled with log information. This file is located in the 'TMP' subfolder of the folder defined by the "ADXDIR" environment variable.

In some cases, the Customer Support team may refer to the file contents in order to form a diagnosis.

# Syntax

```
ST=closelog()
```

It uses the following parameters:

* `ST` is an integer value that stores the return status (0 if everything is fine).

# Example

```
# Stop the Sage X3 engine log
I=closelog()
```

# See also

[openlog](4gl_openlog.html), [getlogname](4gl_getlogname.html)

  

[Index](index.html)  [Home](getting-started_home.html)