# Accessors

**Accessors** are the central means of reading and writing variable data in Rant.
Accessors are contained within a pair of angle brackets (`< >`).

They have several uses:
* defining new variables
* getting/setting variable values
* accessing elements in collections

Accessors have three subtypes: **definitions**, **setters**, and **getters**.

## Definitions

A **definition** creates a new variable in the current scope.
They are denoted by placing a `$` symbol before the variable name.

It is optional to assign a value in a definition.
You can leave the assignment part out and it will be initialized to empty.

```rant
# Define a variable `name` but leave it empty
<$name>

# Define a variable `name` and assign it the string "Nick"
<$name = Nick>
```

## Setters

A **setter** modifies an existing variable or value.

```rant
# Define a variable
<$name = Bob>
# Overwrite value on existing variable `name`
<name = Susan>
```

Along with setting variables, setters can also write to specific elements of collections.

```rant
<$numbers = (1; 2; 3)>
<numbers/0 = 4> # list is now (4; 2; 3)
```

## Getters

A **getter** retrieves some value and prints it to the output.

Attempting to retrieve a variable that does not exist causes a runtime error.

```rant
# Get value of `name` (note the lack of '$')
<$name = Robin>
My name is <name>.\n # Prints "My name is Robin."
```

## Multi-part accessors

To aid readability, Rant also allows you to place several access operations in a single accessor block.
Simply end each operation with a semicolon; the final semicolon is optional and may be omitted.

```rant
<$first-name = John; $last-name = Smith; $full-name = <first-name>\s<last-name>;>
```

## Variable scope

Variables only live as long as the expression or block in which they are defined.

Blocks, function arguments, setter expressions, dynamic keys, and function bodies are all examples of variable scopes.
As soon as a scope is finished running, all variables defined within it are discarded.

### Child scopes

Child scopes inherit variables from parent scopes. In addition, they may define their own variables.

```rant
{
    <$a = 1>
    {
        <$b = 2>
        [add: <a>; <b>] # Outputs "3"
    }
}
```

### Shadowing

Variables in a parent scope can be temporarily hidden ("shadowed") by defining a variable of the same name in a child scope.

When the child variable goes out of scope, the shadowed parent variable will once again become accessible.

```rant
# Define variable `a` in parent scope
<$a = foo>
a is <a>\n
{
    # Define another variable `a` in child scope
    # Parent variable is not affected
    <$a = bar>
    a is <a>\n
}
# Parent variable takes over after child scope exits
a is <a>

##
    Output:

    a is foo
    a is bar
    a is foo
##
```

## Constants

Constants are much like variables in that they are scoped the same way and store a value.
Unlike variables, however, constants are immutable: they can only be assigned within a definition, and cannot be redefined.

The syntax to define a constant is simple: where variable definitions use `$`, constant definitions use `%`:

```rant
# Variable definition
<$mutable-value = 123>

# Constant definition
<%constant-value = 123>


<mutable-value = 456>   # works as expected
<constant-value = 456>  # error
```

Constants can still be shadowed by child scopes.

```rant
<%foo = 123>
{
    <$foo = 456>    # this is valid since we're not reassigning ^foo
}
```

### By-ref constants have interior mutability

Storing a by-ref type, such as a list or map, in a constant does not prevent its contents from being changed; 
it only guarantees that the reference stored by the constant cannot change.

```rant
# Create a constant list
<%special-list = (1; 2; 3)>

# Modifying the contents is still allowed
[push: <special-list>; 4]   # list now contains (1; 2; 3; 4)

# Swapping out the list itself is not allowed
<special-list = (7; 8; 9)>  # error!
```
