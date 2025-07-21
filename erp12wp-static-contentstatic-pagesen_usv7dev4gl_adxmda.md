[Index](index.html)  [Home](getting-started_home.html)

Adxmda

`adxmda` is a numeric value that determines the current angular mode. It is used for the functions that return or use angles.

`adxmda` can only have three values:

* **'0' :** if the angular mode is degrees.
* **'1' :** if the angular mode is radians.
* **'2' :** if the angular mode is grades.

# Syntax

```
adxmda
```

# Examples

```
# This function returns the following character string:
# "90 (in degrees) = 1.570796327 (in radians) = 100 (in grades)"

Funprog CONVERSION_MESSAGE
Local char CONVERSION_RULE(200)
  adxmda=0
  CONVERSION_RULE=num$(acos(0))-"(in degrees) = "
  adxmda=1
  CONVERSION_RULE+=num$(acos(0))-"(in radians) = "
  adxmda=2
  CONVERSION_RULE+=num$(acos(0))-"(in grades)"
End CONVERSION_RULE
```

# See also

[sin](4gl_sin.html), [cos](4gl_cos.html), [tan](4gl_tan.html), [asin](4gl_asin.html), [acos](4gl_acos.html), [atan](4gl_atan.html), [atan2](4gl_atan2.html).

  

[Index](index.html)  [Home](getting-started_home.html)