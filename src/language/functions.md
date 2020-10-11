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

### Shadowed functions are still callable

The situation may occasionally arise where you accidentally (or intentionally)
define a non-function variable with the same name as a function from a parent scope (e.g. a stdlib function) 
and then try to call it: 

```rant
<$rep = "not a function">
[rep:10] # Wait a sec...
[sep:\n]
{
    # ...
}
```

Some people might (understandably) assume that this would crash the program, but this code actually still works!

When this happens, Rant will perform what is known as a "trickle-down function lookup":
the runtime will search each parent scope up to the global scope until it finds a function with the same name, and then call it as normal.

This behavior only applies to function calls, so getters will still correctly retrieve the new variable instead of the function.


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

A function parameter can be marked as optional using the `?` symbol.
When the argument is omitted for an optional parameter, it will default to the empty value `<>`.
Please note that any optional parameters must appear after all required parameters, and before any variadic parameter.

```rant
# Generates a map for a pet with a name and species (defaults to "dog")
[$gen-pet: name; species?] {
    @(
        name = <name>|
        species = [alt: <species>; dog]
    )
}
```

### Variadic parameters

Functions support variadic parameters with the special symbols `*` and `+`.

A `*` parameter is optional and defaults to an empty list, while a `+` parameter is required and must contain at least one element.

Functions may only have up to one variadic parameter, and it must appear last in the signature.

```rant
[$how-many:items*] {
    [len:<items>]
}

[how-many: foo; bar; baz] # Outputs "3"
```