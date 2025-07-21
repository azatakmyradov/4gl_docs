[Index](index.html)  [Home](getting-started_home.html)

Glossary

The Sage X3 script glossary documents the language elements of the Sage X3 scripting engine. Every language element has an associated keyword. A keyword cannot be used as a variable or property name, whenever the case is the same or not. The keyword recognition is not case sensitive, but this will change in the future.

For instance, as `For` is a keyword of the language, `FOR`, `FoR`, `fOR`, `FOr`, `fOr`, `foR` and `for` variables are not allowed.

For a complete list of keywords, see [Sage X3 Script Keywords Glossary](4gl_x3script-keywords-glossary.html).

To describe the language, this documentation includes four categories of documents:

# Concepts

* [Updtick management](4gl_glossary-updtick.html)
* [UUID](4gl_glossary-uuid.html)
* [Datetime definition](4gl_glossary-datetime.html)
* [Structure definition](4gl_glossary-structure.html)
* [Snapshot definition](4gl_glossary-snapshot.html)
* [Engine Error list](4gl_engine-error-list.html)

# Functions [A](#funa)[B](#funb)[C](#func)[D](#fund)[E](#fune)[F](#funf)[G](#fung)[H](#funh)[L](#funl)[M](#funm)[N](#funn)[O](#funo)[P](#funp)[R](#funr)[S](#funs)[T](#funt)[U](#funu)[V](#funv)[W](#funw)[X](#funx)[Y](#funy)

