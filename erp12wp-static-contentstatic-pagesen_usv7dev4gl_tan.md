[Index](index.html)  [Home](getting-started_home.html)

Tan

`tan` returns the value of the tangent of an angle expressed in degrees, radians, or grades, depending on [adxmda](4gl_adxmda.html). The type of result is [Double](4gl_double.html).

# Syntax

```
tan(value)
```

# Example

```
# This function calculates the height of a point considering the ground distance and the angle
Func HEIGHT(ANGLE_VALUE,DISTANCE_VALUE)
Value Double ANGLE_VALUE,DISTANCE_VALUE

  If abs(ANGLE_VALUE)=acos(0)
     # value is infinite, we should return an error
  Else
     End DISTANCE_VALUE*tan(ANGLE_VALUE)
  Endif
```

# See also

[cos](4gl_cos.html), [tan](4gl_tan.html), [asin](4gl_asin.html), [acos](4gl_acos.html), [atan](4gl_atan.html), [atan2](4gl_atan2.html).

  

[Index](index.html)  [Home](getting-started_home.html)