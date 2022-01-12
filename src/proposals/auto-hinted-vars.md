# Auto-hinted variables

{{ #include _proposal_msg.md }}

In many cases, certain functions and variables are defined exclusively for use in text, which means that they should always be hinted.
Hinting them every time they're referenced can get tedious, so a way to tell the compiler that a variable or function is "text-like" would be a natural solution to this.

## @text

The `@text` keyword specifies to the compiler that a specific variable or function should always be treated as hinted when referenced in code and no hint or sink is specified.

## Auto-hinting variables

Specify `@text` at the start of the accessor when defining a variable.

```rant
<@text $first-name = Bob>
<@text $last-name = Smith>

<first-name> <last-name>
```

This prints `Bob Smith`. Without `@text` on the two variables, it would print `BobSmith`.



## Auto-hinting functions

Specify `@text` between the function signature and body.

```rant
[%first-letter: x] @text {
    [to-string: <x> |> either: <![]/0>; <>]
}

My last initial is [first-letter: Smith].
```

This prints `My last initial is S.` 

Without `@text` on the function definition, it would print `My last initial isS.`

### Behavior of auto-hinted functions in piped calls

A piped function call will only become auto-hinted if the last function in the chain is auto-hinted.