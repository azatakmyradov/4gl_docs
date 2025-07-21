[Index](index.html)  [Home](getting-started_home.html)

Adxdcs

`adxdcs` is a pivot year used to determine the century when the year is two digits.

# Syntax

```
adxdcs
```

# Examples

```
# Pivot date is 1941
  adxdcs=1941
  If aweek(5,40)=aweek(5,2040)
    # This is true, so this branch will be executed
  Endif
  If gdat$(1,5,41)=gdat$(1,5,1941)
    # This is also true
  Endif
```

# Definition

The pivot year is used to define the century when a year is two digits. If the pivot year is 'xxNN' ('xx' betwen 16 and 99 and 'NN' between 00 and 99) the following occurs:

* Any year shown with two digits, 'yy' where 'yy' ≤ 'NN', will be considered in the century 'xx'.
* Any year shown with two digits, 'yy' where 'yy' > 'NN', will be considered in the century 'xx+1'.

# Comments

This variable was previously used for data input with the fat client, and is now deprecated for this purpose.  
It can still be used on functions such as [aweek](4gl_aweek.html) or [gdat$](4gl_gdat$.html).

The value of adxdcs is got from the [connection locale](administration-reference_locales.html) when connecting with the version 7 web server, and is no more read from the DCS parameter, **except for the batch tasks that haven't any client connection**.

# See also

[aweek](4gl_aweek.html), [gdat$](4gl_gdat$.html).

  

[Index](index.html)  [Home](getting-started_home.html)