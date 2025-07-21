[Index](index.html)  [Home](getting-started_home.html)

Asin

`asin` returns the arc sine of a value. The result is expressed in degrees, radians, or grades, depending on [adxmda](4gl_adxmda.html). The type of the result is [Double](4gl_double.html).

`asin` returns a negative value if `x` is negative (you have to add 360 degrees to get a negative angle value).

# Syntax

```
asin(x)
```

# Example

```
# This function returns the angle of the shot if we consider that after a given distance an arrow has reached a given height.
Func GET_ANGLE(DISTANCE_VALUE,HEIGHT)
Value Double DISTANCE_VALUE, HEIGHT
End asin(HEIGH/DISTANCE)
```

# See also

[sin](4gl_sin.html), [cos](4gl_cos.html), [tan](4gl_tan.html), [acos](4gl_acos.html), [atan](4gl_atan.html), [atan2](4gl_atan2.html).

  

[Index](index.html)  [Home](getting-started_home.html)