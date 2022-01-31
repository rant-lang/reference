# Blocks

A **block** represents one or more paths of execution as a single unit. 
It is one of the fundamental grammatical structures of the Rant language.

## Syntax

A block is written as a set of curly braces containing one or more sections of code separated by vertical pipes (`|`). 
Here are a few examples:

```rant
{}              # Empty block (1 implicit element which does nothing)
{ A }           # Block with 1 element (a "linear" block)
{ A | B }       # Block with 2 elements
{ A | B | C }   # Block with 3 elements
```

## Use cases

Blocks serve several purposes in Rant, ranging from simple branch selection to collection generation and even loops.
They can contain any valid Rant code&mdash;even other blocks.

### Item selection

By default, a block randomly selects one of its elements and runs the code inside.

```rant
# Randomly prints "Heads" or "Tails" with uniform probability
{Heads|Tails}
```

The selection strategy can be customized if needed using a [selector](/runtime/attributes.md#selectors).

### Collection generation

Blocks can be used to combine collections with conditional, repeating, or probabilistic elements.

```rant
# Evaluates to (A; B; C) or (A; D; E)
{ (A;) { (B; C) | (D; E) } }
```

```rant
# Evaluates to (1; 2; 3; 4; 5; 6; 7; 8; 9; 10)
[rep: 10] { ([step]) }
```

> **Important to note:**
>
> Blocks used for function bodies and dynamic accessor keys are slightly different: 
> 
> 1. **They are strictly linear**: they can only contain a single element. Adding multiple elements will cause a compiler error.
> 2. **They never consume [attributes](/runtime/attributes.md)**: Attributes must be explicitly consumed by adding an inner block.

### Entanglement

A selector can "entangle" several blocks to coordinate their behavior.

```rant
# Create a selector and store it in <sync>
[mksel:one > %sync]
# Both blocks use the `sync` selector, so they're entangled
[sel:<sync>]{Dogs|Cats} say \"[sel:<sync>]{woof|meow}!\"

##
Possible outputs:
- Dogs say "woof!"
- Cats say "meow!"
##
```

### Variable scope

Blocks act as scopes for local variables. Any variables created inside of a block are destroyed immediately after the block resolves.

```rant
{
    <%pi = 3.14>    # Create a variable called `pi`
    <pi>            # Prints 3.14 to the output
}                   # `pi` goes out of scope here
<pi>                # Error!
```