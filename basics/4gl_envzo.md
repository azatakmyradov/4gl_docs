[Index](index.html)  [Home](getting-started_home.html)

Envzo

`Envzo` forces the display of the fields in a mask.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

`Envzo`

# Examples

```
# in record deletion
# the'Object controls the links with the table dictionary
# each analysed table is displayed in this window
$VERF
For [A_TZ]LIEN(2) Where LIEN=FICANU & ANNUL=1
  FICHIER = [F:A_TZ]CODFIC
  Read [A_TB]CODFIC = FICHIER
  If !GSERVEUR & !GIMPORT
     If [M:VLC]NUMERO=""
     [M:VLC]TEX = mess(56,123,1) : # Table
     Affzo [VLC]TEX
     Endif
     [M:VLC]NUMERO = FICHIER
     Affzo [VLC]NUMERO
     Envzo 
  Endif
...
    Next
```

# Description

`Envzo` forces the display of the fields in a mask.

The system procedes with a buffering of the `Affzo` to optimisation. In this way, in order to re-display it, it is necessary :

* either a certain number of `Affzo`
* or an entry instruction such as `Boxinp`
* or the display of a message by `Infbox`, `Errbox`,...
* or by forcing with the `Envzo` instruction

This instruction is notably used to display a field in a window that cannot be entered.

# See also

[Saizo](4gl_Saizo.html), [Actzo](4gl_Actzo.html), [Affzo](4gl_Affzo.html), [Effzo](4gl_Effzo.html), [Grizo](4gl_Grizo.html), [Diszo](4gl_Diszo.html).

  

[Index](index.html)  [Home](getting-started_home.html)