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

### Variable scope

Blocks also act as scopes for local variables. Any variables created inside of a block are destroyed immediately after the block resolves.

### Lists and maps

Blocks can be turned into lists and maps using special syntax.

```rant
# Create a list of values
@{cayenne|serrano|habanero}

# Create a map of values
@:{name:John|age:25}
```