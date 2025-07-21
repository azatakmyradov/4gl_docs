[Index](index.html)  [Home](getting-started_home.html)

System

`System` allows you to execute system orders and to obtain the information sent by the order on the standard output.

# Syntax

```
(1)   System EXPR_ORDER
(2)   System VAR_RET = EXPR_ORDER
(3)   Local File (VAR_LIST) From System EXPR_ORDER As [CLASS]
```

The syntax 3 is described in the [File](../4gl/file.md) documentation. The parameters are the following:

* `EXPR_ORDER` is a string expression giving the system order as it would be typed in a shell. It can be followed by a server name with the syntax `SERVER@ORDER`, where:
  + `SERVER` is a server name on the network that has a Sage X3 administration engine installed.
  + `ORDER` is the system order.
* `VAR_RET` is a string character variable that will contain the result sent by the standard output. `VAR_RET` can be an array of lines. For every line sent back from the order, an additional index in the array will be filled. This is appropriate if the number of lines sent back by the system order is not too large. The lines that exceeds the dimension of the array will be ignored. If a large number of lines are sent back, it is preferable to use the syntax 3 ([File](4gl_file.html)... `From System`...).

# Examples

```
   # Copy FILE1 to FILE2 with stderr redirection on UNIX
    System "cp "+FILE1+" "+FILE2-"2>/dev/null"

   # List of a directory on a Windows server on which the first reference folder is located
   # Returns the list of files and the number of lines read
   # If no directory is given we default it with a temporary directory
    Subprog DIRECTORY_LIST(FILES,DIRECTORY,NUMBER)
    Variable Char FILES(100)(1..)
    Value Char DIRECTORY(100)
    If DIRECTORY="" : DIRECTORY = "C:\sage\tmp" : Endif
    System FILES = adxmac(1)+"@DIR/b/o:n"+DIRECTORY
    NUMBER=stat1
    End
```

# Description

System executes a system order. The server in which the system order must be executed can be given in the system order expression:

* If `server@order` is used, the order is executed on the server provided.
* If `@order` is used, the order is executed on the application server.
* If `order` is used, the order is executed on the process server.

If a variable is given (syntax 2), the standard output is sent back to this variable. The [stat1](4gl_stat1.html) variable returns the number of lines sent back (it can be greater than the dimension of the variable: in this case, the remaining lines are lost).

# Execution restriction in Clouds environment

For obvious security reasons, the execution of this instruction is controlled on Clouds environments:

* in `trusted` execution conditions, only the commands allowed by a white list are allowed.
* in `untrusted` execution conditions, `System` execution is not allowed.

When the execution is denied, an error 27 is raised.

For more information, look at the [sandbox configuration page](getting-started_sandbox-configuration-file.html).

# See also

[stat1](4gl_stat1.html), [File](4gl_file.html).

  

[Index](index.html)  [Home](getting-started_home.html)