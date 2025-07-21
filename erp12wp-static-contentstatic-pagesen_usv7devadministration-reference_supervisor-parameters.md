[Index](index.html)  [Home](getting-started_home.html)

Supervisor parameters

# Introduction

**The Sage X3 supervisor is the layer that handles the following:**   
\* The administration of the Sage X3 code.  
\* The security and filtering rules associated with the following:  
 \* The function profiles.  
 \* The tools used for the following:   
 \* Reporting (requesters, statistics, Business intelligence administration).   
  
 \* Update functions (folder creation and validation, folder upgrade, patching, and copy tools from one folder to another).

To manage these functions, some general parameters are required. Parameters can be set up at different organizational level of a folder as explained in the document describing the [context](developer-guide_context.html).

**The value of parameters can be set up:**

* From the Classic Sage X3 user definition (the function code is GESAUS) on the *Parameter* tab, when the parameter is set up at the user level.
* From a dedicated Classic page (the function code is ADOVAL).

The value of parameters is managed by the development partner in the code through methods available in the context class as explained in the [Developer guide Context](developer-guide_context.html#param) documentation.

The purpose of this page is to list the parameters that have an impact on the supervisor function. Only the parameters that have been modified since version 6 and that are deprecated in version 7, or that are new in version 7 are documented. The other parameters can be found in the global parameter definition pages.

# Parameter list

## Workflow management

* [WRKRMTMAC](administration-reference_parameter-wrkrmtmac.html): Server where the answer files for workflow are created (the application server by default).
* [WRKRMTDIR](administration-reference_parameter-wrkrmtdir.html): Directory where the answer files for workflow are created.
* WRKRMTHTTP: Deprecated.
* WRKSINTER: Deprecated.
* WRKSINTRA: Deprecated.

## Classic mode management

* [ACONVONLY](administration-reference_parameter-aconvonly.html) : defines how the links on version 6 functions that are generated are handled.

# Context variables list

The context is accessed from ACTX property present in every class instance, as well as from the general GACTX context variable.

The following table gives the main context variables used by the supervisor. Note that the group identifies a sub-hierarchy in the variable path. If the group is empty, the variable is directly accessible. For instance, `AFOLDER` value is available directly with the `GACTX.AFOLDER` path, where `AMODULE` is accessed by the `GACTX.AFOLD.AMODULE` path.

| Group | Variable | Description | Data type |
| --- | --- | --- | --- |
|  | AFOLDER | Current folder | ADS |
|  | ALLACS | All access | M |
|  | APRFCOD | Function profile | A |
|  | ASOLUTION | Name of the solution | A |
|  | LAN | User language | LAN |
|  | LANISO | ISO code language | A |
|  | LEVWML | Level | C |
|  | LOGIN | User login code | A |
|  | USER | User code | AUS |
| AFOLD | AHISTO | Purge folder | C |
| AFOLD | ALANGDEF | Default language | LAN |
| AFOLD | ALEGCUR | Current legislation | ADI |
| AFOLD | ALISTLEG | Current folder legislations | ADI |
| AFOLD | AMODULE | Installed modules | M |
| AFOLD | ANBLEG | Number of legislations | C |
| AFOLD | AVERSION | Current version | A |
| AINTL | DECIMALSEP | Decimal separator | A |
| AINTL | FIRSTDAYWEEK | First day of the week | M |
| AINTL | LONGDATE | Date format | A |
| AINTL | LONGDATETIM | Timestamp format | A |
| AINTL | LONGTIME | Time format | A |
| AINTL | NBGROUPSEP | No. of digits for the separator | C |
| AINTL | SHORTDATE | Date format | A |
| AINTL | SHORTDATETIM | Timestamp format | A |
| AINTL | SHORTTIME | Time format | A |
| AINTL | THOUSANDSEP | Thousand separator | A |
| AINTL | TWODIGITYEAR | Base date | C |
| ASOL | FCTCUR | Current function | AFC |
| ASOL | IRS | Default line separator | A |
| ASOL | OS | Type of operating system for the server (dos/unix) | A |
| ASOL | OS2 | Sub-type | A |
| ASOL | SERVEUR | Task server environment | L |
| ASOL | TMPDIR | Temporary directory | A |

  

[Index](index.html)  [Home](getting-started_home.html)