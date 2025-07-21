[Index](index.html)  [Home](getting-started_home.html)

Default

When a variable name is given without class or with a [F]class, a default priority order determines the class used for the variable. `Default` is used to define this search priority:

* For the tables classes when [F] is used.
* For all the classes when no class is given.

`Default` is also used in the syntax of a [Case](4gl_case.html) alternative ([When](4gl_when.html) Default). See [Case](4gl_case.html) for this syntax.

# Syntax

```
CODECODE CODE 

  Default File CLASS
  Default CLASS_LIST
  Default CLASS
  Default Local
  Default Global
```

* `CLASS` is a class such as `[V]`, `[L]`, `[abv]`, or `[F:abv]`, where abv is the abbreviation of a table.
* `CLASS_LIST` is a list of at least two classes separated by commas.

# Description and comments

The command `Default` defines the sequence in which the engine searches variables when their class is not specified, with the various syntax given below:

The syntax `Default File` is used to specify the default table. This table is used by default:

* When using [Read](4gl_read.html), [For](4gl_for.html), [Look](4gl_look.html), [Readlock](4gl_readlock.html), [Write](4gl_write.html), [Delete](4gl_delete.html), [Rewrite](4gl_rewrite.html), [Update](4gl_update.html), [RewriteByKey](4gl_rewritebykey.html), and [DeleteByKey](4gl_deletebykey.html) without specifying the table concerned.
* When using a variable with class [F] or [G], it searches first in the default table. If it is not found in this file, it then searches in the other tables.

The syntax `Default class` specifies the variable class to use by default when a variable is not preceded by any class indicator. If the variable cannot be found in the default class, it searches in the other classes.

The syntax `Default CLASSES_LIST` gives a complete list of classes (there must be at least two) for the search on variables when no class is specified. From the time a list of classes is given, only those in the list are used to search for variables.

**Warning:** if class [S] is excluded from this list, there is no access to the engine system variables such as [fstat](4gl_fstat.html) unless they are preceded by [S].

The two syntaxes, `Default Local` and `Default Global`, define the class used to create default variables. Remember that variables can be created automatically by a routine, a procedure, or a menu during allocation. If the variable to which a value is assigned has no class, and if it does not exist, then it is created automatically with a type matching that of the assigned expression, selected from Date, Decimal and Char, and with maximum length. The class in which the variable is created is therefore a [V] if using `Default Global` and [L] if using `Default Local`.

# Examples

```
   # Only the following classes are accessible for a variable
   # whose class is not specified, and in the order given           
     Default [S], [L], [V], [C], [F:ATB]

   # By default, variables without class are searched for in class [L]
     Default [L]

   # By default, non-existent variables are created in class [L]
   # Thus, if the I variable wasn't found in the default classes list, it will be created
   # as a Decimal variable in the local class ([L])
     Default Local
     For I = 1 To 100 : J+=I : Next I

   # By default, after the 3 instructions above, when a table related variable is declared without class,
   # it will be searched by default in [F:CLI] class, then in [F:PRO] class, then in [F:REP] class,
   # and then in the other [F] classes
   # But if an instruction seach as Read Key=value is used, only the [CLI] table will be considered
     Default File [REP]
     Default File [PRO]
     Default File [CLI]

   # By default, after the instruction above, variables without classes will be searched only
   # in [F:REP], [F:PRO], [F:CLI], [L] classes in that order
     Default file [REP], [CLI], [PRO], [L]

   # By default, after the instruction above, variables without class will be searched only:
   # first, as table variables (in the order given by Default File if any was given
   # then, as local variables, and finally as [C]variables
     Default [F], [L], [C]

   # The default classes should preferably be first [C], then [L],
   # then [V], then the other classes in the usual sequence.
       Default [V] : Default [L] : Default [C]

   # Only class [L] may be used for variables without class
     Default [L], [L]
```

# Comments

The engine manages a list of default classes and default tables. These lists are used to search for variables and to define default arguments.

The list of default tables is modified by:

* The [File](4gl_file.html) instruction that only places files declared on the list, in the order in which they are declared.
* The `Default File` instruction followed by a table abbreviation, which places the table on top of the list.

The list of default classes is modified by:  
\* The command `Default` followed by a list of classes, giving a complete list of classes.  
\* The `Default` instruction followed by a single class, which places the class on top of the list of default classes.  
\* The `Default` instruction followed by a list of classes, which replaces the previous list of classes by the list.

The list of default classes is restored when returning from a subprogram.

By default, in a subprogram, the variable policy creation is `Default Local`.

Do not to confuse 'Default [L]' and `Default Local`. The first syntax specifies that a variable, without class, is searched for by default in class [L]; while `Default Local` specifies that if a variable does not exist, it is created by default in class [L].

Do not omit [S] from the list of classes when giving a complete list in a Default command. In this case, all the engine system variables would become inaccessible, unless the name was always preceded by an [S]. When [F] appears on a list of default classes, all the tables on the list are in their default order.

If there is no `Default` instruction, the default classes used when a script runs are those given by:

```
Default [S], [L], [V], [M], [F]
```

# Associated errors

7: The class does not exist (for a table, this means it has not been declared in a previous File command).

# See also

[File](4gl_file.html), [Read](4gl_read.html), [Write](4gl_write.html), [Look](4gl_look.html), [Readlock](4gl_readlock.html), [RewriteByKey](4gl_rewritebykey.html), [DeleteByKey](4gl_deletebykey.html), [Delete](4gl_delete.html), [Update](4gl_update.html), [Local](4gl_local.html), [Global](4gl_global.html), [For](4gl_for.html).

  

[Index](index.html)  [Home](getting-started_home.html)