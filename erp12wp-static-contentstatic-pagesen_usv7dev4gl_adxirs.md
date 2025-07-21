[Index](index.html)  [Home](getting-started_home.html)

Adxirs

`adxirs` is a character string variable of length 2 maximum that contains the record separator used when reading or writing sequential files by the instructions [Rdseq](4gl_rdseq.html) and [Wrseq](4gl_wrseq.html).

Every element in a list given as an argument in [Rdseq](4gl_rdseq.html) or [Wrseq](4gl_wrseq.html) is separated by the field separator, but at the end of the record, a line separator defined by [adxifs](4gl_adxifs.html) is read or written instead of a record separator.

Note that this is a global value for all the files opened. Using the [Iomode](4gl_iomode.html) instruction gives you the control on every file opened; which is preferable.

# Syntax

```
adxirs
Iomode adxirs EXPRESSION Using [ABBREVIATION]
```

* **`EXPRESSION`** is an alphanumeric expression returning the value of the separator.
* **`ABBREVIATION`** is the abbreviation that has been used to open the file by [Openi](4gl_openi.html), [Openo](4gl_openo.html), or [Openio](4gl_openio.html).

# Examples

```
# On a Unix server, read the /etc/passwd file to find out the user characteristics for a given user ID
# This supposes that the user connected has the access rights !
# The structure of a line is the following:
# login:x:user_id:group_id:user_description:home_directory:shell

Subprog GET_UNIX_USER(USER_ID, USER_DESCRIPTION, HOME_DIRECTORY)
Value Integer USER_ID
Variable Char USER_DESCRIPTION(), HOME_DIRECTORY()
Local Char LOGIN(20),DUMMY(20),UID(10),GID(10),DESCRIPTION(100),HOMEDIR(100),SHELL(100)

  Openi "/etc/passwd" using [PWD]
  adxifs = ":"
  adxirs = chr$(10) : # Unix files usually have a line feed as end end of line
  Repeat
     Rdseq LOGIN,DUMMY,UID,GID,DESCRIPTION,HOMEDIR,SHELL Using [PWD]
  Until val(GID)=USER_ID or fstat=0

  Openi using [PWD]

  If val(GID)=USER_ID
     USER_DESCRIPTION=DESCRIPTION
     HOME_DIRECTORY=HOMEDIR
  Else
     Raz USER_DESCRIPTION, HOME_DIRECTORY
  Endif
End
# Write on a Windows sequential file values separated by commas
  Openo MYFILE Using [MYF]

  Iomode adxifs ',' Using [MYF]
  Iomode adxifs chr$(13)+chr$(10) Using [MYF] : # Carriage return Line feed usually for Windows files

  For I=1 to dim(VALUES)
     Wrseq I,VALUES(I),sum(VALUES(1..I)) Using [MYF]
  Next I

  Openo Using [MYF]
```

# Comments

Reading a list of N values by a [Rdseq](4gl_rdseq.html) instruction will read the record until the end of line character or an end of file is encountered. Thus, if more than N values are present on the line, the exceeding values will be skipped. If less than N values are present, the remaining elements will not be filled.

# See also

[adxifs](4gl_adxifs.html), [adxium](4gl_adxium.html), [Rdseq](4gl_rdseq.html), [Wrseq](4gl_wrseq.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html).

  

[Index](index.html)  [Home](getting-started_home.html)