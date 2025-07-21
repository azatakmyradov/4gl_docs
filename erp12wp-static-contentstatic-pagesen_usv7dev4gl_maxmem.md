[Index](index.html)  [Home](getting-started_home.html)

Maxmem

The `maxmem` variable defines the memory (in bytes) that can be allocated in the main memory of the Adonix server process.

## Syntax

```
maxmem
```

## Example

```
# check if at least 100K of memory is available
If freemem>100000
  # We have enough memory
Else
  # Let's enhance maxmem to get more memory
  maxmem+=100000
Endif
```

## See also

[freemem](4gl_freemem.html), [maxheap](4gl_maxheap.html), [freeheap](4gl_freeheap.html), [Memory requirements on the server](developer-guide_memory-requirements-on-the-server.html).

  

[Index](index.html)  [Home](getting-started_home.html)