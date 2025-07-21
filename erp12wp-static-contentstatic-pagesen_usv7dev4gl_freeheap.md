[Index](index.html)  [Home](getting-started_home.html)

Freeheap

The 'Freeheap' function returns the number of bytes not used in the heap memory of the Adonix server process.

## Syntax

```
freeheap
```

## Example

```
# check if at least 100K of memory are available
If freeheap>100000
  # We have enough memory
Else
  # Let's enhance maxmem to get more memory
  maxheap+=100000
Endif
```

### See also

[maxmem](4gl_maxmem.html), [freemem](4gl_freemem.html), [maxheap](4gl_maxheap.html), [Server Memory requirements](developer-guide_memory-requirements-on-the-server.html)

  

[Index](index.html)  [Home](getting-started_home.html)