# Function composition

When function calls are nested inside each other, they can be difficult to read and understand at a glance:

```rant
[e: [d: [c: [b: [a: 1]; 2]; 3]; 4]; 5] # Welcome to bracket hell
```

An alternative way to write nested function calls is by using iterative (rather than recursive) syntax-- a method known as **function composition**.

By using function composition, the same expression above can be rewritten with only a single pair of brackets:

```rant
[a: 1 |> b: 2 |> c: 3 |> d: 4 |> e: 5] # Much more readable!
```

In a composed function, the output of one function is fed into the next. By default, the output is inserted as the first argument;
however, this can be changed by passing the **composition value** `[]` as an argument:

```rant
[$get-zipper] {
    {<add>|<sub>}
}

# Pass the output of [get-zipper] as the third argument for [zip]
[get-zipper |> zip: (1; 2; 3); (4; 5; 6); []]
```

If the composition value is a `function`, you can call it directly using an anonymous call:

```rant
[$get-math-func] {
    {<add>|<mul>|<sub>|<div>}
}

# Get a random math function and call it, passing in two numbers
[get-math-func |> ![]: 3.0; 2.0]
```

## Behavior with temporal arguments

Temporal arguments in composed function calls behave differently than those in nested function calls.

To illustrate this, suppose we have a call to `[foo]` that passes its return value into `[bar]`.

In the nested scenario, a temporal argument in `[foo]` will not duplicate the call to `[bar]`:

```rant
[bar: [foo: **(1; 2; 3)]]
# -> [bar: [foo: 1][foo: 2][foo: 3]]
```

In the composed scenario, the temporal argument in `[foo]` duplicates the entire call chain:

```rant
[foo: **(1; 2; 3) |> bar]
# -> [bar: [foo: 1]]
# -> [bar: [foo: 2]]
# -> [bar: [foo: 3]]
```