[Index](index.html)  [Home](getting-started_home.html)

Filinfo

`filinfo` returns the properties of a file located on a file system that is accessible by the X3 engine. The file path is given as argument, and a second numeric argument defines the returned properties.

On UNIX, the `filinfo` performs a `stat` function on the file.

## Syntax

```
   filinfo(FILE_PATH,INTEGER_EXPR)
```

* FILE\_PATH is a string expression that returns the file path. It can be prefixed by a server name with the syntax `server@path`, if the server has an adxd service running.

## Examples

```
### Example 1: Check the size (in bytes) of a file
#### If the result is negative, the file doesn't exist or is not accessible
  FILE_SIZE = filinfo(FILE_PATH, 7)

### Example 2: What is the type of the UNIX MYFILE file ?
#### The P1, P2, PDIR, PCAR, PBLO, PFI1, PFI2, PFIF value might depend on the version of UNIX
#### check in mknod (2) documentation
  P1 = 2 ^ 12 : P2 = 16
  PFIF = 1 : PCAR = 2 : PDIR = 4 : PBLO = 6 : PFI1 = 0 : PFI2 = 8
  FILE_MODE = filinfo(FICHIER, 0)
  If FILE_MODE > 0
    Case int(mod(FILE_MODE/P1, P2))
      When PFIF : FILE_TYPE="fifo"
      When PCAR : FILE_TYPE="character device"
      When PDIR : FILE_TYPE="directory"
      When PBLO : FILE_TYPE="block device"
      When PFI1, PFI2 : FILE_TYPE="normal file"
      When default :FILE_TYPE="unknown"
    Endcase
  Else
    FILE_TYPE="(cannot be read)"
  Endif

### Example 3: two files xx.c and xx.o are present in the current directory
#### If the xx.c file is most recent than xx.o, let's recompile it
  Local Char TRACE_ERR(80)(1..24)

## Check the dates
  If filinfo("xx.c", 9) > filinfo("xx.o", 9)
    System "cc -c xx.c -o xx.o 2>trace.com"
    # Is the logfile empty?
    If filinfo("trace.com", 7)
      ERROR_FOUND=1
    Else
      ERROR_FOUND=0
    Endif
  Endif

## A file will be modified only if the number of links is 1
    NB_LINKS = filinfo(DIRECTORY+"/"+FILE_NAME,4)
    If NB_LINKS<0    : ERROR_MSG="File does not exist"
    Elsif NB_LIENS >1: ERROR_MSG="File with several links"
    Else
       Openio DIRECTORY+"/"+FILE_NAME
       ...
    Endif
```

## Description

`filinfo`returns the properties of a file in a file system as the unix function stat (2) does. Depending on the second argument given, a different property is returned, according to the following table:

| Second argument | Property | Available on UNIX | Available on Windows |
| --- | --- | --- | --- |
| 0 | File mode (type, permissions) | yes | yes |
| 1 | Inode number | yes | no |
| 2 | Id of the device on which the file is located | yes | no |
| 3 | Id of the device if the file is a device | yes | no |
| 4 | Number of links | yes | 1 is returned |
| 5 | User ID of the owner of the file | yes | yes |
| 6 | Group ID of the owner of the file | yes | yes |
| 7 | File size in bytes | yes | yes |
| 8 | Last access time in millisecond since 1970,1,1 | yes | yes |
| 9 | Last modification time in millisecond since 1970,1,1 | yes | \* |
| 10 | Last status change time in millisecond since 1970,1,1 | yes | \* |

(\*) On Windows, the value returned for second arguments 9 and 10 (above) is the last access time.

## Comments

`filinfo` returns an [Integer](4gl_integer.html).

If the file does not exist or cannot be accessed, a negative value that corresponds to the error status returned by the operating system is rendered. The usual values are the following:

| Error value | Description |
| --- | --- |
| -20 | File does not exist. |
| -27 | Access to the directory is denied. |

## Associated errors

| Error code | Description |
| --- | --- |
| 10 | Incorrect argument type. |
| 50 | The second argument is not in the [0,10] range. |

## See also

[filpath](4gl_filpath.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html)

  

[Index](index.html)  [Home](getting-started_home.html)