# @if, @elseif, @else

{{ #include _proposal_msg.md }}

The keywords `@if`, `@elseif`, and `@else` are used to construct conditional expressions.

```rant
@if <a> @eq <b>: {
    # do something
} @elseif <a> @eq <c>: {
    # do something else
} @else {
    # do something else
}
```