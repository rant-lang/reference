# Standard Library: Generators


### [dig: count?]

Prints a uniformly random decimal digit. If `count` is specified, repeats `count` times.

```rant
# Generate a random 32-character decimal string
[dig:32] # ~> 01952208554533821061510695429126
```

### [digh: count?]

Prints a uniformly random lowercase hexadecimal digit. If `count` is specified, repeats `count` times.

#### Example

```rant
# Generate a random 32-character hex string
[digh:32] # ~> f4e5bef31ea02eac22f220e68e837587
```

### [dignz: count?]

Prints a uniformly random non-zero decimal digit. If `count` is specified, repeats `count` times.

```rant
# Generate a random 32-character decimal string without zeros
[dignz:32] # ~> 92558761934966287236132511739511
```

### [maybe: p?]

Returns a `bool` value with `p` probability of being true.

`p` must be either a `float` or `empty`. If omitted, it will default to `0.5`.

### [rand: min; max]

Prints a random integer with uniform distribution between `min` and `max` (both inclusive).

#### Example

```rant
You roll the dice and get '[rand:1;6] and '[rand:1;6].
# You roll the dice and get 2 and 5.
```

### [randf: min; max]

Prints a random float with uniform distribution between `min` (inclusive) and `max` (exclusive).


### [shred: input; count; variance]

Generates a list of `count` random numbers that vary from each other by `variance`, and whose sum equals `input`.

All three arguments must be numbers, and `count` must be an `integer`.

#### Errors

Causes a runtime error if:

* `input`, `count`, or `variance` is not a number
* `count` is zero or negative

#### Example

```rant
# Generate and print a list of 5 random numbers that add up to 1000
<$parts = [shred:1000;5;200]>
[join:" + ";<parts>] = [sum:<parts>]

##
Output:
170 + 378 + 83 + 189 + 180 = 1000
##
```