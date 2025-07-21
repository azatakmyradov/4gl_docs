[Index](index.html)  [Home](getting-started_home.html)

Glossary snapshot

A snapshot is an initial copy of the data stored in a class. It includes all child classes, if there are any. This concept is very useful when managing CRUD operation because it provides the differences between the data read and the modification done.

In every class instance, a pointer on the snapshot exists when the snapshot is enabled. Through a single instruction, it is possible to re-assign the value of a class with its origin value stored in the snapshot, or to start a snapshot by considering the current value as a new starting point.

The following links provide additional information on snapshots:

|  |  |
| --- | --- |
| Definition and use | [Developer Guide Snapshots](developer-guide_snapshots.html) |
| Instructions | [snapshot](4gl_snapshot.html) | [freeSnapshot](4gl_freesnapshot.html) | [revertToSnapshot](4gl_reverttosnapshot.html) | [snapshotEnabled](4gl_snapshotenabled.html) | [getModified](4gl_getmodified.html) |

  

[Index](index.html)  [Home](getting-started_home.html)