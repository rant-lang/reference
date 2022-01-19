# Glossary

### Accessor

Accessors are program elements that directly read or write variables or fields. 
They are the primary means of interacting with variables.

There are three types of accessors: **getters**, **setters**, and **definitions**.

### Access path

An access path is used to access variables or items in collections. They consist of `/`-delimited series of identifiers, keys, and indices. 

### Attribute

Attributes are special variables that specify how the next **block** will resolve. 
They are stored in the **attribute stack**.

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

### Block

A block is a section of a Rant program subdivided into zero or more parts.
Blocks act as variable scopes and can be combined with various constructs to produce a wide variety of behaviors.

### Closure

A closure is a function that captures one or more variables from its enclosing scope.

### Construct

A construct is a group of one or more runtime variables can be used to interact with the Rant runtime 
and customize various aspects of program behavior.

### Definition

A definition is an accessor type that creates a new variable.

### Descoping

Descoping is a type of variable access that explicitly retrieves a variable from a parent scope, overriding **shadowing**.

### Dynamic key

A dynamic key is an access path key, consisting of a single-element block, that must be resolved before the containing path can be read. 
The block resolves to the final key or index that will be inserted into the path.

### Formatter

A formatter is a runtime component that passively changes the output in some way.

### Fragment

A fragment is a sequence of any non-whitespace, non-reserved characters found in a Rant program.

### Function percolation

Function percolation is the ability of function calls to access functions from parent scopes despite **shadowing** by non-function variables.
It is an implicit form of **descoping**.

### Getter

A getter is an accessor type that retrieves a value from a variable or collection.

### Hint

A compile-time flag that marks the following program element as text.

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

A module is a library of Rant functions that can be loaded into another program using the `[require]` function.

### Repeater

A looping block. Blocks can be made to loop by setting the repetition count with `[rep]`.

### Resolution

Resolution refers to the process of Rant selecting which branch to run on a **block**.

### Resolver

The component of the Rant runtime that handles block resolution.

### Shadowing

A variable is **shadowed** (hidden) when it is overridden by a variable of the same name in a child scope.

### Setter

A setter is an accessor type that writes to a variable or collection.

### Sink

A compile-time flag that marks the following program element as non-text.

### Varity

Varity is the classification of a function parameter relating to the number of values it expects and can accept.

Rant has four varity types:
* **Required** (accepts one value)
* **Optional** (accepts zero or one values)
* **Optional-variadic** (accepts zero or more values)
* **Required-variadic** (accepts one or more values)