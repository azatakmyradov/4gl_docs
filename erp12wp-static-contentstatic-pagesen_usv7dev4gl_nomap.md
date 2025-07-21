[Index](index.html)  [Home](getting-started_home.html)

Nomap

`Nomap` is a character string type variable array that contains the names of the current folder.

# Syntax

```
nomap
```

# Examples

```
# Call a subprogram only if the script is present in the parent folder and not in the current folder
 If filinfo(filpath('TRT','MYSCRIPT','adx',nomap),0)<0 and  filinfo(filpath('TRT','MYSCRIPT','adx',adxmother),0)>0
   Call MYCALL From MYSCRIPT
 Endif
```

# See also

[adxmother](4gl_adxmother.html), [adxmac](4gl_adxmac.html).

  

[Index](index.html)  [Home](getting-started_home.html)