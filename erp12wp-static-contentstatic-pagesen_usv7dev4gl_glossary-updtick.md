[Index](index.html)  [Home](getting-started_home.html)

Glossary updtick

To manage optimistic update concurrency control, Version 7 of the Sage X3 engine introduced a new concept called `UpdTick`. `UpdTick`, which means update ticks.

It is an additional numeric column added automatically in any database table at dictionary validation. This column is used to store a revision number on every database line. The syntax to access this property is `[abbreviation]UpdTick`, where abbreviation is the abbreviation of the table.

The following are the Principles of Management for this column:

* When a line is inserted in the database, `UpdTick` has a value of 1.
* Every time an update is performed on at least a column value on a line, `UpdTick` is incremented by 1.

The management of `UpdTick` is implemented through a database trigger that is created on every table. The development partner does not need to manage its value.

When an update operation is managed from a representation, the underlying supervisor code does the following:

* Reads the current `UpdTick` value for every class or child class instance, when the working copy is created before it is sent to the user to modify the document.
* When the user saves the modification, the supervisor updates the line only if the `UpdTick` value did not change for any line modified. Otherwise, the user will receive an error message that someone previously modified the data. This is also tested on details lines when an update is done on a header/line document. In this case, the modification can also be a deletion.

To support this function, the Sage X3 engine includes a set of new instructions:

* [RewriteByKey](4gl_rewritebykey.html): Use to update a line in the database only if the `UpdTick` value is the correct one.
* [DeleteByKey](4gl_deletebykey.html): Use to delete a line in the database only if the `UpdTick` value is the correct one.

Compared to the techniques used in version 6, this current management mode offers the following advantages:

* No bottleneck is created on a technical locking table.
* In a single database operation, an update operation is performed on the table and a verification that no other modification is done.
* `UpdTick` is completely managed by the supervisor code.

  

[Index](index.html)  [Home](getting-started_home.html)