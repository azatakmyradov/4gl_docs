[Index](index.html)  [Home](getting-started_home.html)

Glossary structure

Version 7 of the Sage X3 engine introduced structures. A structure has properties and methods and it is defined in files with an 'STC' extension.

The STC files do not have to be modified manually because they are generated from class [class](developer-guide_classes.html) and [representation](developer-guide_representations.html) dictionaries with "C\_*CLASS\_CODE*" and "R\_*REPRESENTATION\_CODE*" names. Rather than structure, we can call them classes or representation classes.

To support structures, the language includes the following features:

* [Instance](4gl_instance.html): Used to declare a pointer on a structure instance.
* [NewInstance](4gl_newinstance.html): Used to instantiate a structure (class or representation) in memory.
* [Freeinstance](4gl_freeinstance.html): Used to free the memory associated with an instance of a class or representation.
* [FreeGroup](4gl_freegroup.html): Used to free the memory associated with an instance and all the instances in the same allocation group.
* The syntax `MYINSTANCE.PROPERTY` gives access to a property of an instance.
* The syntax `RETURN_VALUE = fmet MYINSTANCE.METHOD(parameters)` is used to execute a class method.
* Methods also exist on properties, but they are predefined.
* A structure can include pointers to other structures as well as arrays. A syntax such as
  `RETURN_VALUE = fmet MYORDER.LINES(3).DISCOUNT(2).CONTROL()` is possible ("CONTROL" method on "DISCOUNT(2)" property).

  

[Index](index.html)  [Home](getting-started_home.html)