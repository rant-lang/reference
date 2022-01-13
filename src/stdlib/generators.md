# Standard Library: Generators

## dig

```rant

[%dig: count ? 1]

```
&rarr; `string`

Prints a uniformly random decimal digit. If `count` is specified, repeats `count` times.

### Parameters

**`count`** &larr; `int` *(optional)* <br/>
The number of digits to generate. Defaults to 1.

### Example

```rant
# Generate a random 32-character decimal string
[dig:32] # ~> 01952208554533821061510695429126
```


## digh

```rant

[%digh: count ? 1]

```
&rarr; `string`

Prints a uniformly random lowercase hexadecimal digit. If `count` is specified, repeats `count` times.

### Parameters

**`count`** &larr; `int` *(optional)* <br/>
The number of digits to generate. Defaults to 1.

### Example

```rant
# Generate a random 32-character hex string
[digh:32] # ~> f4e5bef31ea02eac22f220e68e837587
```


## dignz

```rant

[%dignz: count ? 1]

```
&rarr; `string`

Prints a uniformly random non-zero decimal digit. If `count` is specified, repeats `count` times.

### Parameters

**`count`** &larr; `int` *(optional)* <br/>
The number of digits to generate. Defaults to 1.

### Example

```rant
# Generate a random 32-character decimal string without zeros
[dignz:32] # ~> 92558761934966287236132511739511
```


## maybe

```rant

[%maybe: p ? 0.5]

```
&rarr; `bool`

Returns a `bool` value with `p` probability of being true.

`p` must be either a `float` or `empty`. If omitted, it will default to `0.5`.

### Parameters

**`p`** &larr; `float | empty` *(optional)* <br/>
The probability (0.0 <= p <= 1.0) of the printed boolean being true. 
If omitted or empty, defaults to 0.5.


## rand

```rant

[%rand: a; b]

```
&rarr; `int`

Prints a random integer with uniform distribution between `a` and `b` (both inclusive).

### Parameters

**`a`** &larr; `int` <br/>
The first inclusive bound of the random number.

**`b`** &larr; `int` <br/>
The second inclusive bound of the random number.

### Example

```rant
# Choose a number by fair dice roll.
You roll a `[rand:1;6].

# ~> You roll a 4.
```


## randf

```rant

[%randf: a; b]

```
&rarr; `float`

Prints a random float with uniform distribution between `a` (inclusive) and `b` (exclusive).

### Parameters

**`a`** &larr; `float` <br/>
The first inclusive bound of the random number.

**`b`** &larr; `float` <br/>
The second inclusive bound of the random number.


## rand-list

```rant

[%rand-list: a; b; n]

```
&rarr; `list`

Prints a list of `n` random integers with uniform distribution between `a` and `b` (both inclusive).

### Parameters

**`a`** &larr; `int` <br/>
The first inclusive bound of the random numbers.

**`b`** &larr; `int` <br/>
The second inclusive bound of the random numbers.

**`n`** &larr; `int` <br/>
The amount of numbers to generate.

### Example

```rant
# 2-dice roll

<$roll = [rand-list: 1; 6; 2]>
You rolled `[join: \sand\s; <roll>] for a total of `[sum: <roll>].

# ~> You rolled 5 and 3 for a total of 8.
```


## randf-list

```rant

[%randf-list: a; b; n]

```
&rarr; `list`

Prints a list of `n` random floats with uniform distribution between `a` (inclusive) and `b` (exclusive).

### Parameters

**`a`** &larr; `float` <br/>
The first inclusive bound of the random numbers.

**`b`** &larr; `float` <br/>
The second inclusive bound of the random numbers.

**`n`** &larr; `int` <br/>
The amount of numbers to generate.


## rand-list-sum

```rant

[%rand-list-sum: input; count; variance]

```
&rarr; `list`

Generates a list of `count` random numbers, whose sum equals `input`, and with a maximum absolute difference of `variance`.

### Parameters

**`input`** &larr; `int | float` <br/>
The input number to that the output numbers should add up to.

**`count`** &larr; `int` <br/>
The amount of numbers to generate.

**`variance`** &larr; `int | float` <br/>
The maximum absolute difference between any two generated numbers. 

### Errors

Raises an error if `count` is less than 1.

### Example

```rant
# Generate and print a list of 5 random numbers that add up to 1000
<$parts = [rand-list-sum: 1000; 5; 200]>
[join: <parts>; \s+\s] = [sum: <parts>]

##
Output:
170 + 378 + 83 + 189 + 180 = 1000
##
```