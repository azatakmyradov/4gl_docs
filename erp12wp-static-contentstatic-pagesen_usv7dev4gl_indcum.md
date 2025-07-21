[Index](index.html)  [Home](getting-started_home.html)

Indcum

`indcum` is a short integer variable used as a default index by the [sigma](4gl_sigma.html) function. It is only relevant when a single sigma loop is used; otherwise, you need to name the variable used as a sigma index.

# Syntax

```
  indcum
```

# Examples

```

# Let's compute a (very) approximated value of pi
# The loop value cannot exceed 32,767 (short integer value)
Local Decimal APPROX_PI
APPROX_PI=4*sigma(0,1000,((-1)^indcum)/(2*indcum+1))

# Let's compute a (much better) approximated value of pi (David and Gregory Chudnovsky)
# Due to the factorials and exponentiation used here, you cannot exceed 3 for the loop
# Otherwise you will get a numeric overflow
APPROX_PI=1/(12*sigma(0,3,((-1)^indcum)*fac(6*indcum)*(13591409+(545140134*indcum))
&            /(fac(3*indcum)*((fac(indcum))^3)*(640320^(3*indcum+3/2)))))

# Let's get the 26 letters in Latin alphabet
LETTERS=sigma(65,90,chr$(indcum)) 

# Sum of the square numbers of the integers from one (1) to N
  SQUARE_SUM = sigma(1, N, indcum*indcum)
```

# Comments

Using `indcum` in a [sigma](4gl_sigma.html) expression performs faster than using a numeric variable.

# See also

[sigma](4gl_sigma.html).

  

[Index](index.html)  [Home](getting-started_home.html)