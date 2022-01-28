# Piping

When function calls are nested inside each other, they can be difficult to read and understand at a glance:

```rant
[e: [d: [c: [b: [a: 1]; 2]; 3]; 4]; 5] # Welcome to bracket hell
```

An alternative way to write nested function calls is by using iterative (rather than recursive) syntax-- a method known as **piping**.

By using piping, the same expression above can be rewritten with only a single pair of brackets:

```rant
[a: 1 |> b: 2 |> c: 3 |> d: 4 |> e: 5] # Much more readable!
```

In a piped function call, the output of one function is fed into the input of the next. By default, the output is inserted as the first argument;
however, this can be changed by passing the **pipe value** `[]` as an argument:

```rant
[$get-zipper] {
    {<add>|<sub>}
}

# Pass the output of [get-zipper] as the third argument for [zip]
[get-zipper |> zip: (1; 2; 3); (4; 5; 6); []]
```

If the pipe value is a `function`, you can call it directly using an anonymous call:

```rant
[$get-math-func] {
    {<add>|<mul>|<sub>|<div>}
}

# Get a random math function and call it, passing in two numbers
[get-math-func |> ![]: 3.0; 2.0]
```

## Behavior with temporal arguments

Temporal arguments in piped calls behave differently than those in nested calls.

To illustrate this, suppose we have a call to `[foo]` that passes its return value into `[bar]`.

In the nested scenario, a temporal argument in `[foo]` will not duplicate the call to `[bar]`:

```rant
[bar: [foo: **(1; 2; 3)]]
# -> [bar: [foo: 1][foo: 2][foo: 3]]
```

In the piped scenario, the temporal argument in `[foo]` duplicates the entire call chain:

```rant
[foo: **(1; 2; 3) |> bar]
# -> [bar: [foo: 1]]
# -> [bar: [foo: 2]]
# -> [bar: [foo: 3]]
```

## Assignment pipe

There is another pipe operator called the **assignment pipe** (`>`) which lets you assign pipeval to a variable inside your call chain.
This can save some nesting and make your code more readable. You can also use it in temporal calls to perform multiple assignments.

The assignment pipe must appear at the end of the call chain.

```rant
<$test>
[upper: "hello!" > test] # same as <test = [upper: "hello!"]>
[assert-eq: <test>; "hello!"]
```

You can also create new variables from assignment pipes:
```rant
[rand: 1; 100 > $n] # same as <$n = [rand: 1; 100]>
```

Call chains ending in an assignment pipe are automatically sinked.