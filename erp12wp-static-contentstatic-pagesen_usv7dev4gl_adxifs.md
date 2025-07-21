[Index](index.html)  [Home](getting-started_home.html)

Adxifs

`adxifs` is a character string variable of length 1 that contains the field separator used when reading or writing sequential files by the instructions [Rdseq](4gl_rdseq.html) and [Wrseq](4gl_wrseq.html).

Every element in a list given as an argument in [Rdseq](4gl_rdseq.html) or [Wrseq](4gl_wrseq.html) is separated by the field separator, and there is a line separator defined by [[adxirs] at the end of the element list.

Note that this is a global value for all the files opened. Using the [Iomode](4gl_iomode.html) instruction gives you the control on every file opened, which is preferable.

# Syntax

```
adxifs
Iomode adxifs EXPRESSION Using [ABBREVIATION]
```

* **`EXPRESSION`** is an alphanumeric expression returning the value of the separator.
* **`ABBREVIATION`** is the abbreviation that has been used to open the file by [Openi](4gl_openi.html), [Openo](4gl_openo.html), or [Openio](4gl_openio.html).

# Examples

```
# On a Unix server, read the /etc/passwd file to find out the user characteristics for a given user id
# This supposes that the user connected has the access rights !
# The structure of a line is the following:
# login:x:user_id:group_id:user_description:home_directory:shell

Subprog GET_UNIX_USER(USER_ID, USER_DESCRIPTION, HOME_DIRECTORY)
Value Integer USER_ID
Variable Char USER_DESCRIPTION(), HOME_DIRECTORY()
Local Char LOGIN(20),DUMMY(20),UID(10),GID(10),DESCRIPTION(100),HOMEDIR(100),SHELL(100)

  Openi "/etc/passwd" using [PWD]
  adxifs = ":"
  adxirs = chr$(10)
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
# Write on a sequential file values separated by commas
  Openo MYFILE Using [MYF]

  Iomode adxifs ',' Using [MYF]
  Iomode adxifs chr$(13)+chr$(10) Using [MYF] : # Carriage return Line feed

  For I=1 to dim(VALUES)
     Wrseq I,VALUES(I),sum(VALUES(1..I)) Using [MYF]
  Next I

  Openo Using [MYF]
```

# Comments

If the field separator is the space character, [Rdseq](4gl_rdseq.html) considers several spaces in a row as a single separator.

# See also

[adxirs](4gl_adxirs.html), [adxium](4gl_adxium.html), [Rdseq](4gl_rdseq.html), [Wrseq](4gl_wrseq.html), [Openi](4gl_openi.html), [Openo](4gl_openo.html), [Openio](4gl_openio.html).

  

[Index](index.html)  [Home](getting-started_home.html)