[Index](index.html)  [Home](getting-started_home.html)

Glossary datetime

Version 7 of the Sage X3 engine introduced a new data type called 'DateTime'. It stores a date and an hour in the same field, while the date data type is limited to the date (usually a business date).

The purpose of 'DateTime' is to allow the storage of a date related to a physical event in a unique format that is independent from the time zone where it occurred (usually, the time is stored in GMT time zone).

The Sage X3 engine includes a set of instructions and functions to support DateTime:

* [Datetime](4gl_datetime.html): Use to declare a date time variable.
* [datetime$](4gl_datetime$.html): Use to get the current date time.
* [gdatetime$](4gl_gdatetime$.html): Use to convert a string character to a date time.

The supervisor layers, especially CRUD operation support and input control operations, use 'DateTime' columns (`CREDATTIM` and `UPDDATTIM`) to store time stamps for creation and last modification of a line in the database.

  

[Index](index.html)  [Home](getting-started_home.html)