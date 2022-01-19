# Aggregators

{{ #include _proposal_msg.md }}

Aggregators are special operators for transforming the parent scope's output.

## @edit

`@edit` *(right-associative prefix operator)*

Applies a custom operation to the parent output.

The parent scope's current output is accessible via `@it`.

```rant
[%factorial: x] {
    1 [rep: <x>] {@edit @it * [step]}
}

[%fibonacci: x] {
    () [rep: <x>] {@edit @it (<@it/-2 ? 0> + <@it/-1 ? 1>) }
}
```

## @apply

`@apply` (*right-associative prefix operator)*

Same as `@edit` but automatically inserts `@it` at the start of the expression.

```rant
[%factorial: x] {
    1 [rep: <x>] {@apply * [step]}
}

[%fibonacci: x] {
    () [rep: <x>] {@apply (<@it/-2 ? 0> + <@it/-1 ? 1>) }
}
```

## Precedence

Aggregators have lower precedence than all regular operators.


## Remarks

Aggregators are not permitted in the global scope.