[Index](index.html)  [Home](getting-started_home.html)

X3 script keywords glossary

**The Sage X3 scripting language includes a list of keywords. Not all these keywords are used, but they remain reserved words in the language.**

# Keyword use

When a keyword exists, it is recognized as an element of the language regardless of its letter case. Otherwise, a symbol is automatically created in upper case.

For example, `For` is a keyword in the Sage X3 scripting language; therefore, you cannot use `for`, `fOr`, `foR`, `FOr`, `FoR`, `fOR` or `FOR` to define a symbol (variable, instance, class name, and so forth) in any scripting program.

Likewise, a variable called `FOO` can be spelled `foo`, `Foo`, `fOo`, `foO`, `FOo`, `FoO`, `fOO`, which represents the same variable. The script editor will automatically rewrite it `FOO`.

This will change in the future when a new policy is defined, but for now it is important to have a list of all the keywords to avoid using them inadvertently.

# Keyword status

Though deprecated, some of these keywords still exist for compatibility reasons with earlier versions.

The following tables provide lists of keywords with their status and a link to the corresponding documentation if available. for readability reasons, the deprecated and internal keywords have been put on separated tables.

The different statuses for these keywords are:

* **Deprecated Classic**: The keyword must not be used in version 7 style programming, and also in version 6 style programming for Classic mode. It must therefore be replaced in V6 code to use it in Classic mode.
* **Deprecated**: The keyword must not be used in version 7 style programming, although it can still be used in version 6. Its availability in future versions is not guaranteed.
* **Internal**: This keyword can only be used by the supervisor layers. Its use is strongly discouraged since its behavior is subject to change without notice.
* **Public**: This keyword already exists in version 6 and can be used without restrictions.
* **New**: This keyword has been introduced in version 7 and can be used without restrictions.

# Keyword lists tables description

The following tables list all keywords of the Sage X3 scripting language in version 6 with the following columns:

* The keyword name.
* The status of the keyword.
* The syntax for the keyword only described for functions that are public or new. The following letters are used in the syntax:
  + `n` represents a numeric value.
  + `d` represents a date value.
  + `i` represents an integer value.
  + `b` represents a bit value (0/1)
  + `c` represents an instance (class or representation).
  + `s` represents a character string.
  + `u` represents a logical value (0 or not 0).
  + `p` represents a parameter with an undefined or particular type.
  + `...` means that a variable number of parameters can be used.
* A short description of the purpose of the keyword if it is not internal or deprecated.

Links are available from the keyword to the detailed documentation when applicable.

# List of keywords

