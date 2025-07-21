[Index](index.html)  [Home](getting-started_home.html)

Fmethod

This instruction declares a method in a class. It is used to declare methods that return a value. Methods that *do not* return any value are declared with the [Method](4gl_method.html) instruction.

Most CRUD method declarations are automatically generated in class STC files. These files contain `Fmethod` declarations with method bodies that dispatch to [events](developer-guide_classes-events.html) labels. The method's local scope is active when execution branches out to the event labels.

# Syntax

```
Fmethod METHOD_NAME [ '(' args_list ')' ]
```

The declaration is similar to [Subprog](../4gl/subprog.md) and [Funprog](../4gl/funprog.md) declarations. The method name is followed by an optional list of parameters.

The body of the method must be terminated by an `End result` instruction, where `result` is the value returned to the calling program.

# Invocation

A method behaves like a [Subprog](4gl_subprog.html) or [Funprog](4gl_funprog.html). A new scope is pushed upon entry and popped when `End` is reached. This scope contains a fresh set of local (`[L]`) variables. The local variables of the calling program are inaccessible.

The [this](4gl_this.html) keyword gives access to the instance to which the method has been applied.

# See also

[callmet](4gl_callmet.html), [fmet](4gl_fmet.html), [Method](4gl_method.html).

  

[Index](index.html)  [Home](getting-started_home.html)