# Variables and accessors

Variables enable you to store and retrieve values.

Rant is a dynamically-typed language, meaning that variables have no set type;
for example, you can initialize a variable with an integer, and change it later on to a string.

## Accessors

**Accessors** are the central means of reading and writing data in Rant, 
and are denoted by a pair of angle brackets.

They have several uses:
* defining new variables
* getting/setting variable values
* accessing elements in collections

Accessors have three subtypes: **definitions**, **setters**, and **getters**.

### Definitions

A **definition** creates a new variable in the current scope.
They are denoted by placing a `$` symbol before the variable name.

It is optional to assign a value in a definition.
You can leave the assignment part out and it will be initialized to the empty value (`~`).

```rant
# Define a variable `name` but leave it empty (value is `~`)
<$name>

# Define a variable `name` and assign it the string "Nick"
<$name = Nick>
```

### Setters

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

### Getters

A **getter** retrieves some value and prints it to the output.

Attempting to retrieve a variable that does not exist causes a runtime error.

```rant
# Get value of `name` (note the lack of '$')
<$name = Robin>
My name is <name>.\n # Prints "My name is Robin."
```

### Providing a default value when a getter fails

If a getter fails (due to a missing variable, index, or key), the user may sometimes want to provide a default value to fall back on
instead of raising an error. To do this, a **fallback expression** can be added to the end of the getter.

A fallback expression only runs if the data requested by the associated getter is not found; otherwise, it is ignored completely.

#### Example

```rant
# Store a value to use as a fallback
<$fallback = "I don't exist!">

{
    # Define a variable `foo`
    <$foo = "I exist!">

    # Get `foo` with fallback
    <foo ? <fallback>> # -> "I exist!"
}\n

# Getting `foo` again out of scope will trigger the fallback
<foo ? <fallback>> # -> "I don't exist!"

# Getting `foo` without a fallback here would crash the program
<foo> # error
```

## Multi-part accessors

To aid readability, Rant also allows you to place several access operations in a single accessor block.
Simply end each operation with a semicolon; the final semicolon is optional and may be omitted.

```rant
<$first-name = John; $last-name = Smith; $full-name = <first-name>\s<last-name>;>
```

## Anonymous accessors

In order to access a key or index on a value, it normally must be stored in a variable; 
however, **anonymous accessors** remove this requirement by accepting a raw value instead of a variable name.

To create an anonymous accessor, replace the variable name in the accessor with `!` followed by a single expression 
(block, collection, accessor, function call, etc.) and write the rest of your access path as normal.

Both getters and setters can be made anonymous; however, anonymous setters must include at least one index or key.

#### Example 1

```rant
# Create two lists
<$list1 = (1;2;3;4;5;6;7;8)>
<$list2 = (a;b;c;d;e;f;g;h)>

# Create a function that returns one of two lists
[$get-either-list]{{<list1>|<list2>}}

# Call [get-random-list] and get the 4th item (index 3) of the returned list
<![get-either-list]/3> # Returns either '4' or 'd'
```

#### Example 2

```rant
# Get the first letter of a string literal
<!"hello"/0> # Returns 'h'
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

### The 'descope' operator

If a child scope shadows a parent variable and you want to access the parent variable explicitly, you can use the **descope operator**.

To do this, prefix the variable name with a `^` character.

```rant
<$a = foo>
{
    <$a = bar>
    Shadowed: <a>\n
    Descoped: <^a>\n
}

##
    Output:

    Shadowed: bar
    Descoped: foo
##
```

Adding more than one `^` character in a row will skip up to that many scopes.
These operations are called "_n_-descopes", where _n_ is the number of scopes skipped:
For example, `<^^foo>` is a 2-descope, `<^^^foo>` is a 3-descope, and so on.

```rant
# Define `test`
<$test = foo>
{
    # Shadow `test`
    <$test = bar>
    {
        # Shadow `test` again
        <$test = baz>
        <^^test> <^test> <test>
    }
}
## Output: "foo bar baz"
```

While the compiler imposes no explicit limit on descope depth, use cases for large descope depths are rare and it is recommended to avoid them when possible.

```rant
# An example of a 360-descope.
<^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
foo>
```

### Explicitly accessing global variables

The top level of a Rant program implicitly defines a local variable scope; 
because of this, top-level variables will only persist for the duration of the program.

To explicitly access a variable in the global scope, prefix the path with the `/` character.

Similarly to the descope operator, this method also allows you to override shadowing on globals.

```rant
<$foo = Hello from program scope!>
<$/foo = Hello from global scope!>

Local: <foo>\n
Global: </foo>\n

##
    Output:

    Local: Hello from program scope!
    Global: Hello from global scope!
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
