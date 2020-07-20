# Glossary

### Block

A block is a section of a Rant program subdivided into zero or more parts.
Blocks act as variable scopes and can be combined with various constructs to produce a wide variety of behaviors.

### Block attributes

Block attributes provide a way to customize the resolver's behavior through the variable system, such as changing iteration count.

### Channel

A channel is an independent stream of output from a Rant program. Programs may have more than one channel.

### Construct

A construct is a group of one or more runtime variables can be used to interact with the Rant runtime 
and customize various aspects of program behavior.

### Formatter

A formatter is a runtime component that mutates output in some way.

### Fragment

A fragment is a sequence of any non-whitespace, non-reserved characters found in a Rant program.

### Hint

A hint is a compile-time operation that informs the Rant compiler that the next program element is expected to print to the output.

### Resolution

Resolution refers to the process of producing an output from a block, after which the block is referred to as 'resolved.' 

### Resolver

The component of the Rant runtime that handles block resolution.

### Sink

A sink is an operation that suppresses the output of a program element while still allowing its execution.