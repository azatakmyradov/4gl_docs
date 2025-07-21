[Index](index.html)  [Home](getting-started_home.html)

Sandbox configuration file

**For security reasons, you must have a security sandbox definition file for any server where:**

* an `adxd` daemon or service runs,
* an `sadfsq` software is installed to allow access to files in the file system through the Sage X3 engine.

\*\*Security rules have been reinforced from version 7.2: a clear distinction is done between Cloud based and on-premise environments.\*\*
This file is called **configRuntime.json**:
\* It is installed in the **cfg** subfolder of the Sage X3 runtime folder.
\* Ideally, it should be write protected, but readable by the Sage X3 runtime engine.
\* It includes a set of parameters in JSON format, and especially the list of folders where the Sage X3 engine is allowed to access (sandbox definition).

## Cloud security: `trusted` and `untrusted` mode

When an installation is done on the Cloud, the code executed by the engine can run in `trusted` or `untrusted` mode:

* an execution instance of a standard code provided by Sage is `trusted` when called directly or when called from a `trusted` execution instance.
* an execution instance of specific or vertical code is `untrusted`.
* any standard code called from a specific or vertical code executes in `untrusted` mode as well.

Some limitations apply on `trusted` code execution:  
\* the sandbox limitation applies for files accessed from the server.  
\* restrictions exist on the order executed by the `System` command as explained below.

On `untrusted` code execution, the limitations are more severe:  
\* only the sandbox location with `secured` flag set to `true` can be accessed.  
\* no execution of a `System` command is possible.

## Configuration file description

The format of the file is the following:

```
{ 
  "sandbox": {
      "directories": [
         {
            "path": "...",
              "extensions": ["...", "..." ]
              "pattern": ["...", "..." ]
              "writable": true,
              "secured": true,
              "volume": "A"
         }
         â¦
       ],
      "spawn": [
         {
            "path": "â¦",
              "pattern": "â¦"
              "params": [â¦],
              "modes": [â¦]
         }
         â¦
        ],
   "allowConsole" : false

}
```

  
In the `sandbox` section, the `directories` section is a collection of entries that define the sandbox as a whitelist of locations that can be accessed. If there is no match, the access is denied. The following rules apply:

* The volume property is not mandatory, but when defined, it indicates a logical volume previously defined in the `adxvolume` configuration file. For more information, see the [filpath](4gl_filpath.html) documentation.
* `writable` defines if files can be created or modified in the corresponding directory. Its value is `false` by default.
* The longest matching path has priority. If you have rule1 for '/a' and rule2 for '/a/b/c', rule1 applies to '/a/foo.bar' and rule2 applies to '/a/b/c/foo.bar'.
* Paths are always normalized (elimination of components) before being checked against the sandbox rules.
* `secured` defines if the directory can be accessed by in untrusted execution mode. Its value is `false` by default.

In the `sandbox` section, the `spawn` section is a collection of entries that define the system commands usable in trusted mode as a whitelist. If there is no match with the command to be executed, the execution is denied. The following rules apply:

* `path` is the directory where the command can be found. This path must of course be included in the sandbox whitelist.
* `pattern` defines the command pattern to be executed (as a regular expression). See the section above to know the syntaxes usable for regular expressions.
* `params` is an optional collection of numbers that give the list of parameters of the command that are files.
* `modes` is a collection of strings associated to the previous `params` collection, that defines if the corresponding files need read and/or write access (the strings in the collection will include "r" and/or "w" for this purpose).
* when a shellscript or a window script is executed, all the lines of the script are analyzed against the `spawn` rules before execution of the script.

The `allowConsole` parameter must be set to `true` to allow the console to operate. The console operation implies access to all the folders of the server and not only to the whitelist. To ensure this, the adxadmin software, used by the console, is not concerned by the sandbox restrictions. It is therefore important to deactivate the console during normal operations, because there is a security flaw if the flag remains set to `true`. This must only be the case during the short installation and configuration period, or when an evolution of the configuration has to be piloted by the console.

