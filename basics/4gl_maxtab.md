[Index](index.html)  [Home](getting-started_home.html)

Maxtab

This function returns the maximum index used for the first dimension of an array.

## Syntax

```
maxtab(ARRAY)
```

## Example

A common use for maxtab is to determine the number of associated objects. For example, a customer may have several ship to addresses where one of the addresses is a default address for the customer.In this example, determine the array index that contains the default address.

```
Local Integer BPA_INDEX                  # Index in the BPA array containing the default address of the customer

BPA_INDEX = find([V]CST_AYES, MY_CUSTOMER.BPA(1..maxtab(MY_CUSTOMER.BPA)).BPAADDFLG)>0
                                         # The BPA().BPAADDFLG is yes for the default address
```

Other examples include analyzing last element in used in an array.

```
Local Integer ARRAY_MAX, I
Local Char ARRAY(10)(1..)
For I=1 to 5
   ARRAY(maxtab(ARRAY)+1)="Line"
Next 

ARRAY_MAX=maxtab(ARRAY)            # ARRAY_MAX = 5 in this case

ARRAY(500) = "Line"
ARRAY_MAX = maxtab(ARRAY)         # ARRAY_MAX = 500
```

## Description

The difference between maxtab and dim is that maxtab returns the index of the last used element in the array while dim returns the total dimension of the array which for this example is 32767.

In the case of a multi-dimensioned ARRAY, maxtab will return the maximum used value of the first dimension.

```
Local Integer ARRAY2_MAX
Local Char ARRAY2(10)(1.., 3)
ARRAY2(3,0) = "Line 3-0"
ARRAY2(12,1)= "Line 12-1"
ARRAY2(7,2) = "Line 7-2"
ARRAY2_MAX = maxtab(ARRAY2)            # ARRAY2_MAX = 12
```

## See also

[null](4gl_null.html), [dim](4gl_dim.html).

  

[Index](index.html)  [Home](getting-started_home.html)