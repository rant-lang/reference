# Capture control

{{ #include _proposal_msg.md }}

This proposal introduces a capture operator to explicitly opt-in a block to attribute capture.

Implementing this proposal would require making the default block behavior non-capturing.

## Capture operator

To make a block capturing, prefix it with `@`:

```rant
[rep: 10]
{a}
@{b}
# -> abbbbbbbbbb
```