[Index](index.html)  [Home](getting-started_home.html)

Objectexist

This function checks if a given class exists on an application server.

It returns '1' if the class exists; otherwise, it returns '0'.

# Syntax

```
FOUND=objectexist(SERVER, FOLDER, CLASS_NAME)
```

It uses the following parameters:

* `SERVER` is the DNS name (or IP address) of a server that can be accessed from Sage X3. By default, the current application server is used.
* `FOLDER` is a Sage X3 folder name, relative to the root folder of the application server. By default, the current folder is used.
* `CLASS_NAME` is the name of the Sage X3 class, without the extension.

# Example

```
FOUND=objexist("","","C_CUSTOMER")
If FOUND
  Local Instance MYCUSTOMER Using C_CUSTOMER
Endif
```

# Note

`objectexist` execution is based on a Sage X3 service. Only servers on which a Sage X3 administration service (adxd) have been installed, can be accessed by this instruction.

# See also

[filexist](4gl_filexist.html).

  

[Index](index.html)  [Home](getting-started_home.html)