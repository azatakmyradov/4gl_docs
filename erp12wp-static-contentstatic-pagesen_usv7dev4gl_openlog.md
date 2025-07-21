[Index](index.html)  [Home](getting-started_home.html)

Openlog

This function sets the Sage X3 engine in log mode. When log mode is activated, a file located in the 'TMP' subfolder of the folder defined by the "ADXDIR" environment variable is opened and filled with log information.

In some cases, the Customer Support team may refer to the file contents in order to provide a diagnosis.

# Syntax

```
ST=openlog(MODE)
```

It uses the following parameters:

* `ST` is an integer value that stores the return status (0 if everything is OK).
* `MODE` is an integer value defining the different event types that are logged. Every event type is defined as a power of 2 value, and `MODE` is the sum of the options retained.

| Value | Type of Event |
| --- | --- |
| 1 | 'Gosub' and 'Call' stack log |
| 2 | All instructions log |
| 4 | 'Read' and 'For' request log |
| 8 | Log of all sadxxx requests |
| 16 | Log of all JSon exchanges |
| 32 | Log of all the Classic mode exchanges |
| 64 | Log of all the sadldap exchanges |
| 128 | Log of all the opadxd exchanges |

# Example

```
# Log the 'Gosub', 'Call', and database requests
I=openlog(5)
```

# See also

[Closelog](4gl_closelog.html), [Getlogname](4gl_getlogname.html)

  

[Index](index.html)  [Home](getting-started_home.html)