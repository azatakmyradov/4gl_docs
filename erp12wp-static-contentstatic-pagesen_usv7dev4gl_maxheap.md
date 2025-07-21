[Index](index.html)  [Home](getting-started_home.html)

Maxheap

The `maxheap` variable defines the memory (in bytes) that can be allocated in the heap memory of the adonix server process.

## Syntax

```
maxheap
```

## Example

```
# check if at least 100K of heap memory is available
If freeheap>100000
  # We have enough memory
Else
  # Let's enhance maxheap to get more memory
  maxheap+=100000
Endif
```

## See also

[freemem](4gl_freemem.html), [maxmem](4gl_maxmem.html), [freeheap](4gl_freeheap.html), [Memory requirements on the server](developer-guide_memory-requirements-on-the-server.html).

  

[Index](index.html)  [Home](getting-started_home.html)