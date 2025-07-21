[Index](index.html)  [Home](getting-started_home.html)

Stability

`Stability` is a keyword used in a [For](4gl_for.html) loop. It is an option dedicated to SQL server that allows the [For](4gl_for.html) loop to see only the lines that were in the database when the [For](4gl_for.html) loop was started.

`Stability` in 4GL will translate to a static cursor on Microsoft SQL Server. The [Read](4gl_read.html), [Readlock](4gl_readlock.html) and [Look](4gl_look.html) instructions accept the `Stability` keyword but will not utilize a static cursor in Microsoft SQL Server.

  

[Index](index.html)  [Home](getting-started_home.html)