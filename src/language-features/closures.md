# Closures

It is sometimes necessary to pass a function as a value rather than define it with a name, so that it can be called elsewhere later on.
This can be done using **closures**, which are an implementation of anonymous functions with the ability to "capture" external variables.

Basic closure syntax with no parameters consists of a `?` symbol inside brackets preceding the function body. 

```rant
# Creates a closure and places it on the output
[?]{Hello from closure!}
```

## Parameterized closures

If you want to add parameters to a closure, specify the parameter names as you would with a normal function inside the closure's signature:

```rant
[?: param1; param2]{ ... }
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

## Behavior of captured variables

As mentioned previously, a closure can access variables defined outside of its body.
When this happens, it "captures" a reference to that variable for use inside the function.
As a result, changes made to a captured variable persist between calls.

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

Capturing is currently only supported on variables accessed locally from the function body.
Descoped and explicit global accessors do not capture variables.