[Index](index.html)  [Home](getting-started_home.html)

Mask

Mask is used to declare all the masks that can be used in a routine.

# Syntax

```
   Local  Mask MASK_LIST
   Mask MASK_LIST
```

* `MASK_LIST` is a list of `MASKS`separated by commas.
* `MASK` can be one of the following choices:
  + a mask name as a symbol, optionally followed by an abbreviation between square brackets. The mask name can be prefixed by a folder name with the syntax FOLDER.MASKNAME
  + an abbreviation between square brackets (if the mask was already declared in a previous instruction).
  + an expression prefixed by the "=" sign. The result of the expression must be a string that defines the mask to be declared.

# Examples

```
   # Declaring 3 masks
    Mask SAICP1 [CPT1] , =[L]NOMMSK [CPT2], ="DOSSIERA.SAICP1" [CPT3]
```

# Description and comments

Mask is used to declare the masks that can be used during a routine. For this, the following may be declared:  
\* an absolute or relative path  
\* the name of the mask if it is in the MSK directory of the current folder or one of the reference applications.  
If a mask name and an abbreviation are given together, the mask may be opened by changing its abbreviation (allowing it to be opened twice, for example).

The instruction `Mask` closes all previously open masks. The `Local Mask` instruction will therefore be used in sub-programmes in preference to `Mask`. This declaration does not actually close files previously opened by a `Mask` or `Local Mask` instruction; however, the default list of masks then only contains masks declared by `Local Mask`. On return to the calling routine, the default list of masks will be found to be as it was before the sub-programme was called.

# Associated errors

| Error | Description |
| --- | --- |
| ERMODE (10) | The mask name is not alphanumeric. |
| ERTROM (42) | Too many masks opened at once. |
| PAFIC (20) | Mask not found. |
| ERCLAS (7) | Associated file abbreviation not found. |
| ERACCE (27) | Access error to mask. |

# See also

[File](4gl_file.html), [Affzo](4gl_Affzo.html).

  

[Index](index.html)  [Home](getting-started_home.html)