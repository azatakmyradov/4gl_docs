[Index](index.html)  [Home](getting-started_home.html)

Atan

`atan` returns the arc tangent of a value. The result is expressed in degrees, radians, or grades, depending on [adxmda](4gl_adxmda.html). The type of the result is Double.

`atan` returns a negative value if `x` is negative (you have to add 360 degrees to get a negative angle value).

# Syntax

```
atan(x)
```

# Example

```
# This function converts cartesian coordinates to polar coordinates
Func CONVERT_TO_POLAR(X,Y,ANGLE_VALUE,DISTANCE_VALUE)
Value Double X,Y
Variable Double ANGLE_VALUE,DISTANCE

  # Because we don't use the atan2 function here
  If X=0
    ANGLE_VALUE=sgn(Y)*acos(0)
  Else
    ANGLE_VALUE=atan(Y/X)
  Endif

  # If we don't want negative angles
  ANGLE_VALUE+=(ANGLE_VALUE<0)*4*acos(0)

  DISTANCE_VALUE=sqr(X^2+Y^2)

End
```

# See also

[sin](4gl_sin.html), [cos](4gl_cos.html), [tan](4gl_tan.html), [asin](4gl_asin.html), [acos](4gl_acos.html), [atan2](4gl_atan2.html).

  

[Index](index.html)  [Home](getting-started_home.html)