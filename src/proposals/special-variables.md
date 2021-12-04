# Special variables

{{ #include _proposal_msg.md }}

A Rant program has access to certain persistent runtime data, such as the current state of a repeater or the active attribute frame.
As these are always present in a program, it would be sensible to treat them as first-class language features rather than exposing
them through only the standard library.
In the interest of doing this, the following new keywords are proposed as special variable names:

## @step

Constant.

The `@step` variable reflects the current step number of the active block, starting at 1.

```rant
<@reps = 10; @sep = ,\s>
{
    <@step>
}

# 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```

## @step-index

Constant.

The `@step-index` variable reflects the current step index of the active block, starting at 0.

## @reps

Mutable.

The `@reps` variable reflects the current repetition count stored in the topmost attribute frame.

## @sep

Mutable.

The `@sep` variable reflects the current separator stored in the topmost attribute frame.

## @sel

Mutable.

The `@sel` variable reflects the current selector stored in the topmost attribute frame.

## @pipe

Mutable.

The `@pipe` variable reflects the current pipe function stored in the topmost attribute frame.