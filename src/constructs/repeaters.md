# Repeaters

A **repeater** is a collection of block attributes that controls several aspects of block resolution, namely:

1. How many times the block resolves in sequence,
2. Any code that runs before, between, and after each iteration,
3. Any code that runs before and after all iterations,
4. Any conditions that determine whether the block should continue running


## Variables

During a repeater's lifetime, it will store some state information in a local variable named `__REPSTATE` scoped to its associated block.


|Key|Type|Description|
|---|----|-----------|
|`index`|integer|Number of elapsed iterations|
|`max`|integer|Maximum iterations (`0` if infinite)|