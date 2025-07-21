[Index](index.html)  [Home](getting-started_home.html)

Revertupdtick

This built-in method reverts the [updtick](4gl_updtick.html) value of an instance to its snapshot value.

On a simple instance:

```
MYINSTANCE.revertUpdtick
```

  
is equivalent to:

```
MYINSTANCE.updtick=MYINSTANCE.snapshot.updtick
```

  
On complex graphs of instances, `revertUpdtick` reverts the update tick of all instances of the graph.

This instruction is primarily used to handle errors during updates of complex objects. If some instances have been updated in the transaction before the error, their `updtick` values have already been reassigned. When the `Rollback` is executed, this method is invoked to restore the `updtick` property on all instances.

# Syntax

```
MYINSTANCE.revertUpdtick
```

# See also

[DeleteByKey](4gl_deletebykey.html), [updtick](4gl_updtick.html), [RewriteByKey](4gl_rewritebykey.html), [Updtick definition](4gl_glossary-updtick.html).

  

[Index](index.html)  [Home](getting-started_home.html)