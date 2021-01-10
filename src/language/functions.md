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

When this happens, Rant will perform what is known as **function percolation**:
the runtime will search each parent scope up to the global scope until it finds a function with the same name, and then call it as normal.

Function percolation only applies to function calls, so getters will still correctly retrieve the new variable instead of the function.

### Function composition

When function calls are nested inside each other, they can become difficult to read and understand at a glance:

```rant
[e: [d: [c: [b: [a: 1]; 2]; 3]; 4]; 5] # Welcome to bracket hell
```

An alternative way to write nested function calls is by using iterative (rather than recursive) syntax-- a method known as **function composition**.

By using function composition, the same expression above can be rewritten with only a single pair of brackets:

```rant
[a: 1 & b: 2 & c: 3 & d: 4 & e: 5] # Much more readable!
```

In a composed function, the output of one function is fed into the next. By default, the output is inserted as the first argument;
however, this can be changed by passing the **composition value** `[]` as an argument:

```rant
[$get-zipper] {
    {<add>|<sub>}
}

# Pass the output of [get-zipper] as the third argument for [zip]
[get-zipper & zip: (1; 2; 3); (4; 5; 6); []]
```

If the composition value is a `function`, you can call it directly using an anonymous call:

```rant
[$get-math-func] {
    {<add>|<mul>|<sub>|<div>}
}

# Get a random math function and call it, passing in two numbers
[get-math-func & ![]: 3.0; 2.0]
```

### Spread notation

Spread notation lets you use a list to pass multiple arguments at once to a function call.
This is mostly useful for cases where the contents of a list need to be passed to a variadic parameter,
but spread notation works on all parameters (required, optional, and variadic).

There are no restrictions on the position of a spread within an argument list:
you can add them to the start, end, middle, or even have multiple spreads sprinkled throughout.
As long as the final argument list meets the requirements of the target function, it "just works."

Argument spreading is performed by prefixing an argument with `+`, as seen below:

```rant
[$concat-args: a*] {
    [join: \s; <a>]
}

<$extras = (baz; qux)>
[concat-args: foo; bar; +<extras>; boo]
# Same as calling [concat-args: foo; bar; baz; qux; boo]
```

Attempting to spread a non-list will simply pass the value as a normal argument.

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
When the argument is omitted for an optional parameter, it will default to `~`.
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