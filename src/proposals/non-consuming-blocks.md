# Non-consuming blocks

{{ #include _proposal_msg.md }}

This proposal introduces operators to explicitly opt-in a block to attribute capture.

Implementing this proposal would require making the default block behavior non-consuming.

## Attribute operator

Prefix a block with `@` to pass the current attributes to a block, replacing the top attribute frame with its default values:

```rant
[rep: 10]
{a}
@{b}
# -> abbbbbbbbbb
```

## Lazy attribute operator

Prefix a block with `@@` to pass the current attributes to a block, but not overwrite them:

```rant
[rep: 10]
@@{a}
@@{b}
# -> aaaaaaaaaabbbbbbbbbb
```