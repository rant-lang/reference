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
This can be done using the **box operator** `[]`. Boxing a block produces an anonymous function, also simply known as a **box** when created this way.

```rant
# Creates a box and places it on the output
[]{A|B|C|D}
```

A box cannot resolve as-is; in order for it to produce output, it has to be "unboxed" first.

### Parameterized boxes

If you want to assign parameters to a box, specify the parameter names separated by semicolons inside another set of brackets within the box operator:

```rant
[[param1;param2]]{ ... }
```

## Calling anonymous functions

Calling an anonymous function uses the same syntax as regular function calls, but the function name is replaced by the `!` operator followed by an expression that resolves to the function you want to call.

```rant
# Define a function that returns a parameterless box
[$get-anon-func] {
    []{Hello from anonymous function}
}

[![get-anon-func]]          # "Hello from anonymous function"

# Define a function that returns a box with a single parameter
[$get-greet-func] {
    [[name]]{Hello, <name>!}
}

[![get-greet-func]:Rant]    # "Hello, Rant!"
```