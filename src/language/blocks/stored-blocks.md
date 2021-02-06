# Stored Blocks

Blocks can also be stored in variables for later use. To treat a block like a value instead of resolving, you need to prefix it with `<>` (known as the "defer operator").
If the block requires a hint or sink, the `<>` must appear after it.

```rant
<$cool-block = <>{Ohhh yeah!}>
```

Then you can resolve it later with the `[resolve]` function:

```rant
[resolve: <cool-block>] # "Ohhh yeah!"
```

Blocks are similar to closures when used this way, but only in that they contain code you can store and run later. Stored blocks make several guarantees that closures and functions cannot:
1. They never require arguments
3. They never capture variables
2. They will always consume attributes