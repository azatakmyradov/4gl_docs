[Index](index.html)  [Home](getting-started_home.html)

Cos

`cos` returns the value of the cosine of an angle expressed in degrees, radians, or grades, depending on [adxmda](4gl_adxmda.html). The type of result is [Double](4gl_double.html).

# Syntax

```
cos(value)
```

# Example

```
# This function converts polar coordinates to cartesian coordinates
Func CONVERT_TO_CARTESIAN(ANGLE_VALUE,DISTANCE_VALUE, X,Y)
Value Double ANGLE_VALUE,DISTANCE
Variable Double X,Y
  X=DISTANCE_VALUE*cos(ANGLE_VALUE)
  Y=DISTANCE_VALUE*sin(ANGLE_VALUE)
End
```

# See also

[sin](4gl_sin.html), [tan](4gl_tan.html), [asin](4gl_asin.html), [acos](4gl_acos.html), [atan](4gl_atan.html), [atan2](4gl_atan2.html).

  

[Index](index.html)  [Home](getting-started_home.html)