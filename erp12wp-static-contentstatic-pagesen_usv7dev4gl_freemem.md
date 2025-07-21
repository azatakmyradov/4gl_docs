[Index](index.html)  [Home](getting-started_home.html)

Freemem

The 'Freemem' function returns the number of bytes not used in the main memory of the Adonix server process.

## Syntax

```
freemem
```

## Example

```
# check if at least 100K of memory are available
If freemem>100000
  # We have enough memory
Else
  # Let's enhance maxmem to get more memory
  maxmem+=100000
Endif
```

### See also

[maxmem](4gl_maxmem.html), [maxheap](4gl_maxheap.html), [freeheap](4gl_freeheap.html), [Server Memory requirements](developer-guide_memory-requirements-on-the-server.html)

  

[Index](index.html)  [Home](getting-started_home.html)