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

### Optional parameters

A function parameter can be marked as optional using the `?` symbol. When the function is called and no value is passed to the parameter, it will default to `<>`.

```rant
[$]
```

### Variadic parameters

Functions support variadic parameters with the special symbols `*` and `+`. It must be the last parameter in the function signature.
Since the `*` variable is a list object, it can be treated like any other list; it cannot, however, be set by the user.

```rant
[$how-many:items*] {
    [len:<items>]
}

[how-many: foo; bar; baz] # Outputs "3"
```