# @text

The `@text` keyword is used for auto-hinting.

Auto-hinting can be applied to variable definitions, function parameters, and named function bodies to indicate that their output should be automatically hinted by the compiler.
This feature eliminates the need to apply hints to every occurrence of a value that you know should *always* be hinted.

## Auto-hinting a variable

To auto-hint a variable, add `@text` at the start of the definition.

```rant
<@text $first-name = John>
<@text $last-name = Smith>

<first-name> <last-name>
```

This prints `John Smith`. Without auto-hinting, the output would be `JohnSmith`.

## Auto-hinting a function

To auto-hint a (named) function, add `@text` between the signature and body of its definition.

```rant
[$adjective] @text {
    {cursed|blessed}
}

Have a [adjective] day!
```

This prints either `Have a blessed day!` or `Have a cursed day!`.

Without auto-hinting, it would print either `Have ablessedday!` or `Have acursedday!`.

### Auto-hinting behavior in piped calls

A piped function call will only become auto-hinted if the last function in the chain is auto-hinted.

## Auto-hinting a parameter

To auto-hint a parameter, add `@text` before the parameter name.

```rant
[$full-name: @text first; @text last] {
    <first> <last>
}

[full-name: Robin; Pederson]
```

This prints `Robin Pederson`. Without auto-hinting, it would print `RobinPederson`.

## Remarks

Auto-hinting can be overridden on an element by sinking it.