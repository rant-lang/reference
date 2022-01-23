# Output modifiers

Output modifiers are block elements that transform the calling scope's current output.

## The @edit operator

The `@edit` operator consumes the calling scope's output, applies some operation to it, and replaces the original output with the transformed value. 
It must appear at the start of a block element.

The parent scope's current output is accessible via the variable designated after the keyword, if specified.
The expression inside the block element produces the value that will then replace the caller's previous output.

The result of the operation is applied immediately to the parent's output as soon the the element finishes running.

```rant
# Variable <x> contains the parent's current output
"example" { @edit x: `<x> `<x> } # <x> = "example"
# -> example example

# No variable specified, so the current output is discarded
"example" { @edit: "overwritten" }
# -> overwritten
```

### Examples

**Using `@edit` to compute a factorial**
```rant
[%factorial: n] {
    # Modifies integer from parent output.
    # Multiplies over repeater's step values to calculate n!
    1 [rep: <n>] {@edit x: <x> * [step]}
}

[factorial: 10]
# -> 3628800
```

**Using `@edit` to generate the Fibonacci series**
```rant
[%fibonacci: n] {
    # Adds the last two values in the input list to produce Fibonacci series
    # Fallbacks provide the initial seed values.
    () [rep: <n>] {@edit f: <f> (<f/-2 ? 0> + <f/-1 ? 1>)}
}

[fibonacci: 10]
# -> (1; 1; 2; 3; 5; 8; 13; 21; 34; 55)
```