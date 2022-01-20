# Protected blocks

{{ #include _proposal_msg.md }}

This proposal introduces operators to modify how blocks interact with attributes.

## Protected block

Prefix a block with `@` to mark the block as _(outer-)protected_.

A protected block will not consume attributes and will use a separate attribute frame internally. Any attribute changes made inside the block will not persist outside of the block.

```rant
[rep: 3]
@{ A{B} }
{C}
# -> ABCCC
```

## Inner-protected block

Prefix a block with `@@` to mark the block as _inner-protected_.

An inner-protected block will consume the current attributes and also use a separate attribute frame internally. Any attribute changes made inside the block will not persist outside of the block.

```rant
[rep: 3]
@@{ A{B} [rep: 2] } # [rep: 2] not applied outside this block
{ C }
# -> ABABBABBC
```
