# Lists and maps

Rant's variable system has two collection types: **lists** and **maps**.

## Lists

Lists are editable arrays. Lists may contain multiple types of values.

A list is created by placing the list operator `@` before a block containing the contents of the list.

```rant
# Create an empty list
<$empty-list = @{}>

# Create a list of numbers
<$lucky-numbers = @{1|2|3|5|7|11|13}>

# Create a list of lists
<$important-letters = @{
    @{A|B|C} | @{D|E|F}
}>
```

## Maps

Maps are like lists, but store their values as key-value pairs. Map keys are always strings.

Map creation uses slightly different syntax from lists: instead of `@` before the block, `@:` is used instead.

The block elements must each also contain both a key and value, separated by a `:` character.
If any element of the block is empty or only contains a single component, a compiler error will occur.

Map keys can contain any Rant code, which will be coerced to a string after resolving.

```rant
# Create an empty map
<$empty-map = @:{}>

# Create a map with various value types
<$person = @:{
    name: John|
    age: 25
}>
```

## Retrieving values from lists and maps

Variable accessors can also access individual elements in lists and maps by using the `/` operator:

```rant
<$person = @:{
    name: Bob|
    age: 30|
    hobbies: @{programming|hiking}
}>

name = <person/name>\n
age = <person/age>\n
hobbies = [join:<person/hobbies>;,\s]

##
    Output:

    name = Bob
    age = 30
    hobbies = programming, hiking
##
```