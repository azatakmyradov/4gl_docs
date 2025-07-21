[Index](index.html)  [Home](getting-started_home.html)

Logicclose

This function closes a table logically. It releases the [F] buffer and any filters in a way that makes a further `Local File` execution much faster than if the table were closed by the `Close` instruction.

## Syntax

```
# The first syntax closes all the tables opened at the current level of Call nesting
LogicClose File

# The second syntax closes a given table identified by its abbreviation
LogicClose File [abbreviation]

# The second syntax closes a list of tables identified by their abbreviation
LogicClose File [abbreviation], [abbreviation]
```

## Use by the supervisor

The code called on [classes events](developer-guide_classes-events.html)  automatically performs a `LogicClose File` at the end of the execution of the event. The development partner has to declare the tables needed by adding a `Local File` instruction at the beginning of the code.

  

[Index](index.html)  [Home](getting-started_home.html)