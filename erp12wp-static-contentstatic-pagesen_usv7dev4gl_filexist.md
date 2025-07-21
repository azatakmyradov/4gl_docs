[Index](index.html)  [Home](getting-started_home.html)

Filexist

This function checks if a given Sage X3 script file exists on a server. It returns 1 if the file exists, if not, it returns 0.

# Syntax

```
FOUND=filexist(SERVER, FOLDER, SCRIPT_NAME)
```

It uses the following parameters:

* `SERVER` is the DNS name (or IP address) of a server that can be accessed from Sage X3. By default, the current application server is used.
* `FOLDER` is a Sage X3 folder name, relative to the root folder of the application server. By default, the current folder is used.
* `SCRIPT_NAME` is the name of the Sage X3 script, without the extension.

# Example

```
I=filexist("", "", "TEST")
If I
  Call MYTEST From TEST
Endif
```

# Note

`Filexist` execution is based on a Sage X3 service. Only servers on which a Sage X3 administration service (adxd) has been installed can be accessed by this instruction.

# See also

[objectexist](4gl_objectexist.html)

  

[Index](index.html)  [Home](getting-started_home.html)