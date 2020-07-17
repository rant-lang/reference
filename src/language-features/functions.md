# Functions

Functions contain code that can be executed arbitrarily. The Rant standard library includes several native functions, but you can also define your own.

## Calling functions

Function calls use the following syntax:

```rant
# Function with no arguments
[func-name]

# Function with one argument
[func-name: arg1]

# Function with multiple arguments, delimited by ';'
[func-name: arg1; arg2]
```

## Defining functions

To define a function and assign it to a variable, the syntax is as follows:

```rant
# Define a parameterless function named `say-hello` that prints "Hello"
[$say-hello] {
    Hello
}

# Define a function `greet` with parameter `name` that prints a custom greeting
[$greet: name] {
    Hello, <name>!
}

# Define a function `flip-coin` that returns the value of either `heads` and `tails`
[$flip-coin: heads; tails] {
    {<heads>|<tails>}
}
```

## Boxing

It is sometimes necessary to pass a block as a function rather than resolve it, so that it can be resolved elsewhere later on.
This can be done using the **box operator** `[]`. Boxing a block produces an anonymous function, which is simply known as a **box** when created this way.

```rant
# Creates a box and places it on the output
[]{A|B|C|D}
```

A box cannot resolve as-is; in order for it to produce output, it has to be "unboxed" first.

### Parameterized boxes

If you want to assign parameters to a box, use this:

```rant
[[param1;param2]]{ ... }
```

## Unboxing

Forcing one or more boxed values to resolve is known as "unboxing". This is performed with the unbox operator `[!]` followed by a block containing what you want to unbox.

```rant
[!]{[]{Heads|Tails}}    # Equivalent to {Heads|Tails}
```