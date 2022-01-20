# Glossary

### Accessor

Accessors are used to read and write data. They are primarily used to access variables.

There are three types of accessors: **getters**, **setters**, and **definitions**.

### Access path

An access path is the first part of an accessor that specifies what is being accessed. They consist of `/`-delimited series of identifiers, keys, and indices. 

### Attribute

Attributes are special variables that specify how the next **block** will resolve. 
They are stored in frames in the **attribute stack**.

Attributes can be set through **attribute functions**.

### Attribute frame

A full set of all available attributes. The **attribute stack** contains one or more frames, which can be consumed by **blocks**.

### Attribute function

A function that reads or writes an **attribute**.

Attribute functions can only modify the attributes in the topmost frame.

### Attribute stack

Rant maintains an "attribute stack" that stores **attributes** and provides them to **blocks**.
When a block starts resolving, it consumes the attributes in the topmost frame of the attribute stack, replacing them with their default values.

The user can add and remove frames from the attribute stack to preserve attribute frames for later use.

### Auto-hinting

Auto-hinting refers to using the `@text` keyword to mark variables, function parameters, and function return values as text, eliminating the need to add hints to each usage of them.

### Block

A block is a section of a Rant program subdivided into zero or more parts.
Blocks act as variable scopes and can be combined with various constructs to produce a wide variety of behaviors.

### Closure

A closure is a function that captures one or more variables from its enclosing scope.

### Definition

A definition is an accessor type that creates a new variable.

### Descoping

Descoping is a type of variable access that explicitly retrieves a variable from a parent scope, overriding **shadowing**.

### Dynamic key

A dynamic key is an access path key, consisting of a single-element block, that must be resolved before the containing path can be read. 
The block resolves to the final key or index that will be inserted into the path.

### Empty

Empty (also: "emptyval") refers to the value of the `empty` type.

### Expression

An expression is a sequence of Rant **expression units**.

### Expression unit

An expression unit is the smallest component of a Rant program. Examples of expression units inclide fragments, accessors, function calls, and blocks.

### Formatter

A formatter is a runtime component that passively changes the output in some way.

### Fragment

A fragment is a sequence of any non-whitespace, non-reserved characters found in a Rant program.

### Function percolation

Function percolation is the ability of function calls to access functions from parent scopes despite **shadowing** by non-function variables.
It is an implicit form of **descoping**.

### Getter

A getter is an accessor that reads the value at the specified **access path** and prints it.

### Hint

A compile-time flag that marks the following expression unit as text.

### Identifier

A name assigned to a **variable** or **module**.

Identifiers enforce specific formatting requirements to ensure consistency:

* Must contain **at least one** alphanumeric character.
* Must only contain alphanumeric characters, underscores, and hyphens.

### Lambda expression

A lambda expression is an anonymous (nameless) function.

### List

A list is an ordered collection of values, accessible by index.

### Map

A map is a collection of key-value pairs, also known as an "associative array".

### Module

A module is a library of Rant functions that can be loaded into another program with `@require`.

### Pipeval

Pipeval is short for "Pipe value" and refers to the return value of a piped function that has been passed to the next function in a piped call.

### Repeater

A looping block that uses **attributes**. Blocks can be made to loop by setting the repetition count with `[rep]`.

### Resolution

Resolution refers to the process of Rant selecting which branch to run on a **block**.

### Resolver

The component of the Rant runtime that handles block resolution.

### Shadowing

A variable is **shadowed** (hidden) when it is overridden by a variable of the same name in a child scope.

### Setter

A setter is an accessor type that changes the value at the specified **access path**.

### Sink

A compile-time flag that marks the following expression unit as non-text.

### Slice

A slice is an arbitrary range of elements in an ordered collection.

### Splice

A splice is a **setter** that modifies a **slice** of an ordered collection.

### Varity

Varity is the classification of a function parameter relating to the number of values it expects and can accept.

Rant has four varity types:
* **Required** (accepts one value)
* **Optional** (accepts zero or one values)
* **Optional-variadic** (accepts zero or more values)
* **Required-variadic** (accepts one or more values)