---  
\* [abs](4gl_abs.html) : absolute value of a number  
\* [ach](4gl_ach.html): Inverse hyperbolic cosine  
\* [acos](4gl_acos.html) : arc cosine computation  
\* [addmonth](4gl_addmonth.html) : Adds months to a date  
\* [adxmac](4gl_adxmac.html) : Returns name of the servers  
\* [adxpno](4gl_adxpno.html): Returns the stack of the calling scripts  
\* [adxseek](4gl_adxseek.html) : "Read / Write" pointer on a file  
\* [adxtcp](4gl_adxtcp.html) : Returns the connection port  
\* [adxuid](4gl_adxuid.html) : Unique session identifier  
\* [allocgrp](4gl_allocgrp.html) : Allocation group for an instance  
\* [and](4gl_and.html) : Logical "And"  
\* [anp](4gl_anp.html) : Ordered arrangements (statistical function)  
\* [ar2](4gl_ar2.html) : Rounding to two digits  
\* [arr](4gl_arr.html) : Rounding  
\* [ascii](4gl_ascii.html) : ASCII code of first char in a string  
\* [ash](4gl_ash.html) : Inverse hyperbolic sine  
\* [asin](4gl_asin.html) : arc sine computation  
\* [atan](4gl_atan.html) : arc tangent computation  
\* [atan2](4gl_atan2.html) : arc tangent for a quotient  
\* [ath](4gl_ath.html) : Inverse hyperbolic tangent  
\* [avg](4gl_avg.html) : average value of a list of numeric elements  
\* [aweek](4gl_aweek.html) : First day of a week in a year  
---  
\* [B64Decode](4gl_b64decode.html) : base 64 decoding  
\* [B64Encode](4gl_b64encode.html) : base 64 encoding  
---  
\* [cast](4gl_cast.html) : cast of a generic instance pointer  
\* [ch](4gl_ch.html) : Hyperbolic cosine  
\* [checkpath](4gl_checkpath.html) : checks the path validity against engine sandbox rules  
\* [chr$](4gl_chr$.html) : Character from ASCII code  
\* [clalev](4gl_clalev.html) : Level value for a variable class  
\* [clanam](4gl_clanam.html) : Variable class name  
\* [clanbs](4gl_clanbs.html) : Variable class number of variables  
\* [clasiz](4gl_clasiz.html) : Size of a variable class  
\* [clavar](4gl_clavar.html) : Name of a variable in a variable class  
\* [clacmp](4gl_clacmp.html) : Compares two variable classes  
\* [closelog](4gl_closelog.html) : closes the engine log  
\* [cnp](4gl_cnp.html) : Combinations (statistical function)  
\* [cos](4gl_cos.html) : cosine computation  
\* [ctrans](4gl_ctrans.html) : String character substitutions  
---  
\* [date$](4gl_date$.html) : gets the current date  
\* [datetime$](4gl_datetime$.html) : gets the current date and time  
\* [day](4gl_day.html) : Current day  
\* [day$](4gl_day$.html) : Name of the day in a week  
\* [dayn](4gl_day$.html) : Number of the day in a week  
\* [delfile](4gl_delfile.html) : Deletes a file in a file system  
\* [dim](4gl_dim.html) : Dimensions of variable arrays  
\* [dir$](4gl_dir$.html) : Directory where the runtime is installed  
---  
\* [eomonth](4gl_eomonth.html) : Last day of a month  
\* [errl](4gl_errl.html) : Line number in a script when an error occurs  
\* [errm](4gl_errm.html) : Error message details  
\* [errmes$](4gl_errmes$.html) : Translatable error message  
\* [errn](4gl_errn.html) : Error number  
\* [errp](4gl_errp.html) : Error program  
\* [escjson](4gl_escjson.html) : Character escaping function for "JSON" constants  
\* [evalue](4gl_evalue.html) : Evaluation of an expression  
\* [evalueSData](4gl_evaluesdata.html) : evaluation of SData conditions in database queries  
\* [exp](4gl_exp.html) : Exponential function  
---  
\* [filexist](4gl_filexist.html) : Existence of a file  
\* [fac](4gl_fac.html) : Factorial function  
\* [filinfo](4gl_filinfo.html) : Access to file information  
\* [filexist](4gl_filexist.html) : checks the existence of a file  
\* [filpath](4gl_filpath.html) : Path builder for files on X3 servers  
\* [find](4gl_find.html) : Finds the first occurrence of a value in a list  
\* [fix](4gl_fix.html) : Integer truncation  
\* [fmet](4gl_fmet.html) : Call of a method  
\* [format$](4gl_format$.html) : Formats a value according to a format description  
\* [freeheap](4gl_freeheap.html) : Gives free memory available in the object heap  
\* [freemem](4gl_freemem.html) : Gives free memory in the common memory segment  
\* [freesnapshot](4gl_freesnapshot.html) : Method that frees a snapshot  
\* [func](4gl_func.html) : Calls a function  
---  
\* [gdat$](4gl_gdat$.html) : Constructs a date from day, month, year  
\* [gdatetime$](4gl_gdatetime$.html) : transforms a string canonical date / time value to a datetime  
\* [getBit](4gl_getbit.html) : Extracts out of an integer the value of the bit in the rank i  
\* [getenv$](4gl_getenv$.html) : Access to variable environment values  
\* [getlogname](4gl_getlogname.html) : returns the engine log file name  
\* [getmodified](4gl_getmodified.html) : returns the list of modified properties on an instance  
\* [Getuuid](4gl_getuuid.html) : returns a unique id (UUID)  
---  
\* [Heapdmp](4gl_heapdmp.html) : Dumps the memory allocation for classes  
---  
\* [instr](4gl_instr.html) : First occurrence of a substring in a string from a position  
\* [int](4gl_int.html) : Integer value function  
---  
\* [left$](4gl_left$.html) : Left part of a string  
\* [len](4gl_len.html) : Length of a string  
\* [ln](4gl_ln.html) : e-based logarithm  
\* [lobsize](4gl_lobsize.html) : Gives the real size of a LOB  
\* [log](4gl_log.html) : 10 based logarithm  
---  
\* [max](4gl_max.html) : maximum of a list of values  
\* [maxtab](4gl_maxtab.html) : Maximum index in a variable length array  
\* [mess](4gl_mess.html) : Translatable messages  
\* [mid$](4gl_mid$.html) : Extracts a substring of a string  
\* [min](4gl_min.html) : minimum of a list of values  
\* [mod](4gl_mod.html) : Modulus function  
\* [modified](4gl_modified.html) : Checks if a property of an instance has been modified  
\* [month](4gl_month.html) : Extracts the month number of a date  
\* [month$](4gl_month$.html) : Returns the month name from a date  
---  
\* [nbrecord](4gl_nbrecord.html) : Returns count(*) on a database table or cursor  
\* [nday](4gl_nday.html) : Returns a number of days from a date  
\* [nday$](4gl_nday$.html) : Returns a date from a number of days  
\* [NewInstance](4gl_newinstance.html) : Creates an instance in memory  
\* [not](4gl_not.html) : Logical negation  
\* [null](4gl_null.html) : returns a null instance pointer  
\* [Nulluuid](4gl_nulluuid.html) : returns a null UUID  
\* [num$](4gl_num$.html) : string Decimal representation of a number  
---  
\* [objectexist](4gl_objectexist.html) : checks if a given class exists on a folder  
\* [objectnbs](4gl_objectnbs.html) : Gives the number of property of an instance  
\* [objecttype](4gl_objecttype.html) : Gives the name of the class associated to an instance  
\* [objectvar](4gl_objectvar.html) : Gives the "n" property of an instance  
\* [openlog](4gl_openlog.html) : sets the engine in a log mode  
\* [or](4gl_or.html) : Logical "Or"  
---  
\* [parse](4gl_parse.html) : Parses a string containing a Sage X3 script expression  
\* [pat](4gl_pat.html) : Checks the conformity of a string against a pattern  
\* [pi](4gl_pi.html) : "pi" rounded to 32 digits precision (3.14159265358979323846264338328)  
\* [prd](4gl_prd.html) : multiplication of a list of values  
---  
\* [renamefile](4gl_renamefile.html) : Renames a file  
\* [reverttosnapshot](4gl_reverttosnapshot.html) : Reassigns a class with the snapshot values  
\* [revertupdtick](4gl_revertupdtick.html) : Reassigns a class hierarchy with the "Updtick" values from snapshot  
\* [right$](4gl_right$.html) : Right part of a string  
\* [rnd](4gl_rnd.html) : Returns a random number between 0 and x  
\* [rowcount](4gl_rowcount.html) : Performs count(*) on a filtered database table  
---  
\* [seg$](4gl_seg$.html) : Extracts a substring of a string  
\* [setBit](4gl_setbit.html) : Sets one of the bits of an integer to a given value (0 or 1)  
\* [sgn](4gl_sgn.html) : Returns the sign (+1/-1) of a number  
\* [sh](4gl_sh.html) : Hyperbolic sine function  
\* [sigma](4gl_sigma.html) : Performs a sum on expressions based on an index value  
\* [sin](4gl_sin.html) : sine computation  
\* [space$](4gl_space$.html) : Returns a string filled with a given number of spaces  
\* [sqr](4gl_sqr.html) : Square root function  
\* [strDecode](4gl_strdecode.html) : UTF8 to UCS2 character encoder  
\* [strEncode](4gl_strencode.html) : UCS2 to UTF8 character encoder  
\* [string$](4gl_string$.html) : Returns a string filled with a repeated character or character sequence  
\* [sum](4gl_sum.html) : sum or concatenation of a list of values  
---  
\* [tan](4gl_tan.html) : tangent computation  
\* [th](4gl_th.html) : Hyperbolic tangent function  
\* [time](4gl_time.html) : Returns the number of second elapsed since the beginning of the day  
\* [time$](4gl_time$.html) : Returns a string giving the current time on the server  
\* [timestamp$](4gl_timestamp$.html) : Returns a string containing the digital representation of a time stamp  
\* [tolower](4gl_tolower.html) : Transforms the upper case characters in a string into lower case  
\* [toSData](4gl_tosdata.html) : transforms a X3 where clause in a SData sentence  
\* [toupper](4gl_toupper.html) : Transforms the lower case characters in a string into upper case  
\* [Touuid](4gl_touuid.html) : conversion of a canonical string UUID representation to a UUID  
\* [trtcou](4gl_trtcou.html) : Returns the name of the current executed Sage X3 script file  
\* [type](4gl_type.html) : returns the data type of a variable  
---  
\* [unescjson](4gl_unescjson.html) : replaces a JSON escaped character string by its character value  
\* [uni](4gl_uni.html) : Returns the first occurrence of a duplicate value in a list of values  
\* [uniqid](4gl_uniqid.html) : Returns a sequence unique value for a database table  
\* [uuid$](4gl_uuid$.html) : Returns a unique "id" in canonical (string) format  
---  
\* [val](4gl_val.html) : Returns a numeric value from a string containing a decimal representation  
\* [var](4gl_var.html) : Gives the variance of several arguments  
\* [ver$](4gl_ver$.html) : Returns a revision number  
\* [vireblc](4gl_vireblc.html) : Space cleaning of a string (leading, trailing, consecutive...)  
---  
\* [week](4gl_week.html) : Returns the week number from a date  
---  
\* [Xgetchar](4gl_xgetchar.html) : extracts one character from string or clob value  
\* [xor](4gl_xor.html) : Logical exclusive "Or"  
---  
\* [year](4gl_year.html) : Extracts the date from a year

