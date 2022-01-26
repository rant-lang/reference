# Protected blocks

Protected blocks allow you use separate attributes for an inner scope.

They behave differently than regular blocks in the following ways:
1. They don't consume attributes. 
1. Attribute changes inside the block won't persist outside of the block.

## Syntax

Prefix a block with `@` to protect it.

```rant
[rep: 3]
@{ A{B} }
{C}
# -> ABCCC
```