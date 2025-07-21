[Index](index.html)  [Home](getting-started_home.html)

Adxwrb

`adxwrb` stores the number of buffered database write operations.

# Syntax

```
 adxwrb=10 : # Recommended value
```

For performance reasons, you can buffer database write operations by using a dedicated instruction called [Writeb](../4gl/writeb.md). When this instruction is used, the write operations are grouped in a buffer and written when the buffer is full, that is when the number of delayed write operation reaches the value of `adxwrb`. The behavior of [Writeb](../4gl/writeb.md) is different from instruction [Write](../4gl/write.md) because the errors that might happen during insertion are returned only when the write buffer is flushed.

A modification of the `adxwrb` variable triggers an error if lines are still present in the write buffers. It is therefore important to execute a [Flush](4gl_flush.html) or a [Rollback](4gl_rollback.html) before modifying it.

# See also

[Write](4gl_write.html), [Writeb](4gl_writeb.html), [adxftl](4gl_adxftl.html).

  

[Index](index.html)  [Home](getting-started_home.html)