# Instructions [A](#insa)[B](#insb)[C](#insc)[D](#insd)[E](#inse)[F](#insf)[G](#insg)[H](#insh)[I](#insi)[K](#insk)[L](#insl)[M](#insm)[N](#insn)[O](#inso)[P](#insp)[R](#insr)[S](#inss)[T](#inst)[U](#insu)[V](#insv)[W](#insw)

---  
\* [Anasql](4gl_anasql.html) : Parses an SQl sentence  
\* [Append](4gl_append.html) : Append a string or a clob to another clob  
\* [As](4gl_as.html) : used in different syntaxes  
\* [Asc](4gl_asc.html): ascending order for [Sorta](4gl_sorta.html) syntax and [Order By](4gl_order-by.html) syntax  
\* [Assign](4gl_assign.html) : Assign a variable which name is evaluated  
---  
\* [Blbfile](4gl_blbfile.html) : Declaration of a large binary object (Blob) variable  
\* [Break](4gl_break.html) : Break in "For...Next", "Repeat...Until", "While...Wend" loops  
\* [By](4gl_by.html) : Used in several syntaxes. See [Order By](4gl_order-by.html)  
---  
\* [Call](4gl_call.html) : Call of a subroutine  
\* [Case](4gl_case.html) : Defines a branch sequence based on list of values  
\* [Char](4gl_char.html) : String character variable declaration  
\* [Clbfile](4gl_clbfile.html) : Declaration of a large character object (Clob) variable  
\* [Close](4gl_close.html) : Closes a database file  
\* [Columns](4gl_columns.html)Defines a list of columns that will be read on a database table on "For" loops  
\* [Commit](4gl_commit.html) : Commits a database transaction  
\* [Const](4gl_const.html) : Declaration of constant parameters  
\* [Curr](4gl_curr.html) : Current line in some database access syntaxes  
---  
\* [Date](4gl_date.html) : Declaration of a date variable  
\* [Datetime](4gl_datetime.html) : Declaration of a Date and time variable  
\* [Dbgaff](4gl_dbgaff.html) : Opens the debugger  
\* [Decimal](4gl_decimal.html) : Declaration of a binary coded decimal variable  
\* [Default](4gl_default.html) : Declaration of default classes  
\* [Dela](4gl_dela.html) : Deletes positions in a list of arrays  
\* [Delete](4gl_delete.html) : Deletes lines in the database  
\* [DeleteByKey](4gl_deletebykey.html) : Deletes a line in the database with a condition on the update tick  
\* [Delfile](4gl_delfile.html) : Deletes a file on a file system  
\* [Desc](4gl_desc.html): descending order for [Sorta](4gl_sorta.html) syntax and [Order By](4gl_order-by.html) syntax  
\* [Double](4gl_double.html) : Declaration of a double precision flaoting point variable  
---  
\* [Else](4gl_else.html) : Alternative choice in an "If" sequence  
\* [Elsif](4gl_elsif.html) : Alternative condition in an "If" sequence  
\* [End](4gl_end.html) : Ends a subprogram or a function  
\* [Endcase](4gl_endcase.html) : Ends a "Case" sequence  
\* [Endif](4gl_endif.html) : Ends an "If.. Elsif.. Else.." sequence  
\* [Execsql](4gl_execsql.html) : Executes a SQL command on the database  
\* [Extended](4gl_extended.html) : Option Key word of [Columns](4gl_columns.html) instruction  
---  
\* [File](4gl_file.html) : Database table or view declaration  
\* [Filter](4gl_filter.html) : Adds a filter ("Where" clause) on a database table  
\* [First](4gl_first.html) : Reads the first line in different database access syntax  
\* [Float](4gl_float.html) : Declaration of a floating point variable  
\* [Flush](4gl_flush.html) : Flushes the "write buffer" used by [Writeb](4gl_writeb.html)  
\* [Fmethod](4gl_fmethod.html) : Method declaration (in STC files)  
\* [For](4gl_for.html) : Performs loops  
\* [FreeInstance](4gl_freeinstance.html) : Frees an instance   
\* [FreeGroup](4gl_freegroup.html) : Frees an allocation group associated to an instance  
\* [FreeSnapshot](4gl_freesnapshot.html) : Releases a snapshot for an instance  
\* [From](4gl_from.html) : Used in different branch syntaxes  
\* [Funprog](4gl_funprog.html) : Function declaration  
---  
\* [Getseq](4gl_getseq.html) : Reads data in a file in binary mode  
\* [Global](4gl_global.html) : Prefix of a declaration if the variable is in the [V] class  
\* [Gosub](4gl_gosub.html) : Calls a subroutine (ends with [Return](4gl_return.html))  
\* [Goto](4gl_goto.html) : Branches on another label  
---  
\* [Hint](4gl_hint.html) : used to force the database access strategy  
---  
\* [If](4gl_if.html) : Test sequence  
\* [Insa](4gl_insa.html) : Inserts positions in a list of arrays  
\* [Instance](4gl_instance.html) : Declaration of a variable storing a reference to an instance  
\* [Integer](4gl_integer.html) : Declaration of an integer variable  
\* [Iomode](4gl_iomode.html) : Parameter setting for sequential files  
---  
\* [Key](4gl_key.html) : Used in different database access syntaxes  
\* [Kill](4gl_kill.html) : Frees a variable  
\* [Last](4gl_last.html) : Reads the last line in different database access syntaxes  
---  
\* [Link](4gl_link.html) : Performs a "Join" between tables in a SQL cursor declaration  
\* [Local](4gl_local.html): Prefix of a declaration if the variable is in the local [L] class  
\* [Lock](4gl_lock.html): Performs a lock on a database table  
\* [LogicClose](4gl_logicclose.html): Closes a Table declared by File in an optimized way  
\* [Look](4gl_look.html): Performs a select on a database without filling the [F] buffer  
---  
\* [Method](4gl_method.html) : Method declaration (in STC files)  
---  
\* [NewInstance](4gl_newinstance.html) : Creation of a new instance for a given class  
\* [Next](4gl_next.html) : Ends a "For" loop; also used as Read mode  
\* [Nohint](4gl_hint.html) : used to force the database access strategy  
---  
\* [Onerrgo](4gl_onerrgo.html) : Declares a label in which a branch will be done if an error occurs  
\* [Openi](4gl_openi.html) : Opens a file for reading data  
\* [Openio](4gl_openio.html) : Opens a file for reading and writing data  
\* [Openo](4gl_openo.html) : Opens a file for writing data  
\* [Order By](4gl_order-by.html) : Used in different database access and sorting syntax  
---  
\* [Prev](4gl_prev.html) : Reads the previous line in different database access syntax  
\* [Putseq](4gl_putseq.html) : Writes data in binary mode in a file  
---  
\* [Raz](4gl_raz.html) : Fills variables with a null value  
\* [Rdseq](4gl_rdseq.html) : Reads data as characters string in a file  
\* [Read](4gl_read.html) : Reads a line from a cursor in a database  
\* [Readlock](4gl_readlock.html) : Reads a line with a lock from a cursor in a database  
\* [RenameFile](4gl_renamefile.html) : Renames a file on a file system  
\* [RenameFile](4gl_renamefile.html) : Renames a file on a file system  
\* [Repeat](4gl_repeat.html) : Performs a loop until a condition is fulfilled  
\* [Resume](4gl_resume.html) : Resumes the execution of a script after the error handling script has been executed  
\* [Return](4gl_return.html) : Ends a subroutine called by [Gosub](4gl_gosub.html)  
\* [Rewrite](4gl_rewrite.html) : Rewrites a line in the database  
\* [RewriteByKey](4gl_rewritebykey.html) : Rewrites a line in the database with a condition on the update tick  
\* [Rollback](4gl_rollback.html) : Aborts (rolls back) a database transaction  
---  
\* [Schar](4gl_schar.html) : Declares a single char (1 byte) variable  
\* [Seek](4gl_seek.html) : Moves the "Read / Write" cursor in a sequential file  
\* [Setlob](4gl_setlob.html) : Assignment of clob values  
\* [SetInstance](4gl_setinstance.html) : Assignment of an instance from or to a file class  
\* [SetInstancenosys](4gl_setinstancenosys.html) : Assignment of an instance from or to a file class with excluded properties  
\* [Shortint](4gl_shortint.html) : Declaration of a short integer variable  
\* [Sleep](4gl_sleep.html) : Suspends the execution of a script during a given number of seconds  
\* [Sorta](4gl_sorta.html) : Sorts a list of arrays  
\* [Sql](4gl_sql.html) : Used by several syntax to access to the database by an Sql query  
\* [Stability](4gl_stability.html) : Clause used in [For](4gl_for.html) statements  
\* [Step](4gl_step.html) : used to define the increment in a [For](4gl_for.html) loop  
\* [Subprog](4gl_subprog.html) : Declaration of a subprogram called by [Call](4gl_call.html)  
\* [System](4gl_system.html) : Used by different syntaxes to perform a system call  
---  
\* [Then](4gl_then.html) : Used to separate members of an [If](4gl_if.html) structure  
\* [Tinyint](4gl_tinyint.html) : Declaration of a tiny integer variable stored on 1 byte (replaces [Libelle](4gl_libelle.html))  
\* [To](4gl_to.html) : Used in [For](4gl_for.html) syntax to define the end value for a loop  
\* [Trbegin](4gl_trbegin.html) : Begins a database transaction  
---  
\* [Unlock](4gl_unlock.html) : Releases symbol locks and database locks  
\* [Until](4gl_until.html) : End condition of a [Repeat](4gl_repeat.html) loop  
\* [Update](4gl_update.html) : Updates lines in the database  
\* [Using](4gl_using.html) : Used by different syntaxes  
\* [Uuident](4gl_uuident.html) : Declaration of a UUID variable  
---  
\* [Value](4gl_value.html) : Declaration of parameters sent as values  
\* [Variable](4gl_variable.html) : Declaration of parameters sent as references  
---  
\* [Wend](4gl_wend.html) : Ends a [While]] loop  
\* [When](4gl_when.html) : Used in [Case](4gl_case.html) syntax  
\* [Where](4gl_where.html) : Used in different database syntaxes  
\* [While](4gl_while.html) : Starts a [While](4gl_while.html)...[Wend](4gl_wend.html) sequence  
\* [With](4gl_with.html) : Used in different syntaxes  
\* [Write](4gl_write.html) : Inserts a line in the database  
\* [Writeb](4gl_writeb.html) : Buffered insertion of lines in the database  
\* [Wrseq](4gl_wrseq.html) : Writes data in string mode in a file

