# Lambdas

Rant implements anonymous (nameless) functions as **lambda expressions**, commonly referred to as simply **lambdas**.
The body of a lambda can also capture variables from its environment, enabling you to construct **closures**.

Basic lambda expression syntax with no parameters consists of a `?` symbol inside brackets preceding the function body. 

```rant
# Creates a function and places it on the output
[?] { Hello from lambda expression! }
```

## Parameterization

If you want to add parameters to a lambda, specify the parameter names as you would with a normal function inside the lambda's signature:

```rant
[?: param1; param2] { ... }
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

## Closures

As mentioned previously, a lambda can access variables defined outside of its body.
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

## Limitations on variable capture

Capturing is only supported on variables accessed locally from the function body.
Descoped and explicit global accessors do not capture variables.