[Index](index.html)  [Home](getting-started_home.html)

Getlogname

This function returns the file name of the last Sage X3 engine log. When the log mode is activated, a file located in the 'TMP' subfolder of the folder defined by the "ADXDIR" environment variable is opened and filled with log information.

In some cases, the Customer Support team may refer to the file contents in order to provide a diagnosis.

# Syntax

```
LOG_FILE=getlogname()
```

It uses the following parameters:

* `LOG_FILE` is a string value that returns the last generated log file.

# Example

```
# logs the instructions in the SUBROUTINE label
Local Integer I
Local char MYLOG(200)
I=openlog(2)
Gosub SUBROUTINE
I=closelog()

# After this instruction, MYLOG contains the name of the file created
MYLOG=getlogname()
```

# See also

[Closelog](4gl_closelog.html), [Openlog](4gl_openlog.html)

  

[Index](index.html)  [Home](getting-started_home.html)