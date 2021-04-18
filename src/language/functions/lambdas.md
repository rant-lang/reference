# Lambdas

Rant implements anonymous (nameless) functions as **lambda expressions**, commonly referred to as simply **lambdas**.
The body of a lambda can also capture variables from its environment, just like regular named functions.

Basic lambda expression syntax with no parameters consists of a `?` symbol inside brackets preceding the function body. 

```rant
# Creates a function and places it on the output
[?] { Hello from lambda expression! }
```

## Parameterization

If you want to add parameters to a lambda, just specify the parameters after the colon as you would with a normal function definition:

```rant
[?: param1; param2] { ... }
```

## Inlining

If your lambda contains a single expression, such as a fragment or function call, you can omit the braces to save some typing.
This is called an **inline lambda**.

```rant
# Regular "block" lambda
[?: x; y; z] {
    [foo: <x> |> bar: <y>; <z>]
}

# Inline lambda
[?: x; y; z] [foo: <x> |> bar: <y>; <z>]
```

## Calling a lambda

Since lambdas are `function` objects just like named functions, the call syntax is very similar, but with one difference: 
the function name is replaced by the `!` symbol (to denote an anonymous call) followed by an expression providing the `function` to be called.

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