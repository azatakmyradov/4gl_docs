[Index](index.html)  [Home](getting-started_home.html)

status

`status` is a system variable that contains the return status of an entry statement.

**This variable is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Class, type and dimension

```
Tinyint [S]status
```

# Description and comments

`status` is used to know the result of an entry operation.

This variable is also reset to 1 after an [Affzo](4gl_Affzo.html) display operation.

The different values possible are described in the following table:

| Statuses | Associated variables | Description | Index GETABOU |
| --- | --- | --- | --- |
| 1 |  | Tab positioning |  |
| 2 |  | Selection window on a field |  |
| 4 | GSTARET | Exit by return |  |
| 5 |  | Shift+tab positioning |  |
| 7 | GSTAESC | Closing the box |  |
| 20 | GSTATIR | Positioning via mouse click to a field |  |
| 21 |  | Positioning via mouse click to a grid |  |
| 26 |  | Entry in a grid by double-click on a cell |  |
| 27 | GSTALFT | Click on left list |  |
| 28 | GSTALF2 | Double-click on left list |  |
| 36 | GSTALF3 | Click on hierarchized list |  |
| 37 | GSTALF4 | Double-click on hierarchized list |  |
| 41 |  | De-selection in the picking box |  |
| 42 | GSTAPIC | Event on picking box |  |
| 43 |  | De-selection in hierarchized picking box |  |
| 44 | GSTAPKF | Closing a picking box |  |
| 45 | GSTASRA | Quick selection |  |
| 46 |  | activation of the "VERIFIER" button in the formula editor |  |
| 47 |  | Selection of a parent element without a child element in the formula editor |  |
| 48 | GSTAPRG | Previous page for the left list |  |
| 49 | GSTASVG | Next page for the left list |  |
| 55 | GSTABOI | Left list end |  |
| 65 |  | Cancellation of a line |  |
| 68 |  | Cancellation of a group of lines |  |
| 71 |  | Line change |  |
| 73 |  | Line insert |  |
| 75 |  | Line modification |  |
| 82 |  | Summary |  |
| 83 |  | Delete a group of lines |  |
| 91 | GSTANEW | File/New | GNOUV |
| 92 | GSTAENR | File/Save | GENRE |
| 93 | GSTACRE | File/Create | GCREE |
| 94 | GSTAANU | File/Delete | GSUPP |
| 95 | GSTASEL | File/Select | GSELE |
| 96 | GSTAFIR | File/First | GPREM |
| 97 | GSTALAS | File/Last | GDERN |
| 98 | GSTASUI | File/Next | GSUIV |
| 99 | GSTAPRE | File/Previous | GPREC |
| 129-136 | GBOUT1..8 | Contextual menus |  |
| 145 | GSTAEUR | Display/Euro |  |
| 147 | GSTAMHL | Help modification |  |
| 148 | GSTAHLP | Field information |  |
| 1029 | GSTAOK | OK button | GVALI |
| 1100-1119 | GSTASPE1..6 | Application buttons preceded by controls (GSTABOU+I) | GSPE1..6 |
| 1200-1219 |  | Application menus preceded by controls |  |
| 1220-1239 |  | Statuses for the specific/custom developments preceded by controls |  |
| 1792 | GSTAFIN | Abort button | GABAN |
| 1793 | GSTACHG | File/Code change | GCHAN |
| 1794 | GSTAJOI | File/Attachments | GJOIN |
| 1795 | GSTACOM | File/Comments | GCOMM |
| 1796 | GSTAEDI | File/Print | GEDIT |
| 1797 | GSTALIS | File/List | GLIST |
| 1798 | GSTADAT | File/Properties | GDATC |
| 1799 | GSTARAF | Display/Refresh | GRAFF |
| 1800-1819 |  | Application buttons without controls (GSTABOU2+I) |  |
| 1820 | GSTATRN | Transaction button | GTRAN |
| 1821 | GSTAFIN | End button |  |
| 1822 | GSTAHLO | OBjet on Parameter help |  |
| 1823 | GSTASTA | Statistics |  |
| 1824 | GSTAWOR | Workflow |  |
| 1825 | GSTALNK | Link browser |  |
| 1826 | GSTAUNL | web service site: unlock and abort current record |  |
| 1827 | GSTAMOT | Key-word selection |  |
| 1828 | GSTALIT | forcing the read |  |
| 1829 | GSTANBR | Number of records in an OBject (GEODE) |  |
| 1830 | GSTAPCK | Selection on a picking browser ( GEODE ) |  |
| 1831 | GSTAENV | Changing environment ( GEODE ) |  |
| 1832 | GSTAPCK1 | Check all on a picking browser ( GEODE ) |  |
| 1833 | GSTAPCK2 | Uncheck all on a picking browser ( GEODE ) |  |
| 2000-2019 |  | Application menus without controls |  |
| 2020-2029 |  | Statuses for the specific/custom developments without controls |  |

  

[Index](index.html)  [Home](getting-started_home.html)