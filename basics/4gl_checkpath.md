[Index](index.html)  [Home](getting-started_home.html)

Checkpath

`checkpath` is a function that allows you to verify if a file path is in the [white list](getting-started_sandbox-configuration-file.html) of the engine and can therefore be accessed.

# Syntax

```
checkpath(FILE_PATH,ACCESS_MODE)
```

* `FILE_PATH` is the path of a file or a directory which accessibility must be checked. The files do not need to exist, the only check that is done is the control against the white list. For example, if `C:\tmp\subdir\myfile.src` is checked and if `C:\tmp` is in the white list, the return is positive even if the `subdir` folder does not exist.
* `ACCESS_MODE` can have the value 0 (if you want to check the read access) or 1 (if you want to check the write access).

This function returns a 1 if the requested access rights are not denied by the white list definition; otherwise it returns a 0.

# See also

[Delfile](4gl_delfile.html), [Renamefile](4gl_renamefile.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html).

  

[Index](index.html)  [Home](getting-started_home.html)