[Index](index.html)  [Home](getting-started_home.html)

Constants

|  |  |  |  |
| --- | --- | --- | --- |
| [Definition](#definition) | [Creation of constant codes](#creation) | [Access to constants](#access) | [List of standard existing constants](#appendix) |

# 1. Definition

**Constants are variables that get code values when used by the supervisor and the engine layer to return error identification or a status. Some of these constants already exist in version 6, such as the values of âfstatâ while using database access instructions.**

**Version 7 implements the dictionary of constants, a new concept intended to provide explicit symbols instead of meaningless figures that are still in use.**

Technically, the constants dictionary validation generates a list of global variables coded as [V]CST\_xxx where xxx is the symbol that has been defined in the dictionary. The development partner can use these variables instead of existing values.

For example, codes `[V]CST_AWARNING`, `[V]CST_AERROR`, `[V]CST_AOK` used to describe a warning, an error, or an OK status that a function or a method may return, are easier to read than if the values were 1, 2 or 3.

# Creation of constant codes

Creating constant codes is performed in the constants dictionary where the main information that must be entered are:

* The name of the constant
* An associated data type
* A value

The coding rule for naming constants are defined in the [naming document](how-to_how-to-naming.html).

# Access to constants

After the constants are defined and the validation is performed, the constants are available on the next connection as global values in the [V] class, with the syntax [V]CST\_xxx.

# List of standard existing constants

The following constants have been defined for the supervisor operations.

| General context | Name of the variable | Explanation |
| --- | --- | --- |
| Error codes used when calling operations or methods. Every error line that can be found in the [AERROR class](developer-guide_error-handling.html) is present in the current context. | AOK | No error encountered. |
| ASUCCESS | The operation was successful, an additional message that tells the success of the operation can be returned. |
| AINFO | No error encountered, additional information messages returned. |
| AWARNING | Warnings are sent, but no errors are encountered. |
| AERROR | Some errors are encountered, the function did not work as expected, error messages are returned. |
| AFATAL | Fatal error encountered, the function did not work at all, with potential impacts on other operations. |
| Status code of a line within a Collection (ASTALIN property). Defines the status of a line during an update transaction managed by CRUD supervisor operations. | ANEW | A new line that has been inserted. |
| ADEL | A line in which a deletion has been requested. |
| ANEWDEL | A Line that has been inserted and in which a deletion has already been requested. |
| AUPD | A line that has been updated. |
| ALL | A line that has not been modified. |
| Position code of a line within a collection. Code can be used as a parameter for insertion or deletion of lines inside a grid. | ALASTPOS | Position at the end of the grid. |
| AFIRSTPOST | Position at the first line of the grid. |
| ANOTDEFINED | Returned message when a position in a grid is not found. |
| Return value from a database operation such as [Read](4gl_read.html), [Readlock](4gl_readlock.html), [Write](4gl_write.html), [Rewrite](4gl_rewrite.html), [RewriteByKey](4gl_rewritebykey.html), [Delete](4gl_delete.html), [DeleteByKey](4gl_deletebykey.html). This return value can be found in [fstat](4gl_fstat.html) global variable. | AOK | 0: The database operation was successful. |
| ALOCK | 1: A locking error happenend on the current line. |
| AOUTSEARCH | 2: When read with >= or <= operator, a result was found but not with an equal value. |
| ADUPKEY | 3: The write or update operation failed because an attempt of creation of a duplicate key was done on an index on which no duplicate keys are allowed. |
| AOUTKEYS | 4: Attempt of reading a key value that is smaller or greater than all existing key values. |
| ANOREC | 5: Record not read (no current record exists). |
| ARECTICKUPD | 6: The line no longer exists with the right updtick value (concurrency error during an update operation). |
| ARECTICKDEL | 7: The line no longer exists with the right updtick value (concurrency error during a delete operation). |
| Logical values | ATRUE | 1 (corresponds to the result of a comparison that is true). |
| AFALSE | 0 (corresponds to the result of a comparison that is false). |
| AYES | 2 (corresponds to the Yes value in the local menu #1). |
| ANO | 1 (corresponds to the No value in the local menu #1) |
 Level of definition for parameters (corresponds to the value of the 'NIVDEF' column in parameter dictionary) | ALEVCPY | 2 (the parameter is defined at company level). || ALEVFCY | 3 (the parameter is defined at site level). |
| ALEVFOLD | 1 (the parameter is defined at folder level). |
| ALEVLEG | 5 (the parameter is defined at legislation level). |
| ALEVUSR | 4 (the parameter is defined at user level). |
 Internal data types (corresponds to the values stored in local menu #30 for the 'ATYPTYP' column in data type dictionary, with the exception of the value '13' (ATYPINSTANCE) that is not defined in this local menu) | ATYPBLOB | Blbfile type (binary object). || ATYPCHAR | Char type (character string in UNICODE per default). |
| ATYPCLOB | Clbfile type (character long object). |
| ATYPDATE | Date type. |
| ATYPDATETIME | Datetime type. |
| ATYPDECIMAL | Decimal type. |
| ATYPDOUBLE | Double type (floating point with double precision). |
| ATYPFLOAT | Float type (floating point with simple precision). |
| ATYPINSTANCE | Instance type (instance pointer). |
| ATYPINTEGER | Integer type (long integer). |
| ATYPSHORTINT | Shortint type (short integer). |
| ATYPTINYINT | Tinyint type (tiny integer). |
| ATYPUUID | UUID type. |

  

[Index](index.html)  [Home](getting-started_home.html)