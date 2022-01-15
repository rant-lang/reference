# Aggregators

{{ #include _proposal_msg.md }}

Aggregators are special operators for transforming the parent scope's output.

## @edit

`@edit` *(right-associative prefix operator)*

Applies a custom operation to the parent output.

The parent scope's current output is accessible via `@in`.

```rant
[%factorial: x] {
    1 [rep: <x>] {@edit @in * [step]}
}

[%fibonacci: x] {
    () [rep: <x>] {@edit @in (<@in/-2 ? 0> + <@in/-1 ? 1>) }
}
```

## @apply

`@apply` (*right-associative prefix operator)*

Same as `@edit` but automatically inserts `@in` at the start of the expression.

```rant
[%factorial: x] {
    1 [rep: <x>] {@apply * [step]}
}

[%fibonacci: x] {
    () [rep: <x>] {@apply (<@in/-2 ? 0> + <@in/-1 ? 1>) }
}
```

## Precedence

Aggregators have lower precedence than all regular operators. 
They will treat everything already printed in the outer scope as the LHS.

## Remarks

Aggregators in the global scope behave differently:
the first aggregator output will be used as the first operand and will not perform any operation.