[Index](index.html)  [Home](getting-started_home.html)

Adxmac

`adxmac` is a function used to identify the server in which the current folder, or one of its reference folder, is installed. It also allows you to obtain the network name of the client (in Version 7 mode, the client is the node.js server).

# Syntax

```
   adxmac(INDEX)
```

* `INDEX` is a integer value expression that can have the following values:
  + **'-2' :** the client. If using a 'classic non-browser client' then this value contains the client name or ip of where the classic client is runnning. If running a browser client, the web server supporting the browser connection is returned.
  + **'-1' :** the process server where the script is executing.
  + **'0' :** the application server where the folder being accessed is installed. If the adxmac(0) is equal to blank ("") then the application is the same as the process server. To return the server id or ip in this case use adxmac(-1). Note, that most X3 scripting routines that require a server id or ip accept adxmac(0) being blank and resolve blank server names. For example, see [filpath](4gl_filpath.html)
  + **'N' :** the application server where the parent folder `nomap(N)` is installed (it is also the folder `adxmother(N-1))` If blank then the application server is the same as the process server returned in adxmac(-1).

# Example

```
  # What is the application server name
  APPSERV_NAME=adxmac(0)

  # Let's execute a system command on the process server
  System adxmac(-1)+"@"+MY_SYSTEM_ORDER
```

# See also

[System](4gl_system.html), [nomap](4gl_nomap.html), [adxmother](4gl_adxmother.html).

  

[Index](index.html)  [Home](getting-started_home.html)