| [System variables or methods](#varsys) | [Instructions of the language](#instr) | [Functions of the language](#funct) |
| --- | --- | --- |

## 1. System variables or methods

### Public and new keywords

|  |  |  |
| --- | --- | --- |
| **keyword** | **Category** | **Definition or comments** |
| [adxdcs](4gl_adxdcs.html) | Public | Pivot date |
| [adxdir](4gl_adxdir.html) | Public | Directory where the runtime is installed |
| [adxdlrec](4gl_adxdlrec.html) | Public | Number of lines deleted by a "Delete Where" syntax |
| [adxfname](4gl_adxfname.html) | Public | Name of the columns in an [F] record associated with a database table |
| [adxftl](4gl_adxftl.html) | Public | Defines the cache size for database "Read" operations |
| [adxifs](4gl_adxifs.html) | Public | Field separator for sequential file operations |
| [adxirs](4gl_adxirs.html) | Public | Record separator for sequential file operations |
| [adxium](4gl_adxium.html) | Public | Character encoding option for sequential file operations |
| [adxlog](4gl_adxlog.html) | Public | Returns 1 if application is in transaction state, 0 if not. |
| [adxmda](4gl_adxmda.html) | Public | Defines the angular mode |
| [adxmother](4gl_adxmother.html) | Public | Reference folder name |
| [adxsqlrec](4gl_adxsqlrec.html) | Public | Number of lines updated by a direct SQL syntax |
| [adxtct](4gl_adxtct.html) | Public | Defines the table for counters (APLCOM) |
| [adxtlk](4gl_adxtlk.html) | Public | Defines the symbol locks table (APLLCK) |
| [adxtms](4gl_adxtms.html) | Public | Defines the messages table (APLSTD) |
| [adxuprec](4gl_adxuprec.html) | Public | Number of lines updated by an "Update" instruction in the database |
| [adxwrb](4gl_adxwrb.html) | Public | Defines the cache size for database "Writeb" operations |
| [currind](4gl_currind.html) | Public | Current index used by default on a database table |
| [currlen](4gl_currlen.html) | Public | Defines the size of the current key (see currkey) |
| [dbgmode](4gl_dbgmode.html) | Public | variable that enables or disable the ability to run the debugger. |
| [fstat](4gl_fstat.html) | Public | Returns a status (return code) of last database or sequential file operation |
| [getaccessorenabled](4gl_getaccessorenabled.html) | New | Defines if the "Get" accessor is enabled on an instance |
| [indcum](4gl_indcum.html) | Public | Current index used by default in sigma syntax |
| [isreadonly](4gl_isreadonly.html) | New | Defines if an object is "Readonly" (1) or not (0) |
| [lockwait](4gl_lockwait.html) | Public | Defines the "Wait" time in seconds for readlock |
| [nbind](4gl_nbind.html) | Public | Number of indexes defined in [G] record for a table |
| [nbzon](4gl_nbzon.html) | Public | Number of columns defined in [G] record for a table |
| [nomap](4gl_nomap.html) | Public | Current folder name |
| [reckey](4gl_reckey.html) | Public | Used to avoid an "Order by" clause in "For" instruction |
| [setaccessorenabled](4gl_setaccessorenabled.html) | New | Defines if the "Set" accessor is enabled on an instance |
| [snapshot](4gl_snapshot.html) | New | Instance storing the initial value of an instance |
| [snapshotenabled](4gl_snapshotenabled.html) | New | Property of a class defining if the snapshot is activated |
| [stat1](4gl_stat1.html) | Public | Error status or number of lines returned by System |
| [tairec](4gl_tairec.html) | Public | Record size defined in [G] record for a table |
| [this](4gl_this.html) | New | Access to the current instance in a method |
| [updtick](4gl_updtick.html) | New | Column storing the "revision number" for a database table line |

### Deprecated and internal keywords

|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| |  |  |  | | --- | --- | --- | | **keyword** | **Category** | **Definition or comments** | | actihgup | Internal |  | | adxcpw | Internal |  | | adxctx | Internal |  | | adxcus | Internal |  | | adxdbc | Internal |  | | adxdbo | Internal |  | | adxdbx | Internal |  | | adxdpg | Internal |  | | adxfmt | Internal |  | | adxgtb | Deprecated |  | | adxkpg | Deprecated |  | | adxksp | Deprecated |  | | adxlig | Deprecated |  | | adxmbm | Internal |  | | adxmpgpro | Deprecated |  | | adxmpgtrt | Deprecated |  | | adxmpr | Internal |  | | [adxmso](4gl_adxmso.html) | Internal |  | | [adxmto](4gl_adxmto.html) | Internal |  | | adxmua | Deprecated |  | | adxmxl | Deprecated |  | | adxovf | Internal |  | | adxovs | Internal |  | | adxrob | Deprecated |  | | adxsax | Internal |  | | adxsca | Internal |  | | adxses | Internal |  | | adxtrl | Internal |  | | adxtro | Internal |  | | adxtrp | Internal |  | | adxtuc | Internal |  | | adxtul | Internal |  | | adxtut | Internal |  | | adxusr | Internal |  | | ctxinfo | Deprecated |  | | currbox | Deprecated |  | | datesyst | Internal |  | | dbgduration | Internal |  | | dbgexcept | Internal |  | | dbglineoffset | Internal |  | | dbglog | Internal |  | | dbglong | Internal |  | | |  |  |  | | --- | --- | --- | | **keyword** | **Category** | **Definition or comments** | | dbgstr | Internal |  | | dclkey | Deprecated |  | | extsize | New | Defines the extent CLOB/BLOB while "Append" operation | | [fileabre](4gl_fileabre.html) | Internal |  | | [filename](4gl_filename.html) | Internal |  | | filenume | Internal |  | | indice | Deprecated |  | | isomess | Internal | Defines the language in iso form | | [keylen](4gl_keylen.html) | Deprecated | Key lengths for the different indexes described in [G] record | | [keyname](4gl_keyname.html) | Deprecated | Key names for the different indexes described in [G] record | | [keyuniq](4gl_keyuniq.html) | Deprecated | Unique index flag for the different indexes described in [G] record | | locfshost | Deprecated |  | | locfsqport | Deprecated |  | | locfsqon | Deprecated |  | | maxheap | Internal |  | | maxmem | Internal |  | | menchoix | Deprecated |  | | messname | Internal |  | | mkstat | Deprecated |  | | [nolign](4gl_Nolign.html) | Deprecated | Current line in grids in classic mode | | [nolign1](4gl_Nolign1.html) | Deprecated | Line range end for operations in classic mode | | password | Deprecated |  | | pcolor | Deprecated | For Classic, will be replaced by dedicated styles | | sadmem | Internal |  | | secmod | Deprecated |  | | [status](4gl_Status.html) | Deprecated | Input status in classic mode | | syssnapshot | Internal |  | | syssnapshotenabled | Internal |  | | titre | Deprecated |  | | [zc](4gl_Zc.html) | Deprecated |  |Current field in classic mode | [zoncou](4gl_Zoncou.html) | Deprecated | Name of the current field in classic mode | | [zonsor](4gl_Zonsor.html) | Deprecated | Name of the last entered field in classic mode | | [zonsui](4gl_Zonsui.html) | Deprecated | Next input field in classic mode | |

## 2. Language instructions

### Public and new keywords

|  |  |  |
| --- | --- | --- |
| **keyword** | **Category** | **Definition** |
| [Anasql](4gl_anasql.html) | Public | Parses an SQL instruction |
| [Append](4gl_append.html) | New | Appends a string or CLOB to a string or CLOB |
| [As](4gl_as.html) | Public | Used in several syntaxes |
| [Asc](4gl_asc.html) | Public | Ascending mode in some syntaxes |
| [Assign](4gl_assign.html) | Public | Assigns a variable given by a string value with a computed value |
| [Blbfile](4gl_blbfile.html) | Public | BLOB declaration |
| [Break](4gl_break.html) | Public | Break in "For...Next", "Repeat...Until", "While...Wend" loops |
| [By](4gl_by.html) | Public | Used in several syntaxes. See [Order By](../4gl/order-by.md) |
| [Call](4gl_call.html) | Public | Calls a subroutine |
| [Case](4gl_case.html) | Public | Defines a branch sequence based on list of values |
| [Char](4gl_char.html) | Public | String character variable declaration |
| [Clbfile](4gl_clbfile.html) | Public | CLOB variable declaration |
| [Close](4gl_close.html) | Public | Closes a database table (See [Local](../4gl/local.md) [File](../4gl/file.md)) |
| [Columns](4gl_columns.html) | Public | Defines a list of columns that will be read on a database table on "For" loops |
| [Commit](4gl_commit.html) | Public | Triggers a "Commit" of modifications done in the database |
| [Const](4gl_const.html) | Public | Declares parameters of a "Call" as a constant value |
| [Curr](4gl_curr.html) | Public | Used in different database access syntaxes (current line) |
| [Date](4gl_date.html) | Public | Date variable declaration |
| [Datetime](4gl_datetime.html) | Public | Datetime variable declaration |
| [Dbgaff](4gl_dbgaff.html) | Public | Open debugger |
| [Decimal](4gl_decimal.html) | Public | Decimal number declaration |
| [Default](4gl_default.html) | Public | Used in different syntaxes |
| [Dela](4gl_dela.html) | Public | Deletes lines in a set of variable arrays |
| [Delete](4gl_delete.html) | Public | Deletes lines in the database |
| [Deletebykey](4gl_deletebykey.html) | New | Deletes lines in the database with a control on "Updtick" |
| [Desc](4gl_desc.html) | Public | Descending mode in some syntaxes |
| [Double](4gl_double.html) | Public | Double precision floating variable declaration |
| [Else](4gl_else.html) | Public | Alternative choice in an "If" sequence |
| [Elsif](4gl_elsif.html) | Public | Alternative condition in an "If" sequence |
| [End](4gl_end.html) | Public | Ends a subprogram or a function |
| [Endcase](4gl_endcase.html) | Public | Ends a "Case" sequence |
| [Endif](4gl_endif.html) | Public | Ends an "If.. Elsif.. Else.." sequence |
| [Execsql](4gl_execsql.html) | Public | Executes an SQL order |
| [Extended](4gl_extended.html) | Public | Option Key word of [Columns](../4gl/columns.md) instruction |
| [File](4gl_file.html) | Public | Database table or view declaration |
| [Filter](4gl_filter.html) | Public | Adds a filter ("Where" clause) on a database table |
| [First](4gl_first.html) | Public | Reads the first line in different database access syntax |
| [Float](4gl_float.html) | Public | Floating point variable declaration |
| [Flush](4gl_flush.html) | Public | Flushes the "Write" buffer when using buffered database Writen b instruction |
| [Fmethod](4gl_fmethod.html) | New | Calls a method on an instance |
| [For](4gl_for.html) | Public | Loop on a set of values for a variable or on a database cursor |
| [FreeInstance](4gl_freeinstance.html) | New | Releases the memory used by an instance |
| [FreeGroup](4gl_freegroup.html) | New | Releases the memory used by a group of instances |
| [From](4gl_from.html) | Public | Used in different syntaxes |
| [Funprog](4gl_funprog.html) | Public | Function declaration |
| [Getseq](4gl_getseq.html) | Public | Reads data in a file in binary mode |
| [Global](4gl_global.html) | Public | Prefix of a declaration if the variable is in the [V] class |
| [Gosub](4gl_gosub.html) | Public | Calls a subroutine (ends with return) |
| [Goto](4gl_goto.html) | Public | Branches on a label |
| [Hint](4gl_hint.html) | Public | Used to specify hints to a database on SQL request execution |
| [If](4gl_if.html) | Public | Test sequence |
| [Insa](4gl_insa.html) | Public | Insertion of values in a list of variable arrays |
| [Instance](4gl_instance.html) | New | Declares an instance pointer |
| [Integer](4gl_integer.html) | Public | Integer variable declaration |
| [Iomode](4gl_iomode.html) | Public | Sets "Read / Write" options on sequential files |
| [Key](4gl_key.html) | Public | Used in different syntaxes |
| [Kill](4gl_kill.html) | Public | Frees a variable |
| [Last](4gl_last.html) | Public | Reads the last line in different database access syntaxes |
| [Link](4gl_link.html) | Public | Performs a "Join" between tables in a SQL cursor declaration |
| [Local](4gl_local.html) | Public | Prefix of a declaration if the variable is in the local [L] class |
| [Lock](4gl_lock.html) | Public | Locks a symbol or used as modifier in SQL syntaxes |
| [LogicClose](4gl_logicclose.html) | Public | Closes a Table declared by File in an optimized way |
| [Look](4gl_look.html) | Public | Performs a select on a database without filling the [F] buffer |
| [Method](4gl_method.html) | New | Method declaration |
| [Next](4gl_next.html) | Public | Ends a "For" loop; also used as Read mode |
| [NewInstance](4gl_newinstance.html) | New | Creation of a new instance for a given class |
| [Nohint](4gl_nohint.html) | Public | Disables default hints sent to the database in SQL queries |
| [Onerrgo](4gl_onerrgo.html) | Public | Declares a label in which a branch will be done if an error occurs |
| [Openi](4gl_openi.html) | Public | Opens a file for reading data #@ file path (to be opened on the SAFE X3 client) are no more supported |
| [Openio](4gl_openio.html) | Public | Opens a file for reading and writing data #@ file path (to be opened on the SAFE X3 client) are no more supported |
| [Openo](4gl_openo.html) | Public | Opens a file for writing data #@ file path (to be opened on the SAFE X3 client) are no more supported |
| [Order By](4gl_order-by.html) | Public | Used in different database access and sorting syntax ("Order by" option) |
| [Prev](4gl_prev.html) | Public | Reads the previous line in different database access syntaxes |
| [Putseq](4gl_putseq.html) | Public | Writes data in binary mode in a file |
| [Raz](4gl_raz.html) | Public | Fills variable with a null value |
| [Rdseq](4gl_rdseq.html) | Public | Reads data as characters string in a file |
| [Read](4gl_read.html) | Public | Reads a line from a cursor in a database |
| [Readlock](4gl_readlock.html) | Public | Sets a lock on a line on a database cursor and returns its content |
| [RenameFile](4gl_renamefile.html) | New | Renames a file |
| [Repeat](4gl_repeat.html) | Public | Starts a "Repeat..Until" loop |
| [Resume](4gl_resume.html) | Public | Ends the exception handling after an "Onerrgo" branch |
| [Return](4gl_return.html) | Public | Ends a subroutine called by "Gosub" |
| [Rewrite](4gl_rewrite.html) | Public | Updates the current line in the database |
| [Rewritebykey](4gl_rewritebykey.html) | New | Updates the current line in the database (with a condition on "Updtick") |
| [Rollback](4gl_rollback.html) | Public | Performs a rollback on the current database transaction |
| [Schar](4gl_schar.html) | Public | Declares a single char (1 byte) variable |
| [Seek](4gl_seek.html) | Public | Moves the "Read / Write" pointer in a sequential file |
| [Setlob](4gl_setlob.html) | Public | Assignment of "CLOB" values |
| [SetInstance](4gl_setinstance.html) | New | Global assignment of properties of a class |
| [Shortint](4gl_shortint.html) | Public | Declares a short integer variable |
| [Sleep](4gl_sleep.html) | Public | Suspends for a given number of seconds the execution of the current program |
| [Sorta](4gl_sorta.html) | Public | Sorts lines in a set of variable arrays |
| [Sql](4gl_sql.html) | Public | Used in several syntaxes to access database through a direct SQL statement |
| [Stability](4gl_stability.html) | Public | Option key word on "For" clause |
| [Step](4gl_step.html) | Public | Used in "For" syntaxes to define the step to increment the variable loop |
| [Subprog](4gl_subprog.html) | Public | Declares a subprogram called by "Call" |
| [System](4gl_system.html) | Public | Used by different syntaxes to execute operating system commands #@ orders (to be executed on the client) are no more supported |
| [Then](4gl_then.html) | Public | Used optionally in the "If" syntax |
| [Tinyint](4gl_tinyint.html) | New | Declaration of a small integer (0-255 range, used for bytes values). Replaces Libelle |
| [To](4gl_to.html) | Public | Used in the "For" syntax to define the end value for a variable loop |
| [Trbegin](4gl_trbegin.html) | Public | Starts a database transaction |
| [Unlock](4gl_unlock.html) | Public | Releases a logical lock |
| [Until](4gl_until.html) | Public | Ends a "Repeat... Until" sequence |
| [Update](4gl_update.html) | Public | Updates lines in a database cursor defined by a condition |
| [Using](4gl_using.html) | Public | Used in different syntaxes |
| [Uuident](4gl_uuident.html) | New | Declares a unique "ID" variable |
| [Value](4gl_value.html) | Public | Declares a parameter sent as a value in a subprogram |
| [Variable](4gl_variable.html) | Public | Declares a parameter sent as a reference in a subprogram |
| [Wend](4gl_wend.html) | Public | Ends a "While...Wend" sequence |
| [When](4gl_when.html) | Public | Used in "Case...Endcase" sequences to define a list of choices |
| [Where](4gl_where.html) | Public | Used in different database syntaxes |
| [While](4gl_while.html) | Public | Starts a "While...Wend" sequence |
| [With](4gl_with.html) | Public | Used in different syntaxes |
| [Write](4gl_write.html) | Public | Inserts a line in the database |
| [Writeb](4gl_writeb.html) | New | Buffered "Write" to database |
| [Wrseq](4gl_wrseq.html) | Public | Writes data in string mode in a file |

### Deprecated and internal keywords

The keyword present here are deprected at least for V7+ code, but some of the keyword are still usable in classic pages and are therefore documented (a link is present on these functions

|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | **keyword** | **Category** | **Definition** | | --- | --- | --- | | [Actzo](4gl_Actzo.html) | Deprecated | Activates fields in classic mode | | Additm | Deprecated |  | | Addmen | Deprecated |  | | [Affzo](4gl_Affzo.html) | Deprecated | Displays fields in classic mode | | Askui | Deprecated Classic | Access to files must be managed by the storage area management | | At | Deprecated | Used in several deprecated syntax | | Blk | Deprecated |  | | Boxact | Deprecated |  | | Boxclr | Deprecated |  | | Boxinp | Deprecated |  | | Button | Deprecated |  | | Callilog | Deprecated |  | | Calliu | Deprecated |  | | Callmet | Internal | Calls an instance method | | Callocx | Deprecated Classic |  | | Callws | Deprecated |  | | [Callui](4gl_Callui.html) | Deprecated | In Classic, the following actions are no more supported: GetFileAlways, GetFile, PutFileAlways, PutFile, FileExist, FileDelete, GetFileByCopy | | Chain | Deprecated |  | | Checkin | Internal |  | | [Chgfmt](4gl_Chgfmt.html) | Deprecated | Changes format in classic mode | | [Chgstl](4gl_Chgstl.html) | Deprecated | Changes style in classic mode | | [Chgtbk](4gl_Chgtbk.html) | Deprecated | Changes block title in classic mode | | [Chgtfd](4gl_Chgtfd.html) | Deprecated | Changes tab title in classic mode | | [Chgtzn](4gl_Chgtzn.html) | Deprecated | Changes field title in classic mode | | [Choose](4gl_Choose.html) | Deprecated | Displays a selection popup in classic mode | | Clldap | Deprecated | Closes an "ldap" connection | | CloseXml | Internal |  | | Closecom | Internal |  | | Coded | Internal |  | | Convxml | Internal |  | | Dbgattach | Internal | Open debugger | | Dbgbox | Deprecated |  | | Dbgcallstack | Internal | Gives the callstack with an XML form | | [Disable](4gl_Disable.html) | Deprecated | Disables a button in classic mode | | Discombo | Deprecated |  | | Dislbox | Deprecated |  | | Diszo | Deprecated |  | | Dlgbox | Deprecated |  | | Dspzo | Deprecated |  | | Edi | Deprecated Classic |  | | [Effzo](4gl_Effzo.html) | Deprecated | Erases fields in a mask in classic mode | | [Enable](4gl_Enable.html) | Deprecated | Enables a button in classic mode | | [Endbox](4gl_Endbox.html) | Deprecated | Displays a message box with "End" attributes in classic mode | | [Envzo](4gl_Envzo.html) | Deprecated | Forces the display of mask fields in classic mode | | [Errbox](4gl_Errbox.html) | Deprecated | Displays an error box in classic mode | | Execws | Deprecated |  | | Extern | Deprecated |  | | Field | Deprecated |  | | Fillbox | Deprecated |  | | Folder | Deprecated |  | | Formula | Deprecated |  | | GetFirstChild | Internal |  | | GetNextChild | Internal |  | | GetLastChild | Internal |  | | GetFirstChildByName | Internal |  | | GetNextChildByName | Internal |  | | GetLastChildByName | Internal |  | | GetNbChild | Internal |  | | GetChildByName | Internal |  | | GetChildByType | Internal |  | | GetRootElement | Internal |  | | GetParent | Internal |  | | | **keyword** | **Category** | **Definition** | | --- | --- | --- | | Getui | Deprecated |  | | [Grizo](4gl_Grizo.html) | Deprecated | Disables an entry field in classic mode | | Hlpbox | Deprecated |  | | Image | Deprecated |  | | [Infbox](4gl_Infbox.html) | Deprecated | Displays an information box in classic mode | | Infimg | Deprecated |  | | Inftxt | Deprecated |  | | Inpbox | Deprecated |  | | Insli | Deprecated |  | | Inter | Internal |  | | Invfol | Deprecated |  | | Leftbox | Deprecated |  | | Libelle | Deprecated, replaced by [Tinyint](../4gl/tinyint.md) | Byte variable declaration (also used for enumerations) | | Listbox | Deprecated |  | | Listimp | Deprecated |  | | [Mask](4gl_Mask.html) | Deprecated | Mask declaration in classic mode | | Maxrows | Deprecated |  | | Men | Deprecated |  | | Mesbox | Deprecated |  | | Method | Internal | Declaration of a method | | Nap | Deprecated |  | | Nointer | Internal |  | | Nxldap | Deprecated |  | | Nxt | Deprecated |  | | Onevent | Deprecated |  | | Onintgo | Internal |  | | Onkey | Deprecated |  | | Opadxd | Internal |  | | Opldap | Internal |  | | Opsock | Internal |  | | Pick | Deprecated |  | | Pickbox | Deprecated |  | | Pikltb | Deprecated |  | | Pokltb | Deprecated |  | | Pmt | Deprecated Classic | Replaced by the Eclipse Editor | | [Qstbox](4gl_Qstbox.html) | Deprecated | Displays a question box in classic mode | | Reb | Deprecated |  | | Report | Internal |  | | Rptstat | Internal |  | | Rptfile | Internal |  | | Run | Internal |  | | Saizo | Deprecated |  | | Saxparse | Internal |  | |  | Deprecated | Displays a selection box in classic mode | | Seldest | Deprecated Classic |  | | Selimp | Deprecated |  | | Send | Deprecated Classic |  | | Setcod | Deprecated |  | | Setfct | Internal |  | | Setgus | Internal |  | | Setlbox | Deprecated |  | | Setmdu | Internal |  | | Setmode | Deprecated |  | | Setmok | Deprecated |  | | Sized | Deprecated |  | | Srldapbs | Deprecated |  | | Srldaplv | Deprecated |  | | Srldaptr | Deprecated |  | | Ssl | Deprecated |  | | Starting | Deprecated |  | | Supli | Deprecated |  | | Syrrecv | Internal |  | | Syrsend | Internal |  | | Throwerr | Deprecated |  | | Timeval | Deprecated |  | | [Titcol](4gl_Titcol.html) | Deprecated | Changes the title of a column in classic mode | | Titled | Deprecated |  | | Transmask | Deprecated |  | | Treebox | Deprecated |  | | Vbcall | Deprecated |  | | [Wrnbox](4gl_Wrnbox.html) | Deprecated | Displays a warning box in classic mode | |

## 3. Functions of the language

### Public and new keywords

|  |  |  |  |
| --- | --- | --- | --- |
| **keyword** | **Category** | **Syntax** | **Definition** |
| [abs](4gl_abs.html) | Public | n=abs(n) | Absolute value function |
| [ach](4gl_ach.html) | Public | n=ach(n) | Inverse hyperbolic cosine |
| [acos](4gl_acos.html) | Public | n=acos(n) | Inverse cosine |
| [addmonth](4gl_addmonth.html) | Public | d=addmonth(d,n) | Adds months to a date |
| [adxmac](4gl_adxmac.html) | Public | s=adxmac(i) | Returns name of the servers |
| [adxpno](4gl_adxpno.html) | Public | s=adxpno(i) | Returns the stack of the calling scripts |
| [adxseek](4gl_adxseek.html) | Public | i=adxseek(p) | "Read / Write" pointer on a file |
| [adxtcp](4gl_adxtcp.html) | Public | i=adxtcp() | Returns the connection port |
| [adxuid](4gl_adxuid.html) | Public | i=adxiud(i) | Unique session identifier |
| [allocgrp](4gl_allocgrp.html) | New | s=c.allocgrp | Allocation group for an instance |
| [and](4gl_and.html) | Public | l=n and n | Logical "And" |
| [anp](4gl_anp.html) | Public | i=anp(i,i) | Ordered arrangements (statistical function) |
| [ar2](4gl_ar2.html) | Public | n=ar2(n) | Rounding to two digits |
| [arr](4gl_arr.html) | Public | n=arr(n,n) | Rounding |
| [ascii](4gl_ascii.html) | Public | i=ascii(s) | ASCII code of first char in a string |
| [ash](4gl_ash.html) | Public | n=ash(n) | Inverse hyperbolic sine |
| [asin](4gl_asin.html) | Public | n=asin(n) | Inverse sine |
| [atan](4gl_atan.html) | Public | n=atan(n) | Inverse tangent |
| [atan2](4gl_atan2.html) | Public | n=atan2(n,n) | Inverse tangent of a slope |
| [ath](4gl_ath.html) | Public | n=ath(n) | Inverse hyperbolic tangent |
| [avg](4gl_avg.html) | Public | n=avg(p) | Average value of a list of numeric values |
| [aweek](4gl_aweek.html) | Public | d=aweek(i,i) | First day of a week in a year |
| [b64encode](4gl_b64encode.html) | New | i=b64encode(s,s) | Base 64 encoding of a string |
| [b64decode](4gl_b64decode.html) | New | i=b64decode(s,s) | Base 64 decoding of a string |
| [cast](4gl_cast.html) | New | c=cast(c,s) | Forces a class pointer type |
| [ch](4gl_ch.html) | Public | n=ch(n) | Hyperbolic cosine |
| [checkpath](4gl_checkpath.html) | New | i=checkpath(s,i) | checks the path validity against engine sandbox rules |
| [chr$](4gl_chr$.html) | Public | s=chr$(i) | Character from ASCII code |
| [clalev](4gl_clalev.html) | Public | i=clalev(p) | Level value for a variable class |
| [clanam](4gl_clanam.html) | Public | s=clanam(p) | Variable class name |
| [clanbs](4gl_clanbs.html) | Public | i=clanbs(p) | Variable class number of variables |
| [clasiz](4gl_clasiz.html) | Public | i=clasiz(p) | Size of a variable class |
| [clavar](4gl_clavar.html) | Public | s=clavar(p,i) | Name of a variable in a variable class |
| [clacmp](4gl_clacmp.html) | Public | i=clacmp(p,p) | Compares two variable classes |
| [closelog](4gl_closelog.html) | Public | i=closelog() | Closes the log file |
| [cnp](4gl_cnp.html) | Public | i=cnp(i,i) | Combinations (statistical function) |
| [cos](4gl_cos.html) | Public | n=cos(n) | Cosine |
| [ctrans](4gl_ctrans.html) | Public | s=ctrans(s...) | String character substitutions |
| [date$](4gl_date$.html) | Public | d=date$ | Current date |
| [datetime$](4gl_datetime$.html) | New | dt=datetime$ | Current date/time |
| [day](4gl_day.html) | Public | i=day(d) | Current day |
| [day$](4gl_day$.html) | Public | day$(p) | Name of the day in a week |
| [dayn](4gl_day$.html) | Public | dayn(d) | Number of the day in a week |
| [delfile](4gl_delfile.html) | Public | i=delfile(s) | Deletes a file in a file system |
| [dim](4gl_dim.html) | Public | i=dim(p...) | Dimensions of variable arrays |
| [dir$](4gl_dir$.html) | Public | s=dir$ | Directory where the runtime is installed |
| [eomonth](4gl_eomonth.html) | Public | d=eomonth(d) | Last day of a month |
| [errl](4gl_errl.html) | Public | i=errl | Line number in a script when an error occurs |
| [errm](4gl_errm.html) | Public | s=errm | Error message details |
| [errmes$](4gl_errmes$.html) | Public | s=errmes$(i) | Translatable error message |
| [errn](4gl_errn.html) | Public | i=errn | Error number |
| [errp](4gl_errp.html) | Public | s=errp | Error program |
| [escjson](4gl_escjson.html) | Public | s=escjson(s) | Character escaping function for "JSON" constants |
| [evalue](4gl_evalue.html) | Public | p=evalue(s) | Evaluation of an expression |
| [evaluesdata](4gl_evaluesdata.html) | Public | p=evaluesdata(s,p,p) | Evaluation of a "Sdata" expression |
| [exp](4gl_exp.html) | Public | n=exp(n) | Exponential function |
| [filexist](4gl_filexist.html) | Public | i=filexist(s,s,s) | Existence of a file |
| [fac](4gl_fac.html) | Public | i=fac(i) | Factorial function |
| [filinfo](4gl_filinfo.html) | Public | i=filifo(s,i) | Access to file information |
| [filpath](4gl_filpath.html) | Public | s=filpath(s...) | File path construction function |
| [find](4gl_find.html) | Public | i=find(p...) | Finds the first occurrence of a value in a list |
| [fix](4gl_fix.html) | Public | i=fix(n) | Integer truncation |
| [fmet](4gl_fmet.html) | New | p=fmet c.METHOD | Calls a method on an instance |
| [format$](4gl_format$.html) | Public | s=format$(s,p) | Formats a value according to a format description |
| [freeheap](4gl_freeheap.html) | Public | n=freeheap | Gives free memory available in the object heap |
| [freemem](4gl_freemem.html) | Public | n=freemem | Gives free memory in the common memory segment |
| [freesnapshot](4gl_freesnapshot.html) | New | i=c.freesnapshot | Method that frees a snapshot |
| [func](4gl_func.html) | Public | p=func FUNCTION(p) | Calls a function |
| [gdat$](4gl_gdat$.html) | Public | d=gdat$(i,i,i) | Constructs a date from day, month, year |
| [gdatetime$](4gl_gdatetime$.html) | Public | dt=gdatetime$(s) | Constructs a datetime from a string |
| [getBit](4gl_getbit.html) | Public | b=getbit(i,i) | Extracts out of an integer the value of the bit in the rank i |
| [getenv$](4gl_getenv$.html) | Public | s=getenv(s) | Access to variable environment values |
| [getlogname](4gl_getlogname.html) | Public | s=getlogname | Returns the engine log file |
| [getmodified](4gl_getmodified.html) | New | i=c.getmodified(p...) | Access to modified properties in an instance |
| [Getuuid](4gl_getuuid.html) | New | u=getuuid | Returns a UUID |
| [heapdmp](4gl_heapdmp.html) | Public | s=heapdmp | Generates a memory ump file |
| [instr](4gl_instr.html) | Public | i=instr(i,s,s) | First occurrence of a substring in a string from a position |
| [int](4gl_int.html) | Public | i=int(n) | Integer value function |
| [left$](4gl_left$.html) | Public | s=left$(s,i) | Left part of a string |
| [len](4gl_len.html) | Public | i=len(s) | Length of a string |
| [ln](4gl_ln.html) | Public | n=ln(n) | e-based logarithm |
| [lobsize](4gl_lobsize.html) | Public | n=lobsize(s) | Gives the real size of a LOB |
| [log](4gl_log.html) | Public | n=log(n) | 10 based logarithm |
| [max](4gl_max.html) | Public | p=max(p...) | Maximum value in a list |
| [maxtab](4gl_maxtab.html) | New | i=maxtab(p) | Maximum index in a variable length array |
| [mess](4gl_mess.html) | Public | s=mess(i...) | Translatable messages |
| [mid$](4gl_mid$.html) | Public | s=mid$(s,i,i) | Extracts a substring of a string |
| [min](4gl_min.html) | Public | p=min(p...) | Minimum value in a list |
| [mod](4gl_mod.html) | Public | i=mod(n,i) | Modulus function |
| [modified](4gl_modified.html) | New | l=p.modified | Checks if a property of an instance has been modified |
| [month](4gl_month.html) | Public | i=month(d) | Extracts the month number of a date |
| [month$](4gl_month$.html) | Public | s=month$(d) | Returns the month name from a date |
| [nbrecord](4gl_nbrecord.html) | Public | i=nbrecord(p) | Returns count(\*) on a database table or cursor |
| [nday](4gl_nday.html) | Public | i=nday(d) | Returns a number of days from a date |
| [nday$](4gl_nday$.html) | Public | d=nday(i) | Returns a date from a number of days |
| [NewInstance](4gl_newinstance.html) | New | c=Newinstance... | Creates an instance in memory |
| [not](4gl_not.html) | Public | l=not n | Logical negation |
| [Null](4gl_null.html) | New | c=Null | Returns a null instance pointer |
| [Nulluuid](4gl_nulluuid.html) | New | u=Nulluuid | Returns a null UUID |
| [num$](4gl_num$.html) | Public | s=num$(n) | string Decimal representation of a number |
| [objectexist](4gl_objectexist.html) | Public | n=objectexist(s) | Gives information if the object exists or not |
| [objectnbs](4gl_objectnbs.html) | Public | n=objectnbs(c) | Gives the number of property of an instance |
| [objecttype](4gl_objecttype.html) | Public | s=objecttyp(c) | Gives the number of string type of an instance |
| [objectvar](4gl_objectvar.html) | Public | s=objectvar(c) | Gives the "n" property of an instance |
| [openlog](4gl_openlog.html) | Public | i=openlog(i) | Opens a log file for the engine |
| [or](4gl_or.html) | Public | l=n or n | Logical "Or" |
| [parse](4gl_parse.html) | Public | i=parse(s) | Parses a string containing a Sage X3 script expression |
| [pat](4gl_pat.html) | Public | l=pat(s,s) | Checks the conformity of a string against a pattern |
| [pi](4gl_pi.html) | Public | n=pi | "pi" rounded to 32 digits precision (3.14159265358979323846264338328) |
| [prd](4gl_prd.html) | Public | n=prd(n...) | Product of a list of numeric values |
| [renamefile](4gl_renamefile.html) | New | n=renamefile(s,s) | Renames a file |
| [reverttosnapshot](4gl_reverttosnapshot.html) | New | i=c.reverttosnapshot | Reassigns a class with the snapshot values |
| [revertupdtick](4gl_revertupdtick.html) | New | i=c.revertupdtick | Reassigns a class hierarchy with the "Updtick" values from snapshot |
| [right$](4gl_right$.html) | Public | s=right$(s,i) | Right part of a string |
| [rnd](4gl_rnd.html) | Public | n=rnd(n) | Returns a random number between 0 and x |
| [rowcount](4gl_rowcount.html) | Public | n=rowcount(p) | Performs count(\*) on a filtered database table |
| [seg$](4gl_seg$.html) | Public | s=seg$(s,i,i) | Extracts a substring of a string |
| [setBit](4gl_setbit.html) | Public | i=setbit(i,i,b) | Sets the one of the bits of an integer to a given value |
| [sgn](4gl_sgn.html) | Public | i=sgn(n) | Returns the sign (+1/-1) of a number |
| [sh](4gl_sh.html) | Public | n=sh(n) | Hyperbolic sine function |
| [sigma](4gl_sigma.html) | Public | p=sigma(p...) | Performs a sum on expressions based on an index value |
| [sin](4gl_sin.html) | Public | n=sin(n) | Sine function |
| [space$](4gl_space$.html) | Public | s=space$(i) | Returns a string filled with a given number of spaces |
| [sqr](4gl_sqr.html) | Public | n=sqr(n) | Square root function |
| [strdecode](4gl_strdecode.html) | New | s=strdecode(s,s,i) | Decodes a string format to get ab UCS2 encoded string |
| [strencode](4gl_strencode.html) | New | s=strencode(s,s,i) | Encodes a UCS2 encoded string to another format |
| [string$](4gl_string$.html) | Public | s=string$(i,p) | Returns a string filled with a repeated character or character sequence |
| [sum](4gl_sum.html) | Public | p=sum(p...) | Performs a sum on a list of values |
| [tan](4gl_tan.html) | Public | n=tan(n) | Tangent function |
| [th](4gl_th.html) | Public | n=th(n) | Hyperbolic tangent function |
| [time](4gl_time.html) | Public | n=time | Returns the number of second elapsed since the beginning of the day |
| [time$](4gl_time$.html) | Public | s=time$ | Returns a string giving the current time on the server |
| [timestamp$](4gl_timestamp$.html) | Public | s=timestamp$ | Returns a string containing the digital representation of a time stamp |
| [tolower](4gl_tolower.html) | Public | s=tolower(s) | Transforms the upper case characters in a string into lower case |
| [toSData](4gl_tosdata.html) | Public | s=toSData(s,s,s) | Transforms an X3 where sentence in a valid SData expression |
| [toupper](4gl_toupper.html) | Public | s=toupper(s) | Transforms the lower case characters in a string into upper case |
| [touuid](4gl_touuid.html) | New | s=touuid(u) | Transforms a string representation of a "UUID" into a "UUID" |
| [trtcou](4gl_trtcou.html) | Public | s=trtcou | Returns the name of the current executed Sage X3 script file |
| [type](4gl_type.html) | Public | i=type(p) | Returns the type of a variable |
| [unescjson](4gl_unescjson.html) | Public | s=unescjson(s) | Character un-escaping function for "JSON" constants |
| [uni](4gl_uni.html) | Public | i=uni(p...) | Returns the first occurrence of a duplicate value in a list of values |
| [uniqid](4gl_uniqid.html) | Public | i=uniqid(p) | Returns a sequence unique value for a database table |
| [uuid$](4gl_getuuid.html) | New | u=uuid$ | Returns an unique "id" (UUID format), same as "Getuuid" |
| [val](4gl_val.html) | Public | n=val(s) | Returns a numeric value from a string containing a decimal representation |
| [var](4gl_var.html) | Public | n=var(n,n,n,...) | Gives the variance of several arguments |
| [ver$](4gl_ver$.html) | Public | s=ver$(i) | Returns a revision number |
| [vireblc](4gl_vireblc.html) | Public | s=vireblc(s,i) | Space cleaning of a string (leading, trailing, consecutive...) |
| [week](4gl_week.html) | Public | i=week(d) | Returns the week number from a date |
| [xgetchar](4gl_xgetchar.html) | New | s=xgetchar(s,i) | Extracts a character from a string |
| [xor](4gl_xor.html) | Public | l=n xor n | Logical exclusive "Or" |
| [year](4gl_year.html) | Public | i=year(d) | Extracts the date from a year |

### Deprecated and internal keywords

|  |  |  |  |
| --- | --- | --- | --- |
| **keyword** | **Category** | **Syntax** | **Definition** |
| adxcio | Internal |  |  |
| adxioa | internal |  |  |
| adxnfs | Internal |  |  |
| adxpam | Deprecated |  |  |
| adxpid | Internal |  |  |
| adxtyp | Internal | i=adxtyp( ) |  |
| clactxnbs | Internal |  |  |
| clactxvar | Internal |  |  |
| callstack | Internal | S=callstack(i) |  |
| clone | Internal | c=c.clone | Clones an instance |
| cop$ | Deprecated |  |  |
| dbgbreakpointadd | Internal |  |  |
| dbgbreakpointget | Internal |  |  |
| dbgbreakpointlist | Internal |  |  |
| Dbgbreakpointremove | Internal |  |  |
| Dbgbreakpointupdate | Internal |  |  |
| dbgevalue | Internal |  |  |
| dbgevalue2 | Internal |  |  |
| dimctx | Internal | n=dimctx(s,n) |  |
| entete | Deprecated |  |  |
| errnremote | Internal | s=errnremote |  |
| filcom | Internal |  |  |
| filecla | Internal |  |  |
| filelev | Internal |  |  |
| filetyp | Internal |  |  |
| freesyssnapshot | Internal |  |  |
| funciu | Deprecated |  |  |
| getsysmodified | Internal |  |  |
| graph$ | Deprecated |  |  |
| inpmode | Deprecated |  |  |
| IsOpenAdxd | Internal |  |  |
| jsonproto | Internal |  |  |
| maskabr | Deprecated |  |  |
| maskcla | Deprecated |  |  |
| maskcou | Deprecated |  |  |
| masklev | Deprecated |  |  |
| masknam | Deprecated |  |  |
| masknbf | Deprecated |  |  |
| maskrk | Deprecated |  |  |
| masksiz | Deprecated |  |  |
| nbruser | Internal | n=nbruser() |  |
| progcan | Internal | s=progcan(n ) |  |
| progldd | Internal | n=progldd(n) |  |
| progsiz | Internal | n=progldd(n) |  |
| progusd | Internal | n=progusd(n) |  |
| pushscript | Internal | n=pushscript(s) |  |
| pullobject | Internal | n=pullobject(s) |  |
| pullscript | Internal | n=pullscript(s) |  |
| reverttosyssnaphot | Internal | i=c.reverttosyssnapshot |  |
| sysmodified | Internal |  |  |
| tab$ | Deprecated |  |  |
| typectx | Internal | i=typctx(s,n) |  |
| varinit | Deprecated |  |  |
| varmode | Deprecated |  |  |

  

[Index](index.html)  [Home](getting-started_home.html)