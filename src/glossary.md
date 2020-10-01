# Glossary

### Accessor

Accessors are program elements that read or write values. They are the primary means of interacting with variables.

There are three types of accessors: **getters**, **setters**, and **definitions**.

### Access path

An access path is used to access variables or items in collections. They consist of `/`-delimited series of identifiers, keys, and indices. 

### Attributes

Attributes modify **block** behavior, such as how many times a block repeats or how it selects elements.

Attributes can be set through **attribute functions**.

### Attribute frame

An attribute frame is a full set of all available attributes. A program's attribute stack always contains at least one frame.

### Attribute functions

A function that reads or writes an **attribute**.

### Attribute stack

Each program maintains an "attribute stack", which stores and provides **attributes** to **blocks**.
When a block runs, it consumes the attributes in the topmost frame of the attribute stack, replacing them with their default values.

The user can add and remove frames from the attribute stack to preserve attributes for later use.

### Block

A block is a section of a Rant program subdivided into zero or more parts.
Blocks act as variable scopes and can be combined with various constructs to produce a wide variety of behaviors.

### Closure

A closure is a function that captures one or more variables from its environment.

### Construct

A construct is a group of one or more runtime variables can be used to interact with the Rant runtime 
and customize various aspects of program behavior.

### Definition

A definition is an accessor type that creates a new variable.

### Dynamic key

A dynamic key is an access path key, consisting of a single-element block, that must be resolved before the containing path can be read. 
The block resolves to the final key or index that will be inserted into the path.

### Formatter

A formatter is a runtime component that passively changes the output in some way.

### Fragment

A fragment is a sequence of any non-whitespace, non-reserved characters found in a Rant program.

### Getter

A getter is an accessor type that retrieves a value from a variable or collection.

### Hint

A hint is a compile-time operation that informs the Rant compiler that the next program element is expected to print to the output.

### Identifier

A name assigned to a **variable** or **module**.

Identifiers enforce specific formatting requirements to ensure consistency:

* Must contain **at least one** alphanumeric character.
* Must only contain alphanumeric characters, underscores, and hyphens.

### List

A list is an ordered collection of values, accessible by index.

### Map

A map is a collection of key-value pairs, also known as an "associative array".

### Module

A module is a library of Rant functions that can be loaded into another program using the `[require]` function.

### Repeater

A block that can iterate multiple times. Repeaters are created by calling `[rep]`.

### Resolution

Resolution refers to the process of producing an output from a block, after which the block is referred to as 'resolved.' 

### Resolver

The component of the Rant runtime that handles block resolution.

### Setter

A setter is an accessor type that writes to a variable or collection.

### Sink

A sink is an operation that suppresses the output of a program element while still allowing its execution.