# Generators


### [dec: count?]

Prints a uniformly random decimal digit. If `count` is specified, repeats `count` times.

### [hex: count?]

Prints a uniformly random lowercase hexadecimal digit. If `count` is specified, repeats `count` times.

### [n: min; max]

Prints a random integer with uniform distribution between `min` and `max` (both inclusive).

#### Example

```rant
You roll the dice and get '[n:1;6] and '[n:1;6].
# You roll the dice and get 2 and 5.
```

### [nf: min; max]

Prints a random float with uniform distribution between `min` (inclusive) and `max` (exclusive).


