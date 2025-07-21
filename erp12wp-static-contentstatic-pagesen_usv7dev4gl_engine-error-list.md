[Index](index.html)  [Home](getting-started_home.html)

Engine error list

The SAFE X3 engine manages exception errors that can be handled by the [Onerrgo](4gl_onerrgo.html) and [Resume](4gl_resume.html) instructions. The variable [errn](4gl_errn.html) contains the error code according to the following table:

| Error code | Explanation |
| --- | --- |
| 1 | A closing bracket is missing (happens on evalue) |
| 2 | An opening bracket is missing (happens on evalue) |
| 3 | A comma is missing (happens on evalue) |
| 4 | Function unknown (happens on evalue) |
| 5 | Illegal character (happens on evalue) |
| 6 | Nonexistent variable |
| 7 | Nonexistent class |
| 8 | Index incorrect |
| 9 | No current field |
| 10 | Incompatible type |
| 11 | Negative root for a number |
| 12 | Error in trigonometric calculation |
| 13 | Calculation capacity exceeded |
| 14 | Logarithm for a negative number |
| 15 | Hyperbolic trigonometric error |
| 16 | Error in the factorial calculation |
| 17 | Negative index |
| 18 | Incorrect label number |
| 19 | File type incorrect |
| 20 | Nonexistent file |
| 21 | Key does not exist in this table |
| 24 | Error in sequential file management |
| 25 | System error |
| 26 | Internal error |
| 27 | Problem with access to a file |
| 28 | Opening of a single table two times |
| 29 | Too many tables open |
| 30 | Incorrect table associated with mask |
| 31 | No more memory available |
| 32 | Return does not correspond to a Gosub |
| 33 | Function not implemented |
| 34 | Error in variable creation |
| 35 | The rank is not a grid (Mask) |
| 36 | Nonexistent window (Window) |
| 37 | Two masks with same abbreviation |
| 38 | Too many processes or procedures in process |
| 39 | Nonexistent label |
| 40 | Error in write to file |
| 41 | Step value null |
| 42 | Too many masks open |
| 43 | Table locked |
| 44 | No more space on the disk |
| 47 | Nonexistent mask |
| 48 | No transaction underway |
| 49 | There is already a transaction in process |
| 50 | Function not defined for the given value |
| 51 | Error in DCB management |
| 52 | ERROR log(0) |
| 53 | Division by 0 error |
| 55 | Too many dimensions |
| 56 | Error - date incorrect |
| 61 | Variable already exists |
| 62 | Non modifiable variable |
| 63 | Cannot access exclusive opening |
| 64 | Nonexistent processes |
| 65 | File size limit exceeded |
| 66 | Incorrect file name |
| 69 | Incorrect number of parameters |
| 70 | Incompatible parameter type |
| 71 | Unable to close file during a transaction |
| 73 | Nonexistent folder |
| 75 | Oracle error |
| 76 | SQL Server error |
| 78 | Error on transaction file |
| 79 | Too many opened windows |
| 81 | Nonexistent field |
| 84 | Object already exists |

Note that all errors related to Masks or Windows can only occur in Classic pages.

  

[Index](index.html)  [Home](getting-started_home.html)