# Modules

Rant supports basic dependency management via a **module** system.
Modules are libraries of Rant functions that you can write and load into other Rant programs for use. Each module resides in its own source file.

## Writing modules

A module is simply a Rant program that returns a map containing the module's contents. Similar to a regular Rant program, modules are expected have the `.rant` file extension.

Below is a basic example of a very simple module:

```rant
# seq.rant

<%module = (::)>

[$module/fib: n] {
  (:) [rep: <n>] { @edit f: <f> (<f/-2 ? 0> + <f/-1 ? 1>) }
}

<module>
```

## Importing and using modules

A module can be imported using the `@require` keyword or, less commonly, the `[require]` stdlib function.
For this example, we'll import the `seq` module previously shown.

```rant
# Looks for `seq.rant` and imports it as map variable `seq`.
# You don't need to specify the file extension.
@require "seq"

# Call the `[fib]` function from the module
[seq/fib: 16]
# -> (: 1; 1; 2; 3; 5; 8; 13; 21; 34; 55; 89; 144; 233; 377; 610; 987)
```

Imported modules are cached by the Rant context running the program.
If you import the same module twice, it will be fetched from cache.

### Compiler errors in modules

Rant needs to compile modules before they can be imported. If a module fails to compile, a runtime error will be triggered with the compiler error list.

## Where Rant looks for modules

When you use `@require`, Rant looks for the module in the following locations in-order:

1. The requesting program's file location
    * Skipped if the program was not loaded from a file
2. The **local modules path**
    * Defaults to the current working directory, but the host app can reconfigure it
3. The **global modules path**
    * Set by the `RANT_MODULES_PATH` environment variable
    * Can be disabled by the host app

If Rant cannot locate a module with a matching path and name, 
it will trigger a runtime error.

### Relative paths in `@require`

`@require` can also accept a relative path to a module.
This makes it possible to access modules in subfolders of any of the module search locations.

For example, if your application has a `rant_modules` subfolder in its main directory, you can import modules from it like this:

```rant
# Imports `my-module`
@require "rant_modules/my-module"
```