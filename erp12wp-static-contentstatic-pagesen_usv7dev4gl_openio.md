[Index](index.html)  [Home](getting-started_home.html)

Openio

Use `Openio` to open and close a sequential file in update mode on one of the available servers from the Sage X3 application server.

# Syntax

```
   Openio
   Openio Using [ABBREVIATION]
   Openio FILE_EXPR
   Openio FILE_EXPR Using [ABBREVIATION]
   Openio FILE_EXPR, SIZE_EXPR
   Openio FILE_EXPR, SIZE_EXPR  Using [ABBREVIATION]
```

* `FILE_EXPR` is an expression that returns a string containing the path of the file to open.
* `SIZE_EXPR` is an integer expression that returns the offset in the file (in bytes) from which the write starts after opening the file (note that Openio does not truncate the file as Openo does it).
* `ABBREVIATION` is an abbreviation that identifies the channel opened to read the file.

# Examples

```
   # Let's open a file on the server to append data to it
    Openio "C:\Temp\my_file.txt",-1
    ...
   # Close the last file opened to read
    Openio

   # Opening a file on the "distrib" server in read write mode and an initial position at the beginning
    Openio "distrib@"+[L]NOMFIC

   # Open two files located in the TMP sub-directory of the folder directory on the application server
   # The initial position is at byte 1024.
    Openio filpath('TMP','rdfile1',''),1024 Using [YYY]
    Openio filpath('TMP','rdfile2',''),1024 Using [ZZZ]

   # Close the two previously opened files
    Openio Using [YYY]
    Openio Using [ZZZ]
```

# Description

Use `Openio` to open a file for reading and writing data with [Rdseq](4gl_rdseq.html), [Wrseq](4gl_wrseq.html), [Getseq](4gl_getseq.html), and [Putseq](4gl_putseq.html).

The first parameter is the file path that must be opened:

* The [filpath](4gl_filpath.html) function can be used to compute it.
* This file path can be located on another server where a SAFE X3 administration engine is installed with the syntax `"server@local_path"`, where `server` is the server name and `local_path` the path of the file on this server.
* If the file does not exist, `Openio` throws an error and never creates the file.
* `Openio`, used without a file name, closes the previously opened file.

The value in the 2nd parameter is used to position the read/write position (in bytes) in the file:

* If it is missing, or null, the position is at the beginning of the file.
* If negative, the original position is at the end of the file.
* If positive and if it exceeds the size of the file, the first write at this position will increase the file size by adding null characters at the end of the file to reach the expected size.

When a unique file is opened, there is no need to give an abbreviation. If several files can be opened, it is preferable to use an abbreviation that can be freely chosen and used later to identify the channel used.  
\* The maximum number of sequential files that can be opened simultaneously is given by the value of the [adxmso](4gl_adxmso.html) system variable.  
\* For a given abbreviation (or without abbreviation), only one sequential file can be opened by `Openio` [Openi](4gl_openi.html), or [Openo](4gl_openo.html) at a given moment. Opening a file in read/write mode closes any file that may have been previously opened with `Openio`, [Openi](4gl_openi.html), or [Openo](4gl_openo.html) with this abbreviation (or with no abbreviation).

The current read/write position can be known:  
\* By [adxseek](4gl_adxseek.html)(0) or [adxseek](4gl_adxseek.html)(1) if the file has been opened without abbreviation. On a file opened by `Openio`, the two values of [adxseek](4gl_adxseek.html)(0) and [adxseek](4gl_adxseek.html)(1) are always the same.  
\* By `adxseek("ABREV")` if the `[ABREV]` abbreviation has been used.

# Comments

Note that `Openio` does not manage the write conflicts that can happen when two users try to access the same file. It is recommended to position a [Lock](4gl_lock.html) on a predefined symbol. The data written in sequential files is not included in database transactions. Therefore, [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), and [Rollback](4gl_rollback.html) have no interaction with the files written by `Openio`.

The data write operations are buffered by the system and are completely done only after the file is closed by `Openio`. If it is necessary to ensure that the data has been written, use the instruction `Seek 0` on the abbreviation. This instruction flushes the write buffers.

# Execution restriction in Clouds environment

For obvious security reasons, the execution of this instruction is controlled on Clouds environments:

* in `trusted` execution conditions, only the locations allowed by the sandbox white list as `writable` are allowed.
* in `untrusted` execution conditions, only the locations defined as `writable` and `secured` are allowed.

If the conditions defined by the sandbox are not fulfilled, an error 27 will be raised.

For more information, look at the [sandbox configuration page](getting-started_sandbox-configuration-file.html).

The version 2 (code named mindo) will implement the file operations in mongoDB rather than on file systems. The use of Openio to update a file starting at a given position will need to perform a copy of the file and won't therefore be performing with good performances. I is therefore recommended to avoid using this syntax except for small file. Remember that you have the following patterns:

```
Openo FILENAME,0   : # Opens a file and truncates it if it already exists
Openo FILENAME, -1 :  # Opens a file in append mode
```

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | FILE\_EXPR is not a Char type or SEEK\_EXPR is not numeric. |
| 20 | Nonexistent file or path folder. |
| 25 | System error when connecting to a remote server. |
| 27 | Access not possible, permission denied. |
| 44 | No more disk space. |
| 50 | exp\_depl > 0. |
| 57 | No seek operation allowed on the file. |
| 60 | Too many channels used. |
| 65 | Size limit exceeded for the file. |

# See also

[Openi](4gl_openi.html), [Openo](4gl_openo.html), [Seek](4gl_seek.html), [Getseq](4gl_getseq.html), [Rdseq](4gl_rdseq.html), [Putseq](4gl_putseq.html), [Wrseq](4gl_wrseq.html), [adxifs](4gl_adxifs.html), [adxirs](4gl_adxirs.html), [adxium](4gl_adxium.html), [adxmso](4gl_adxmso.html).

  

[Index](index.html)  [Home](getting-started_home.html)