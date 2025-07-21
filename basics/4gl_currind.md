[Index](index.html)  [Home](getting-started_home.html)

Currind

`currind` is a numeric variable in the [G] class associated with a table declared by the [File](4gl_file.html) instruction. It contains the key number used during the last access to the table. When the table is declared but no read operation has been done, the default value of `currind` is 1.

If the table is declared with a syntax such as `File XXXX order By key YYY=...`, `currind` is set to 1.

`currind` can also be assigned to set up the order by the default if a `Read` or a `For` instruction without index is given.

# Syntax

```
[G:ABV]currind
```

* `ABV` is the abbreviation used to open the table.

# Example

```
# The BPCUSTOMER table has 2 indexes:
# The first one is BPC0 which contains BPCNUM (customer id)
# The second one is BPC1 which contains BPCNAM (customer name)
Local File BPCUSTOMER
  Read [BPC]BPC0="DIS001"
# Here, message will contain 'Read performed on key #1 : BPC0'
  MESSAGE="Read performed on key #"+num$([G:BPC]currind)+" : "+[G:BPC]keyname([G:BPC]currind-1)

  Read [BPC]BPC1="MARTIN and sons"
# Here, message will contain 'Read performed on key #2 : BPC1'
  MESSAGE="Read performed on key #"+num$([G:BPC]currind)+" : "+[G:BPC]keyname([G:BPC]currind-1)

Local Char KEYS(20)(1..5), names(30)(1..5)
Local Integer NBREAD
  [G:BPC]currind=1
  Gosub FIRST_KEYS : # KEYS and NAMES contains the contents of the first lines in ascending order of BPCNUM
  [G:BPC]currind=2
  Gosub FIRST_KEYS : # KEYS and NAMES contains the contents of the first lines in ascending order of BPCNAM
End

$FIRST_KEYS
  NBREAD=0
  For [BPC]
    NBREAD+=1
    KEYS(NBREAD)=[BPC]BPCNUM
    NAMES(NBREAD)=[BPC]BPCNAM
    Break (NBREAD=dim(KEYS)
  Next
Return
```

# See also

[File](4gl_file.html), [Read](4gl_read.html), [For](4gl_for.html), [currlen](4gl_currlen.html).

  

[Index](index.html)  [Home](getting-started_home.html)