**In normal exploitation conditions, `allowConsole` must be set to `false`.**

**As there is no exception on folders that can be accessed, the following folders must be present in the whitelist table. The engine will not work properly otherwise.** The paths of these folders start with `xxxx/runtime`, which is supposed to be the path where the runtime is installed:

|  |  |
| --- | --- |
| This folder stores the configuration file and should be available for the other runtimes that access the server from the network. | ```    { "path": "xxxx/runtime/cfg",     "extensions": [ "json" ]   }  ``` |
| This folder stores a semaphore file that needs to be accessed by the process monitoring function (psadx). | ```    { "path": "xxx/V7.1/runtime/sem",     "writable": true,     "extensions": [ "map", "dat" ]   }  ``` |
| This folder stores log files of the engine and must therefore be accessible in write mode. | ```    { "path": "xxxx/runtime/tmp",     "extensions": [ "*" ]   }  ``` |

## Control process

Every time an engine function uses file access in read or write mode (with functions such as [Delfile](4gl_delfile.html), [Renamefile](4gl_renamefile.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), and [Openio](4gl_openio.html)) on a given Sage X3 server, the check is done against the configuration file installed on the right server. If the configuration file denies access to the corresponding file, the error code 27 (no access) appears.

It is possible to check the fact that a file is readable and/or writeable using the [checkpath](4gl_checkpath.html) function.

Every time a [System](4gl_system.html) command is executed in a secured Cloud environment, the rules defined in the `spawn` section are tested if the execution mode is `trusted`. If the result is unsuccessful, the error code 27 (no access) is returned. In `untrusted` mode, the error is raised anyway.

## Special characters usable in regular expressions

| Characters | Definition | Example |
| --- | --- | --- |
| \ | Escape character (must be doubled in path definitions) | **C:\\Sage\\bin** |
| [character\_list] | One of the characters in the list | **[ABC]** defines one of the characters A, B, C |
| [f-l] | One character in the range defined by the first (f) and last (l) character. | **[A-Z0-9]** defines a character that can be either an upper case letter or a digit. |
| (p1|p2|p2) | One of the patterns given in the list (here p1, p2 or p3) | **(SUB|CNS|X|Y|Z)[A-Z]\*** defines a name composed of uppercase characters starting either with SUB, CNS, X, Y or Z. |
| \* | repeats the previous pattern N times (N can be 0) | **[A-Z][A-Z0-9]\*** defines a name starting with an upper case letter followed by a variable number of characters that can be upper case letters and/or digits. |
| . | Any character | **.\*** defines N characters (N can be 0). |
| ^ | Optional marker for the beginning of the pattern | **^.\*A** defines a name that ends with an A. |
| $ | Optional marker for the end of the pattern | **.\*A$** defines a name that ends with an A. |

## Sandbox file examples

The first example here is a sandbox description that allows any system command execution. It works well but doesn't prevent execution of any harmful system command that would be allowed to the user executing the X3 process.

```
{
  "sandbox": {
    "directories": [{
      "path": "c:\\program files\\Sage X3\\runtime\\log",
      "writable": true,

      "extensions": ["log","tra"]
    }, {
      "path": "D:\\Sage_X3\\Folders",
       "extensions": ["*"]
    }, {
      "others" : "D:\\Sage_X3\\\Tmp",
      "writable": true,
      "extensions": ["*"]
    }, {
      "path": "D:\\Othervolumes",
       "volume": "A",
       "extensions": ["*"]
    }]},
  "spawn": [
        {
          "pattern": ".*",
          "path": "*"
            }
    ],         {
   "allowConsole" : false
}
```

A second more realistic example shows a complete list of possible restrictions. Here, the database used is SQL server, the operating system is Windows, and the corresponding administration commands are allowed by the whitelist filtering:

