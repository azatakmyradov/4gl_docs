[Index](index.html)  [Home](getting-started_home.html)

Glossary uuid

Version 7 of the Sage X3 engine introduced a new data type called UUID [Universally Unique Identifier](https://en.wikipedia.org/wiki/UUID). This is a standard published by theÂ [Open Software Foundation](https://en.wikipedia.org/wiki/Open_Software_Foundation)Â (OSF).

The purpose of UUIDs is to allow unique identifiers to be assigned without coordination in distributed systems. There is no system that will guarantee that this identifier is unique because a UUID is a key with a finite length. The UUID generation process has been designed to be *practically unique*, and this is the case for database IDs. UUIDs can be used to identify a piece of information with a reasonable confidence that nobody will unintentionally identify another piece of information with the same UUID and thus create a conflict.

All operating systems provide a function to generate UUIDs. The algorithm usually combines the current time, a unique number assigned to the computer, and a random number.

A UUID is stored on 128 bits (16 bytes). A canonical printable form represents them as 32Â hexadecimalÂ digits, displayed in five groups separated by hyphens. The format is 8-4-4-4-12,Â which totals 36 characters including 32 digits and 4 hyphens (for example, `02311fc1-8bf6-4b90-814d-4b456b03faf2`). There are approximately 3\*10^38 possible UUIDs.

The Sage X3 engine includes a set of instructions and functions to support UUIDs:

* [Uuident](4gl_uuident.html): Use to declare a UUID variable
* [Nulluuid](4gl_nulluuid.html): Use to manage a null (not assigned) UUID
* [Touuid](4gl_touuid.html): Use to transform a canonical form to a UUID
* [Getuuid](4gl_getuuid.html): Use to generate a UUID

The supervisor layers, especially CRUD operation support and input control operations, use UUIDs intensively. For example:

* By default, a UUID column is now present on every Sage X3 table.
* When grids are managed by Sage X3 clients, lines are identified by UUIDs. This makes it very easy to identify array lines in insertion, deletion, and sort operations.

  

[Index](index.html)  [Home](getting-started_home.html)