# Variables or Methods [A](#vara)[C](#varc)[F](#varf)[G](#varg)[M](#varm)[N](#varn)[O](#varo)[R](#varr)[S](#vars)[T](#vart)[U](#varu)

---  
\* [adxdcs](4gl_adxdcs.html) : pivot year used when a year has been given on 2 digits  
\* [adxdir](4gl_adxdir.html) : base directory on the application server  
\* [adxfname](4gl_adxfname.html) : column names in an opened table  
\* [adxdlrec](4gl_adxdlrec.html) : number of records processed by the last Delete order  
\* [adxftl](4gl_adxftl.html) : grouping factor for read operation in a SQL [For](4gl_for.html) instruction  
\* [adxifs](4gl_adxifs.html) : field separator when reading or writing texts in files  
\* [adxirs](4gl_adxirs.html) : field separator when reading or writing texts in files  
\* [adxium](4gl_adxium.html) : character coding used for strings when reading or writing texts in files  
\* [adxlog](4gl_adxlog.html) : identifies that a database transaction is in progress  
\* [adxmda](4gl_adxmda.html) : identifies the angular mode  
\* [adxmother](4gl_adxmother.html) : identifies the reference folders of the current folder  
\* [adxsqlrec](4gl_adxsqlrec.html) : number of records processed by the last ExecSql order  
\* [adxtct](4gl_adxtct.html) : counter table definition  
\* [adxtms](4gl_adxtms.html) : message table definition  
\* [adxtlk](4gl_adxtlk.html) : locks table definition  
\* [adxuprec](4gl_adxuprec.html) : number of records processed by the last Update or Rewrite order  
\* [adxwrb](4gl_adxwrb.html) : grouping factor for write operation in a SQL [Writeb](4gl_writeb.html) instruction  
\* [allocgrp](4gl_allocgrp.html) : allocation group  
---  
\* [currind](4gl_currind.html) : current index for database operations  
\* [currlen](4gl_currlen.html) : current number of segments used in a key for database operations  
---  
\* [freemem](4gl_freemem.html) : free memory for variables and table buffers  
\* [freeheap](4gl_freeheap.html) : free memory for classes instances   
---  
\* [getAccessorEnabled](4gl_getaccessorenabled.html) : get accessor enablement indicator on properties  
---  
\* [isReadonly](4gl_isreadonly.html) : read-only indicator on instance properties  
---  
\* [maxmem](4gl_maxmem.html) : maximum memory for variables and table buffers  
\* [maxheap](4gl_maxheap.html) : maximum memory for classes instance  
\* [maxtab](4gl_maxtab.html) : maximum index assigned in a variable array  
\* [modified](4gl_modified.html) : modification indicator on instance properties  
---  
\* [nbind](4gl_nbind.html) : Number of indexes in an opened table  
\* [nbzon](4gl_nbzon.html) : Number of columns in an opened table  
\* [nomap](4gl_nomap.html) : identifies the current folder  
---  
\* [objectnbs](4gl_objectnbs.html) : number of properties of an instance  
\* [objecttype](4gl_objecttype.html) : class name for an instance  
\* [objectvar](4gl_objectvar.html) : property names of a class  
---  
\* [reckey](4gl_reckey.html) : fast order in For loops  
\* [revertUpdtick](4gl_revertupdtick.html) : returns to the previous update tick  
---  
\* [setAccessorEnabled](4gl_setaccessorenabled.html) : set accessor enablement indicator on properties  
\* [snapshot](4gl_snapshot.html) : access to the snapshot image of an instance  
\* [snapshotEnabled](4gl_snapshotenabled.html) : snapshot enablement indicator on a class  
---  
\* [tairec](4gl_tairec.html) : size of a record in an opened table  
\* [this](4gl_this.html) : current instance pointer (in a method)  
\* [revertToSnapshot](4gl_reverttosnapshot.html) : replaces the instance modifications by their snapshot values  
---  
\* [Updtick](4gl_updtick.html): update tick property in a table buffer

  

[Index](index.html)  [Home](getting-started_home.html)