# Closures

It is sometimes necessary to pass a function as a value rather than define it with a name, so that it can be called elsewhere later on.
This can be done using **closures**, which are an implementation of anonymous functions with the ability to "capture" external variables.

> TODO: Provide variable capture examples

Basic closure syntax with no parameters consists of a `?` symbol inside brackets preceding the function body. 

```rant
# Creates a closure and places it on the output
[?]{A|B|C|D}
```

## Parameterized closures

If you want to add parameters to a closure, specify the parameter names as you would with a normal function inside the closure's signature:

```rant
[?:param1;param2]{ ... }
```

## Calling anonymous functions

Calling an anonymous function uses the same syntax as regular function calls, but the function name is replaced by the `!` symbol followed by an expression that provides the function (or closure) you want to call.

```rant
# Define a function that returns a parameterless box
[$get-anon-func] {
    [?]{Hello from anonymous function}
}

[![get-anon-func]]          # "Hello from anonymous function"

# Define a function that returns a box with a single parameter
[$get-greet-func] {
    [?:name]{Hello, <name>!}
}

[![get-greet-func]:Rant]    # "Hello, Rant!"
```