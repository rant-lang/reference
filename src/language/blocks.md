# Blocks

A **block** is a unit of Rant code subdivided into zero or more parts.

## Syntax

A block is defined by a set of braces containing zero or more sections of Rant code separated by vertical pipes (`|`). Here are a few examples:
```rant
{}          # Empty block
{A}         # Block with one element
{A|B}       # Block with multiple elements
```

## Use cases

Blocks serve several purposes in Rant, ranging from simple element selection to collections and even loops. They can contain any kind of Rant code&mdash;even other blocks.

### Item selection

In their simplest form, blocks resolve a single element from their body and add it to the output.

```rant
# Randomly prints "Heads" or "Tails" with uniform probability
{Heads|Tails}
```

By default, blocks select a random element with uniform probability, but the selection strategy can be customized if needed using a [selector](/constructs/selectors.md).

### Entanglement

A group of blocks can be "entangled" so that they all coordinate their selections.


```rant
# Create a selector and store it in a variable
<$sync = [mksel:one]>
# Both blocks use the `sync` selector, so they're entangled
[sel:<sync>]{Dogs|Cats} say \"[sel:<sync>]{woof|meow}!\"

##
Possible outputs:
- Dogs say "woof!"
- Cats say "meow!"
##
```

### Variable scope

Blocks also act as scopes for local variables. Any variables created inside of a block are destroyed immediately after the block resolves.

### Stored blocks

Blocks can also be stored in variables for later use. To treat a block like a value instead of resolving, you need to prefix it with the `*` symbol.
If the block requires a hint or sink, the `*` must appear after it.

```rant
<$cool-block = *{Ohhh yeah!}>
```

Then you can resolve it later with the `[resolve]` function:

```rant
[resolve:<cool-block>] # "Ohhh yeah!"
```

Blocks are similar to closures when used this way, but only in that they contain code you can store and run later. Stored blocks make several guarantees that closures and functions cannot:
1. They never require arguments
3. They never capture variables
2. They will always consume attributes

## Restrictions on function bodies and dynamic keys

Blocks used as function bodies and dynamic accessor keys are "linear" blocks: they can only contain one element and never consume attributes.
Attempting to use a multi-element block in these contexts will cause a compiler error.

This design consideration prevents function calls and accessors from unintentionally consuming attributes unless the user explicitly requests it by adding an inner block.