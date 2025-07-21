[Index](index.html)  [Home](getting-started_home.html)

Mess

`mess` gives access to the translatable text resources used by the SAFE X3 engine and the application layers (especially local menus and identified messages such as error messages).

# Syntax

```
   mess(EXP_NUMBER,EXP_CHAP,EXP_TABLE)
```

* `EXP_NUMBER` is an integer expression that returns the message ID.
* `EXP_CHAP` is an integer expression that returns the message chapter.
* `EXP_TABLE` is an integer expression that returns the message table ID.

# Examples

```
   # The chapter 14 in table 1 contains the modules definition (local menu).
   # The 14th message is common core. Let's get the message in the default language
    Local Char COMMON_CORE(100)
    COMMON_CORE=mess(9,14,1)

   # Let's now get all the messages from the module table
   # The title of the menu local chapters are in chapter 0
   # The chapter 0 of the menu local associates a character to every choice.
   # The length of this message gives the number of choices
   Local Char TITLE_14(100)
   Local Integer NB_14,I
   Local Char CHOICES_14(100)(1..)
   TITLE_14=mess(14,0,1)
   For I=1 To len(0,14,1)
     CHOICES_14(I)=mess(I,14,1)
   Next I
```

# Description

`mess` gives access to the translatable texts defined in the dictionary and used by the user interface. These messages are organized in chapters that contain a list of messages. The text returned depends on the language used for the connection.

The table ID for these messages is always 1. A value of 0 is possible to access the messages used by the SAFE X3 engine.

The type of the result is [Char](4gl_char.html).

# Comments

The messages of the engine (table 0) are stored in a file of the `lan` sub-directory of the engine installation folder:

* The `messname` system variable defines the file name (std by default).
* The chapter 13 of this table contains the error messages. Thus, [errmes$](4gl_errmes$.html)(I) is equivalent to `mess(I,13,0)`.

The application messages are stored by default in APLSTD database table. The name of the table used is defined by the system variable `adxtms`:

* The number of messages per chapter is variable and depends on the software version.
* The local menus are stored in chapters of the message table (1 to 99, and most of the chapters over 200), and error messages are stored too (in chapters between 100 and 199).
* The titles of the chapter for local menus between 1 and 99 are stored in chapter 0; the titles of the local menus over 200 are stored in chapter 200 (message 1 being the title of local menu 201, and so forth).
* In a chapter that stores a local menu, the text number 0 stores a character by choice in the local menu: its length gives the number of choices in the local menu.

# Associated errors

| Error code | Description |
| --- | --- |
| 10 | At least one of the arguments is not numeric. |
| 50 | At least one of the arguments is out of range (negative). |

# See also

[errmes$](4gl_errmes$.html).

  

[Index](index.html)  [Home](getting-started_home.html)