# Comparison of Rant 3 and 4

Rant 3 (deprecated as of June 2020) was released in April 2017 and was the last version of the "original" Rant, which had several critical design flaws
that version 4 aims to address.

While Rant 4 includes many aspects of the "original" syntax, it is **not** backwards-compatible and both should be considered as completely different languages.

## Feature breakdown

| Feature name                                |              Rant 3              |              Rant 4               |
|---------------------------------------------|:--------------------------------:|:---------------------------------:|
| Blocks                                      |             &#x2705;             |             &#x2705;              |
| Block weights                               |             &#x2705;             |             &#x2705;              |
| Selectors                                   |      🤔<br/>*(named only)*       |             &#x2705;              |
| Queries                                     |             &#x2705;             |             &#x274c;              |
| Variables                                   |   🤔<br/> *(via stdlib only)*    | &#x2705;<br/>*(language support)* |
| Variable access fallbacks                   |             &#x274c;             |             &#x2705;              |
| Named functions                             |             &#x2705;             |             &#x2705;              |
| Variable capture in functions               |             &#x274c;             |             &#x2705;              |
| Anonymous functions                         |             &#x274c;             |             &#x2705;              |
| Variadic parameters                         | 🤔<br/>*(stdlib functions only)* |             &#x2705;              |
| Collection initializers                     |             &#x274c;             |             &#x2705;              |
| Stored blocks                               |             &#x274c;             |             &#x2705;              |
| Slice notation                              |             &#x274c;             |             &#x2705;              |
| Dependency management                       |    &#x2705;<br/>*(packages)*     |     &#x2705;<br/>*(modules)*      |
| Resource management                         |    &#x2705;<br/>*(packages)*     |   &#x2705;<br/>*(data sources)*   |
| Function composition                        |             &#x274c;             |             &#x2705;              |
| Parameter spread notation                   |             &#x274c;             |             &#x2705;              |
| Print support for non-string values         |             &#x274c;             |             &#x2705;              |
| Explicit global accessors                   |             &#x274c;             |             &#x2705;              |
| Explicit parent scope accessors (descoping) |             &#x274c;             |             &#x2705;              |
| Unit type                                   |             &#x274c;             |             &#x2705;              |

<p align="center">
(&#x2705; = implemented; &#x274c; = not implemented; 🤔 = limited implementation)
</p>


## Resource management

Rant 3 had a resource management system that used .rantpkg files to load collections of programs and string tables.
This required the use of a separate command-line tool to compile package files.

In Rant 4, this system has been replaced by two separate systems: 
**modules** now handle code dependency management, and **data sources** introduce a more flexible way to import external data.

## Querying

Rant 3 included a query expression system baked into the language that enabled the user to filter and print random entries from string tables.
In Rant 4, this has been removed in favor of using data sources to handle this use case instead.

## Variables

Variables in Rant 3 had no special syntax, so they had to be interacted with through standard library functions like `[v]`, `[vn]`, and `[vs]`.

Rant 4 replaces this clunky system with **accessors**, providing a rich and flexible interface to read and write variables of all types.

### Example

```rant
# Rant 3 example of adding two variables together
[vn: foo; 1]
[vn: bar; 2]
[add: [v: foo]; [v: bar]]
# -> 3


# Rant 4 equivalent
<$foo = 1; $bar = 2>
[add: <foo>; <bar>]
# -> 3
```

## Printing

Rant 3's printing system worked with strings only; this made operations on non-string types, such as numbers and collections, an extremely laborious task
requiring several specialized standard library functions to perform simple tasks like retrieving a value from a list.

Most data types supported by Rant 4 can be created using literals or collection initializers, and printing them produces a value of the same type rather than always
coercing to a string.

## Functions

Rant 3 had two distinct types of functions: **native functions**, which made up the standard library and could not be manually created, and **subroutines**, which were user-definable, required a `$` prefix, and lived in a separate object space from regular variables. This system confused a lot of people.

Rant 4 has a single `function` type that represents all functions-- native or otherwise. Functions are stored like any other variable type. 
In addition, the language also supports anonymous functions/closures for creating callbacks, which Rant 3 cannot do.

## Collections

Rant 3 had `list` and `map` types, but they could only be created through standard library functions.
This produced code that was hard to read and closely-coupled collection data to variables, which greatly limited their usability.

Rant 4 includes collection initializer syntax, which enables you to create lists and maps without requiring function calls or temporary variables.

## Stored blocks

Rant 3 allowed blocks to be passed as values using `lazy parameters`, which were the closest thing the language had to lambdas.
This allowed them to be resolved multiple times, but their use was limited to within the body of the function on which the parameter was attached.

In Rant 4, blocks can be marked as "deferred" to store them as a value, allowing them to be treated as values and resolved later on using the `[resolve]` function.

### Example

```rant
# Rant 3 example of resolving a block twice
[$[do-it-twice: @expr]:
    [rep: 2]
    {[arg: expr]}
]
[$do-it-twice: {{heads|tails}\n}]


# Rant 4 equivalent
[$do-it-twice: expr] {
    [rep: 2]
    [resolve: <expr>]
}
[do-it-twice: <>{{heads|tails}\n}]
```

## Variadic and optional parameters

Rant 3 only supported variadic and optional parameters on native functions. In Rant 4, any function, inluding user-created functions and lambdas, can include optional and variadic parameters.

## Selectors

Rant 3 managed active selectors in a separate object space that persisted for the lifetime of the program. All selectors required names to be used.
This behavior wasn't very clear to most users, and scoping selector lifetimes was impossible.

In Rant 4, selectors are represented as values of type `special`, which can be used once or stored in variables for later.

### Examples

**Reusing a selector**
```rant
# Old Rant 3 way of using selectors
[x:foo;locked]  # [x] creates, stores, and applies a named selector
{a|b|c|d|e|f|g|h}
[x:foo;locked]  # it's unclear from any one [x] call where 'foo' is created
{1|2|3|4|5|6|7|8}


# Rant 4 equivalent
<%sync = [mksel: one]>  # [mksel] returns a new selector
[sel: <sync>] {a|b|c|d|e|f|g|h} # [sel] applies a selector
[sel: <sync>] {1|2|3|4|5|6|7|8}
```

**Single-use selector**
```rant
# Rant 3 single-use selector to shuffle 8 letters
# Even though it's only used once, a name is required
[x:foo;deck][rep:each]{A|B|C|D|E|F|G|H}
# 'foo' then has to be manually destroyed
[xdel:foo]


# Rant 4 equivalent
# [sel] creates & applies a temporary selector if the user supplies a selection type
# You could also use [mksel: deck |> sel] to be more explicit
[sel:deck] [rep:all] {A|B|C|D|E|F|G|H}
```