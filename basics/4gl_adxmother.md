[Index](index.html)  [Home](getting-started_home.html)

Adxmother

`Adxmother` is a character string type variable array that contains the names of the reference folder of the current folder.

# Syntax

```
adxmother
adxmother(NUMBER)
```

* `NUMBER` is the level of the parent in the hierarchy.

The reference folder is used as reference for all the script elements and database tables not found in the folder.

* `Adxmother` contains the parent folder.
* `Adxmother(1)` contains the grandparent folder, that is the parent folder of the parent folder.

# Examples

```
# Call a subprogram only if the script is present in the parent folder
 If filinfo(filpath('TRT','MYSCRIPT','adx',nomap),0)<0 and  filinfo(filpath('TRT','MYSCRIPT','adx',adxmother),0)>0
   Call MYCALL From MYSCRIPT
 Endif
```

# See also

[nomap](4gl_nomap.html), [adxmac](4gl_adxmac.html).

  

[Index](index.html)  [Home](getting-started_home.html)