[Index](index.html)  [Home](getting-started_home.html)

Acos

`acos` returns the arc cosine of a value. The result is expressed in degrees, radians, or grades, depending on [adxmda](4gl_adxmda.html). The type of the result is [Double](4gl_double.html).

`acos` returns a value in the (-180,180) range (in degrees). You must add 360 degrees to it if you do not want to get a negative angle value.

# Syntax

```
acos(x)
```

# Example

```
# This function returns the angle of the shot
# if we consider that after a given distance an arrow has reached a given ground distance
Func GET_ANGLE(DISTANCE_VALUE,GROUND_DISTANCE)
Value Double DISTANCE_VALUE, GROUND_DISTANCE
End asin(GROUND_DISTANCE/DISTANCE_VALUE)
```

# See also

[sin](4gl_sin.html), [cos](4gl_cos.html), [tan](4gl_tan.html), [asin](4gl_asin.html), [atan](4gl_atan.html), [atan2](4gl_atan2.html).

  

[Index](index.html)  [Home](getting-started_home.html)