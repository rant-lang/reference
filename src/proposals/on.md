# @on

{{ #include _proposal_msg.md }}

The `@on` keyword assigns a trigger value to a block element for use when the block is resolved with a `match` selector.

## Usage

```rant
[match: foo] # Shortcut for [mksel: match; foo |> sel]
{
    # Branch with matching @on-value is chosen
    is foo @on foo |
    is bar @on bar |
    # Branch without any @on becomes the default branch
    is something else
}
# -> is foo
```