```
{
  "allowConsole": false,
  "secured": false,
  "sandbox": {
    "directories": [
      {
        "path": "D:\\Sage\Sage X3\\runtime\\cfg",
        "extensions": [
          "json"
        ]
      },
      {
        "path": "D:\\Sage\Sage X3\\runtime\\sem",
        "writable": true,
        "extensions": [
          "map",
          "dat"
        ]
      },
      {
        "path": "D:\\Sage\Sage X3\\runtime",
        "volume": "0",
        "writable": true,
        "extensions": [
          "*"
        ]
      },
      {
        "path": "D:\\Sage\Sage X3\\folders",
        "writable": true,
        "volume": "A",
        "extensions": [
          "*"
        ]
      },
      {
        "path": "D:\\Sage\Sage X3\\folders",
        "pattern": [
          "^[A-Z1-9]*/TRT/[YZ][A-Z1-9_]*\\.src$",
          "^[A-Z1-9]*/TRT/(SPE|SPV|SUBY|SUBZ|CNSY|CNSZ)[A-Z1-9_]*\\.src$",
          "^[A-Z1-9]*/TRT/[A-Z1-9_]*(_CSPE|_CSPV|_CVER)\\.src$",
          "^[A-Z1-9]*/TRT/CNS[A-Z1-9_]*SPE\\.src$",
          "^[A-Z1-9]*/STC/(C_Y|C_Z|R_Y|R_Z)[A-Z1-9_]*\\.stc$"
        ],
        "writable": "true",
        "secured": "true"
      },
      {
        "path": "D:\\Sage\Sage X3\\folders\\",
        "pattern": [
          "^[A-Z1-9]*\\\\TRA\\\\.*",
          "^[A-Z1-9]*\\\\tmp\\\\.*",
          "^[A-Z1-9]*\\\\TRT\\\\[YZ][A-Z1-9_]*\\.src$",
          "^[A-Z1-9]*\\\\TRT\\\\(SPE|SPV|SUBY|SUBZ|CNSY|CNSZ)[A-Z1-9_]*\\.src$",
          "^[A-Z1-9]*\\\\TRT\\\\[A-Z1-9_]*(_CSPE|_CSPV|_CVER)\\.src$",
          "^[A-Z1-9]*\\\\TRT\\\\CNS[A-Z1-9_]*SPE\\.src$",
          "^[A-Z1-9]*\\\\STC\\\\(C_Y|C_Z|R_Y|R_Z)[A-Z1-9_]*\\.stc$"
        ],
        "writable": true,
        "secured": true
      },
      {
        "path": "D:\\Sage\Sage X3\\runtime\\tmp",
        "writable": true,
        "extensions": [
          "*",
          ""
        ]
      }
    ],
    "spawn": [
      {
        "pattern": "^ae_echo [A-Z0-9\\.\\\\_:\\\"\\-&%]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin"
      },
      {
        "pattern": "^ae_cat [ A-Z0-9\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin",
        "params": [
          1
        ],
        "modes": "r"
      },
      {
        "pattern": "^ae_cp [ A-Z0-9\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin",
        "params": [
          1,
          2
        ],
        "modes": "rw"
      },
      {
        "pattern": "^ae_mv [ A-Z0-9\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin",
        "params": [
          1,
          2
        ],
        "modes": "ww"
      },
      {
        "pattern": "^ae_parse [ A-Z0-9\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin",
        "params": [
          2
        ],
        "modes": "r"
      },
      {
        "pattern": "^lsadx [ A-Z0-9>\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^valfil [ A-Z0-9>/\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^valtrt [ A-Z0-9>\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^valstc [ A-Z0-9>\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^archive [ A-Z0-9>\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^ae_logname$",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin"
      },
      {
        "pattern": "^ae_os$",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin"
      },
      {
        "pattern": "^ae_mkdir [ A-Z0-9\\.\\\\_:\"\\-\\/]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin"
      },
      {
        "pattern": "^lsadx.*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^adonix -v [A-Z0-9_]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^killadx [0-9]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^killadx [0-9]* >> [ A-Z0-9\\.\\\\_:\\\"\\-\\/]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^killadx.exe -e [0-9]* > [ A-Z0-9\\.\\\\_:\\\"\\-\\/]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^BREAK OFF$"
      },
      {
        "pattern": "^BREAK ON$"
      },
      {
        "pattern": "^@ECHO OFF$"
      },
      {
        "pattern": "^ae_rm [ A-Z0-9\\.\\*\\\\_:\\\"\\-]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin",
        "params": [
          1
        ],
        "modes": "w"
      },
      {
        "pattern": "^EXIT$"
      },
      {
        "pattern": "^psadx [ A-Z0-9\\-]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^adxdwhat [ A-Z0-9>\\.\\\\_:\\\"\\-&]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^ae_rmdir [ A-Z0-9\\.\\*\\\\_:\\\"]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin",
        "params": [
          1
        ],
        "modes": "w"
      },
      {
        "pattern": "^[ A-Z0-9>\\.\\\\_:\\\"\\-\\/]*adcrapora\\.bat [ A-Z0-9>\\.\\\\_:\\\"\\-\\/]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin"
      },
      {
        "pattern": "^adonix -a [ 0-9A-Z\\-:]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^set USER_ENTREP=[A-Z0-9~]*"
      },
      {
        "pattern": "^set EXEC_ENTREP=[A-Z0-9~]*"
      },
      {
        "pattern": "^set TRA_ENTREP=[A-Z0-9~]*"
      },
      {
        "pattern": "^set RQT_ENTREP=[A-Z0-9~]*"
      },
      {
        "pattern": "^sqlplus /NOLOG [A-Z0-9\\.\\\\:\\\"\\-@/]*",
        "path": "D:\\Sage\Sage X3\\runtime\\instantclient_12_1\\bin"
      },
      {
        "pattern": "^ae_parsevt [ A-Z0-9\\.\\*\\\\_:]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin"
      },
      {
        "pattern": "^adcrapss7[ A-Z0-9>\\.\\\\_:\\\"\\-@#!\\$%&'\\(\\)\\*\\+/;<=?\\[\\]\\^`{\\|}~]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin"
      },
      {
        "pattern": "^SET OSQL_EXE=osql"
      },
      {
        "pattern": "IF EXIST \\\"%SQLS7_OSQL%\\\\BINN\\\\osql.EXE\\\" SET OSQL_EXE=\\\"%SQLS7_OSQL%\\\\BINN\\\\osql.EXE\\\""
      },
      {
        "pattern": "%OSQL_EXE% -D [ A-Z0-9>\\.\\\\_:\\\"\\-@#!\\$%&'\\(\\)\\*\\+/;<=?\\[\\]\\^`{\\|}~]*"
      },
      {
        "pattern": "^meladx[ A-Z0-9>\\.\\\\_:\\\"\\-@#!\\$%&'\\(\\)\\*\\+/;<=?\\[\\]\\^`{\\|}~]*",
        "path": "D:\\Sage\Sage X3\\runtime\\bin"
      },
      {
        "pattern": "^ae_sort [ A-Z0-9\\.\\\\_:\\\"\\-]*",
        "path": "D:\\Sage\Sage X3\\runtime\\ebin"
      },
      {
        "pattern": "^dir /a:d /b [ 0-9A-Z\\\\:\\\"]*",
        "modes": "r",
            "params": [3]
      }
    ]
  }
}
```

## For further information

[Openi](4gl_openi.html)  
  
[Openo](4gl_openo.html)  
  
[Openio](4gl_openio.html)  
  
[Delfile](4gl_delfile.html)  
  
[Renamefile](4gl_renamefile.html)  
  
[System](4gl_system.html)  
  
[checkpath](4gl_checkpath.html)

  

[Index](index.html)  [Home](getting-started_home.html)