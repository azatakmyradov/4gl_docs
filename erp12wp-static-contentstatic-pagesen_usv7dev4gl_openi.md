[Index](index.html)  [Home](getting-started_home.html)

Openi

Use `Openi` to open and close a sequential file in read-only mode on one of the available servers from a Sage X3 application server.

# Syntax

```
   Openi
   Openi Using [ABBREVIATION]
   Openi FILE_EXPR
   Openi FILE_EXPR Using [ABBREVIATION]
   Openi FILE_EXPR, SEEK_EXPR
   Openi FILE_EXPR, SEEK_EXPR  Using [ABBREVIATION]
```

\* `FILE\_EXPR` is an expression that returns a string containing the path of the file to open.
\* `SEEK\_EXPR` is an integer expression that returns the offset in the file (in bytes) from which the read starts. If omitted or if 0, the read starts from the beginning.
\* `ABBREVIATION` is an abbreviation that identifies the channel opened to read the file.

# Examples

```
   # Let's open a file on the server, skipping the first 10 characters
    Openi "C:\Temp\my_file.txt",10
    ...
   # Close the last file opened to read
    Openi

   # Opening a file on the "distrib" server
    Openi "distrib@"+[L]NOMFIC

   # Open two files located in the TMP sub-directory of the folder directory on the application server
    Openi filpath('TMP','rdfile1','') Using [YYY]
    Openi filpath('TMP','rdfile2','') Using [ZZZ]

   # Close the two previously opened files
    Openi Using [YYY]
    Openi Using [ZZZ]
```

# Description and comments

Use `Openi` to open a file for reading data with [Rdseq](4gl_rdseq.html) and [Getseq](4gl_getseq.html).

The first parameter is the file path that must be opened:

* The [filpath](4gl_filpath.html) function can be used to compute it.
* This file path can be located on another server where a SAFE X3 administration engine is installed with the syntax `"server@local_path"`, where `server` is the server name and `local_path` the path of the file on this server.
* If the file does not exist, an error is thrown.
* `Openi`, used without a file name, closes the previously opened file.

The value given in the 2nd parameter is used to position the read position (in bytes) in the file:

* If it is missing or null, the position is at the beginning of the file.
* If negative, an error is thrown.
* If positive, the initial read position is there even if it exceeds the size of the file: you get an end of file status at the first read operation.
* The [Seek](4gl_seek.html) instruction can be used to move the read pointer during the [Read](4gl_read.html).

When a unique file is opened, there is no need to give an abbreviation. If several files are opened, it is preferable to use an abbreviation that can be freely chosen and used later to identify the channel used.  
\* The maximum number of sequential files that can be opened simultaneously is given by the value of the [adxmso](4gl_adxmso.html) system variable.  
\* For a given abbreviation (or without abbreviation), only one sequential file can be opened by `Openi` or [Openio](4gl_openio.html) at a given moment. Opening a file in write mode closes any file that may have been previously opened with `Openi` or [Openio](4gl_openio.html) with this abbreviation (or with no abbreviation).

The current read position can be known:  
\* By [adxseek](4gl_adxseek.html)(0) if the file has been opened without abbreviation.  
\* By `adxseek("ABREV")` if the `[ABREV]` abbreviation is used.

# Execution restriction in Clouds environment

For obvious security reasons, the execution of this instruction is controlled on Clouds environments:

* in `trusted` execution conditions, only the locations allowed by the sandbox white list are allowed.
* in `untrusted` execution conditions, only the locations defined as `secured` are allowed.

If the conditions defined by the sandbox are not fulfilled, an error 27 will be raised.

For more information, look at the [sandbox configuration page](getting-started_sandbox-configuration-file.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | FILE\_EXPR is not a Char type or SEEK\_EXPR is not numeric. |
| 20 | Nonexistent file or path folder. |
| 25 | System error when connecting to a remote server. |
| 27 | Access not possible, permission denied. |
| 50 | exp\_depl < 0. |
| 57 | No seek operation allowed on the file. |
| 60 | Too many channels used. |

# See also

[Openo](4gl_openo.html), [Openio](4gl_openio.html), [Seek](4gl_seek.html), [Getseq](4gl_getseq.html), [Rdseq](4gl_rdseq.html), [Putseq](4gl_putseq.html), [Wrseq](4gl_wrseq.html), [adxifs](4gl_adxifs.html), [adxirs](4gl_adxirs.html), [adxium](4gl_adxium.html), [adxmso](4gl_adxmso.html), [adxseek](4gl_adxseek.html).

  

[Index](index.html)  [Home](getting-started_home.html)