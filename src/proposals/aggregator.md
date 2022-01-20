# Aggregator

{{ #include _proposal_msg.md }}

An aggregator is an operation that transforms the parent scope's output.


## @edit

`@edit` *(right-associative prefix operator)*

Applies a custom operation to the parent output.

The parent scope's current output is accessible via the variable designated after the keyword.

`@edit` must appear first in an expression. It is not permitted in the global scope.

```rant
"example" { @edit x: `<x> `<x> }
# -> example example
```

### Examples

**Using an aggregator to compute a factorial**
```rant
[%factorial: n] {
    # Aggregator over int from parent output.
    # Multiplies over repeater's step values to calculate n!
    1 [rep: <n>] {@edit x: <x> * [step]}
}
```

**Using an aggregator to generate the Fibonacci series**
```rant
[%fibonacci: n] {
    # Aggregator over list from parent output.
    # Adds the last two values in the input list to produce Fibonacci series
    # Fallbacks provide the initial seed values.
    () [rep: <n>] {@edit f: (<f/-2 ? 0> + <f/-1 ? 1>)}
}
```


## Precedence

`@edit` has lower precedence than all regular operators.