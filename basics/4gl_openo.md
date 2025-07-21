[Index](index.html)  [Home](getting-started_home.html)

Openo

Use `Openo` to open and close a sequential file in write-only mode on one of the available servers from the Sage X3 application server.

# Syntax

```
   Openo
   Openo Using [ABBREVIATION]
   Openo FILE_EXPR
   Openo FILE_EXPR Using [ABBREVIATION]
   Openo FILE_EXPR, SIZE_EXPR
   Openo FILE_EXPR, SIZE_EXPR  Using [ABBREVIATION]
```

* `FILE_EXPR` is an expression that returns a string containing the path of the file to open.
* `SIZE_EXPR` is an integer expression that returns the offset in the file (in bytes) from which the write starts after truncation of the file.
* `ABBREVIATION` is an abbreviation that identifies the channel opened to read the file.

# Examples

```
   # Let's open a file on the server to appen data to it
    Openo "C:\Temp\my_file.txt",-1
    ...
   # Close the last file opened to read
    Openo

   # Opening a file on the "distrib" server with truncation
    Openo "distrib@"+[L]NOMFIC

   # Open two files located in the TMP sub-directory of the folder directory on the application server
   # Both files will be truncated to 1024 size
    Openo filpath('TMP','rdfile1',''),1024 Using [YYY]
    Openo filpath('TMP','rdfile2',''),1024 Using [ZZZ]

   # Close the two previously opened files
    Openo Using [YYY]
    Openo Using [ZZZ]
```

# Description and comments

Use `Openo` to open a file for writing data with [Wrseq](4gl_wrseq.html) and [Putseq](4gl_putseq.html).

The first parameter is the file path that has to open:

* The [filpath](4gl_filpath.html) function can be used to compute it.
* This file path can be located on another server where a SAFE X3 administration engine is installed with the syntax `"server@local_path"`, where `server` is the server name and `local_path` the path of the file on this server.
* If the file does not exist, `Openo` with a null or negative position value creates the file, while `Openo` with a strictly positive value throws an error.
* `Openo`, used without a file name, closes the previously opened file.

The value in the 2nd parameter is used to position the write position (in bytes) in the file:

* If it is missing or null, the position is at the beginning of the file and the file is truncated. When a truncation to 0 is done, the file is really truncated and never deleted. This means that if other links exist on the file in a Unix file system, they will remain. If the file is deleted first by using [Delfile](4gl_delfile.html), the other links remain on the file and a new empty file is created by `Openo`.
* If negative, the original position is at the end of the file.
* If positive and if it exceeds the size of the file, the first write at this position will increase the file size by adding null characters at the end of the file to reach the expected size.
* If positive and if it is smaller than the size of the file, the file is first truncated to the right size. To avoid a file deletion, truncating a file to a size that is not null is done by a preliminary copy of the size to keep in a temporary file, followed by a truncation to 0 of the file, a reverse copy of the temporary file on the origin truncated file, and finally a deletion of the temporary file. This can use temporary space and take time if the size is big.

When a unique file is opened, there is no need to give an abbreviation. If several file can be opened, it is preferable to use an abbreviation that can be freely chosen and used later to identify the channel used.  
\* The maximum number of sequential files that can be opened simultaneously is given by the value of the [adxmso](4gl_adxmso.html) system variable.  
\* For a given abbreviation (or without abbreviation), only one sequential file can be opened by `Openo` or [Openio](4gl_openio.html) at a given moment. Opening a file in write mode closes any file that may have been previously opened with `Openo` or [Openio](4gl_openio.html) with this abbreviation (or with no abbreviation).

The current read/write position can be known:  
\* By [adxseek](4gl_adxseek.html)(1) if the file is opened without abbreviation.  
\* By `adxseek("ABREV")` if the `[ABREV]` abbreviation is used.

# Comments

Note that `Openo` does not manage the write conflicts that can happen when two users try to access the same file. It is recommended to position a [Lock](4gl_lock.html) on a predefined symbol. The data written in sequential files is not included in database transactions. Therefore, [Trbegin](4gl_trbegin.html), [Commit](4gl_commit.html), and [Rollback](4gl_rollback.html) have no interaction with the files written by `Openo`.

The data write operations are buffered by the system and are completely done only after the file is closed by `Openo`. If it is necessary to ensure that the data is written, use the instruction `Seek 0` on the abbreviation. This instruction flushes the write buffers.

# Execution restriction in Clouds environment

For obvious security reasons, the execution of this instruction is controlled on Clouds environments:

* in `trusted` execution conditions, only the locations allowed by the sandbox white list as `writable` are allowed.
* in `untrusted` execution conditions, only the locations defined as `writable` and `secured` are allowed.

If the conditions defined by the sandbox are not fulfilled, an error 27 will be raised.

For more information, look at the [sandbox configuration page](getting-started_sandbox-configuration-file.html).

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | FILE\_EXPR is not a Char type or SEEK\_EXPR is not numeric. |
| 20 | Nonexistent file or path folder. |
| 25 | System error when connecting to a remote server. |
| 27 | Access not possible, permission denied. |
| 44 | No more disk space. |
| 50 | exp\_depl is not an integer value. |
| 57 | No seek operation allowed on the file. |
| 60 | Too many channels used. |
| 65 | Size limit exceeded for the file. |

# See also

[Openi](4gl_openi.html), [Openio](4gl_openio.html), [Seek](4gl_seek.html), [Getseq](4gl_getseq.html), [Rdseq](4gl_rdseq.html), [Putseq](4gl_putseq.html), [Wrseq](4gl_wrseq.html), [adxifs](4gl_adxifs.html), [adxirs](4gl_adxirs.html), [adxium](4gl_adxium.html), [adxmso](4gl_adxmso.html), [adxseek](4gl_adxseek.html).

  

[Index](index.html)  [Home](getting-started_home.html)