[Index](index.html)  [Home](getting-started_home.html)

Atan2

`atan2` returns the value of the arc tangent of a value expressed as a quotient of tow values: `x` and `y`. The result is expressed in degrees, radians, or grades, depending on [adxmda](4gl_adxmda.html). The type of the result is [Double](4gl_double.html).

`atan2` returns a negative value if **'x/y'** is negative (you have to add 360 degrees to get a negative angle value).

If `y` is not null, `atan2(x,y)` is equal to `atan(x/y)`. If `y` is null, it will return `-90` or `90` (if expressed in degrees), depending on the sign of `x`.

# Syntax

```
atan2(x,y)
```

# Example

```
# This function converts cartesian coordinates to polar coordinates
Func CONVERT_TO_POLAR(X,Y,ANGLE_VALUE,DISTANCE_VALUE)
Value Double X,Y
Variable Double ANGLE_VALUE,DISTANCE
  ANGLE_VALUE=atan2(Y,X)
  ANGLE_VALUE+=(ANGLE_VALUE<0)*4*acos(0)
  DISTANCE_VALUE=sqr(X^2+Y^2)

End
```

# See also

[sin](4gl_sin.html), [cos](4gl_cos.html), [tan](4gl_tan.html), [asin](4gl_asin.html), [acos](4gl_acos.html), [atan](4gl_atan.html), [atan2](4gl_atan2.html).

  

[Index](index.html)  [Home](getting-started_home.html)