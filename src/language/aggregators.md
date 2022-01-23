# Aggregators

Aggregators are block elements that transform the calling scope's current output.

## The @edit operator

The `@edit` operator is used to create an aggregator. 
It must be specified at the start of a block element.

The parent scope's current output is accessible via the variable designated after the keyword, if specified.
The expression inside the block element produces the value that will then replace the caller's previous output.

The result of the aggregator is applied immediately to the parent's output as soon the the element finishes running.

```rant
# Aggregate variable <x> contains the parent's current output
"example" { @edit x: `<x> `<x> } # <x> = "example"
# -> example example

# No aggregate variable specified
"example" { @edit: "overwritten" }
# -> overwritten
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
    () [rep: <n>] {@edit f: <f> (<f/-2 ? 0> + <f/-1 ? 1>)}
}
```