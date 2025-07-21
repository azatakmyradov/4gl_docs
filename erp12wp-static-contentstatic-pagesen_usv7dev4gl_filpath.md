[Index](index.html)  [Home](getting-started_home.html)

Filpath

`Filpath` creates the access path to a file on a Sage X3 application server.

# Syntax

```
filpath(directory, filename, extension)
filpath(directory, filename, extension, folder)
filpath(directory, filename, extension, folder, volume)
filpath(directory, filename, extension, folder, volume, server)
```

The parameters are the following:

* `Directory` is the relative sub-directory used to create the path.
* `Filename` is the file name.
* `Extension` is the file extension.
* `Folder` can be either a numeric value or a string value containing the name of the folder. If not given, the current folder is used.
* `Volume` is a volume code giving the root directory for building the path. It can contain the following values:
  + "0" corresponds to the directory where the execution engine is installed.
  + "A", "B", and "C" relate to volumes. These volumes where stored in version 6 in a configuration file called adxvolumes. It is now stored in the [Sandbox configuration file](getting-started_sandbox-configuration-file.html).
* `Server` is the server name of a server on the network. A Sage X3 engine must have been installed on it.

# Comments

The path that is returned does not correspond to an existing file, and has the following format:

```
server@/root_path/folder/directory/file_name.extension
```

  
The file operations such as `Openi` and `Openo`, `filinfo`, are able to manage files with the syntax returned by `filpath`.

**The following rules apply to the parameter values:**

* If the directory name begins with an exclamation point (!), the folder parameter is ignored.
* If the directory name is equal to (".".), the path starts with `./` in Unix and `.\` in Windows and does not use folder and volume parameters.
* If the filename begins with a slash or a backslash, the path is considered an absolute path and the parameter folder, volume, and directory are not taken into account.
* If the filename contains a dot character, for instance "ABC.DEF", the folder parameter is ignored and replaced by the first segment (ABC in the example) and the second part is the file name (DEF in the example).
* Otherwise, the path describes a file in the current folder directory by default. `filpath("", "", "")` gives the path of the current folder.
* If the folder is numeric and has a positive value (N), the folder used is the Nth in the parent folder hierarchy.   
  For example:
  + **'0'** means the current folder,
  + **'1'** means its parent folder,
  + **'2'** means the grandparent folder.
* If the folder is a numeric value equal to '-1', the file is first searched in the current folder. If it is not found, it is searched for in the reference folder in the order in which they were declared. If it is still not found, the path related to the current folder is returned.
* If the folder equals zero (0) or an empty string (""), the file path uses the current folder.
* If the volume is not specified, the one where the folder described is installed - if it exists. If it does not exist on a single volume, the run-time installation directory is used ([adxdir](4gl_adxdir.html)).
* If the volume does not exist, no error appears, and an empty string is returned.
* If the server is given, then the server name is specified in the character string returned in the "server@path" format. If the server is on the same machine as the engine, then the string returned is in the "path" format.
* If the server equals to an empty string (""), the server where the folder is installed is used.
* The pound server name used with the fat client is now deprecated.

# Examples

```
# Verify that the CUSTOMER table compiled description can be accessed from the current folder
  If filinfo(filpath("FIL","CUSTOMER","fde",-1),1) <0
     End -20 : # Does not exist
  Endif

# Compute the root path of the current folder
  FOLDER_PATH = filpath("", "", "")

# Path of the "A" volume on the current server
  A_VOLUME_PATH= filpath("!","","","","A")

# Check if a given script exists in the current folder
  If filinfo(filpath("TRT","MYSCRIPT","adx",0),1) <0
     End -20 : # Does not exist
  Endif
```

# See also

[adxdir](4gl_adxdir.html).

  

[Index](index.html)  [Home](getting-started_home.html)