# Functions

Functions are an essential part of Rant: they facilitate code reuse and allow the user to interface with the standard library.
In addition to Rant's built-in functions, you can also define your own and use them however you see fit.

## Calling functions

To call a function, place the function's name inside a pair of square brackets:

```rant
[dig]
```
This calls the `[dig]` function from the standard library, which prints a random decimal digit.
The output of this call then flows into the caller's output, producing our digit:
```
8
```

### Arguments

Additionally, functions can accept arguments.
When a function requires arguments, we first add a colon `:` after the function's name, followed by a list of arguments separated by semicolons `;`.

Here are a few examples of how this works: 

```rant
# Function with no arguments
[func-name]

# Function with one argument
[func-name: arg1]

# Function with multiple arguments, delimited by ';'
[func-name: arg1; arg2]
```


## Defining functions

All functions are objects of the `function` type, and can be treated like any other variable.
When we define a function, we are simply defining a variable and storing it there.

To define a function, we need the following::
* The **function signature**, enclosed in square brackets `[ ]`, containing:
    * The name of the function,
    * A list of parameters to accept
* The **function body**, enclosed by curly braces `{ }`.

```rant
# Defines a parameterless function named `say-hello` that prints "Hello"
[$say-hello] {
    Hello
}

# Defines a function `greet` with parameter `name` that prints a custom greeting
# Arguments can be accessed like regular variables.
[$greet: name] {
    Hello, <name>!
}

# Defines a function `flip-coin` that returns the value of either `heads` and `tails`
[$flip-coin: heads; tails] {
    {<heads>|<tails>}
}
```

Like other variables, functions can also be made constant by using `%` in place of `$` when defining them:

```rant
# Regular functions can be overwritten
[$foo] { hello! }
[$foo] { goodbye! }

# Constant function; can't be overwritten
[%foo] { 
    important stuff... 
}

# If we try, the compiler will catch it and produce an error
[%foo] { # ERROR: constant redefinition
    this won't work
}
```

> **Note:**
>
> All of Rant's standard library functions are constants, and thus can't be modified&mdash;but they can still be shadowed in child scopes.

### Optional parameters

A function parameter can be marked as optional using the `?` symbol.
When the argument is omitted for an optional parameter, it will default to an `empty`.

> Please note that all optional parameters must appear after all required parameters, and before any variadic parameter;
> breaking this order will cause a compiler error.

```rant
# Generates a map for a pet with a name and species (defaults to "dog")
[$gen-pet: name; species?] {
    @(
        name = <name>;
        species = [alt: <species>; dog];
    )
}
```

#### Default arguments

You can also specify a custom default value for an optional parameter by adding an expression after the `?` modifier.

Each time the function is called without that parameter, Rant will run its default value expression and use its output as the argument.

```rant
# Modification of the previous [gen-pet] to use a default value instead of calling [alt]
[$gen-pet: name; species ? "dog"] {
    @(
        name = <name>;
        species = <species>;
    )
}
```

> **Note:**
>
> Default value expressions can capture external variables just like the body of the function they're attached to.

### Variadic parameters

Functions support variadic parameters with the special symbols `*` and `+`.

A `*` parameter is optional and defaults to an empty list, while a `+` parameter is required and must contain at least one element.

Functions may only have up to one variadic parameter, and it must appear last in the signature.

```rant
[$how-many: items*] {
    [len: <items>]
}

[how-many: foo; bar; baz] # Outputs "3"
```

## Closures

A function can access variables defined outside of its body.
When this happens, it "captures" a reference to that variable for use inside the function.
As a result, changes made to a captured variable persist between calls. 
Functions that capture variables are called **closures**.

Variable capturing can also be used to maintain a persistent state within a closure instance:
even if the original variable falls out of scope, the closure still keeps it alive.

```rant
# Create a function with a persistent state
{
    <$foo-num = 1>
    # Define a function [next-foo] in the parent scope
    [$^next-foo] {
        # Modify `foo-num` from inside the function
        foo <$n = <foo-num>; foo-num = [add: <foo-num>; 1]; n>
    }
} # `foo-num` falls out of scope here, but [next-foo] can still access it

# Call [next-foo] multiple times
[rep:4][sep:\n]
{
    [next-foo]
}
##
  Output:

  foo 1
  foo 2
  foo 3
  foo 4
##
```

### Limitations on variable capture

Capturing is only supported on variables accessed locally from the function body.
Descoped and explicit global accessors do not capture variables.

## Calling shadowed functions

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