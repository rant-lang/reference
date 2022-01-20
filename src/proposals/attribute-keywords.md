# Attribute keywords

{{ #include _proposal_msg.md }}

A Rant program has access to certain persistent runtime data, such as the current state of a repeater or the active attribute frame.
As these are always present in a program, it would be sensible to treat them as intrinsic variables rather than exposing
them only through standard library functions.
In the interest of doing this, the following new keywords are proposed:

## @step

Constant.

The `@step` keyword prints the current step number of the active block, starting at 0.

```rant
@rep 10:
@sep ,\s:
{
    @step + 1
}

# 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```

## @total

Constant.

The `@total` variable reflects the total number of steps that the active block will take.
If the number of steps is infinite, the value will be `<>`.

```rant
@rep 10:
@sep ,\s:
{
    {@step + 1}\/@total
}
```

## @rep

Mutable.

`@rep` reflects the current repeater mode stored in the topmost attribute frame.

```rant
# Setting @rep with a setter
<@rep = 3> { ... }

# Shortcut
@rep 3: { ... }
```

## @sep

Mutable.

`@sep` reflects the current separator stored in the topmost attribute frame.

```rant
# Setting @sep with a setter
<@sep = \s>

# Shortcut
@sep \s: { ... }
```

## @sel

Mutable.

`@sel` reflects the current selector stored in the topmost attribute frame.

```rant
<%sync = [mksel: forward]>

# Setting @sel with a setter
<@sel = <sync>> { ... }

# Shortcut
@sel <sync>: { ... }
```

## @mut

Mutable.

`@mut` reflects the current mutator function stored in the topmost attribute frame.

```rant
# Setting @mut with a setter
<@mut = [?: el] { @rep 3: {[el]} }> { ... }

# Setting @mut with a function definition
[@mut: el] {
    @rep 3: {[el]}
}
{ ... }

# Shortcut
@mut [?: el] { @rep 3: {[el]} }: { ... }
```