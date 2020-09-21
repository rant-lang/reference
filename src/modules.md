# Modules

Rant supports basic dependency management via a **module** system.
Modules are libraries of Rant functions that you can write and load into other Rant programs for use. Each module resides in its own source file.

## Writing modules

A module is simply a Rant program that returns a map containing the module's contents.

Below is a basic example of a very simple module:

```rant
# lol.rant: Laughter Generation Module

<$module = @()>

[$module/cackle: len?] {
  [rep:[alt:<len>;2]]{h{a|e|ee|ue|aa|o}}!!!
}

<module>
```

## Importing modules

A module can be imported using the `[require]` function.
For this example, we'll import the `lol` module previously shown.

```rant
# Looks for `lol.rant` and imports it as map variable `lol`.
# You don't need to specify a file extension.
[require: lol]

# Call the `[cackle]` function from the module
[lol/cackle: 16]
# --> haahoheehehehuehohoheehahohaaheehoheehaa!!!
```

Imported modules are cached by the Rant context running the program.
If you import the same module twice, it will be fetched from cache.

### Compiler errors in modules

Rant needs to compile modules before they can be imported. If a module fails to compile, a runtime error will be triggered with the compiler error list.

## Where Rant looks for modules

When you run `[require]`, Rant looks for the module in two places:

First, Rant will check the **local modules path**. This is usually set up by the host application, but if it's not specified, it defaults to the working directory of the process.

If a local module can't be located, Rant will check the path stored in the `RANT_MODULES_PATH` environment variable; this is your **global modules path**.
If there is no matching module file there, the environment variable is not defined, or the path is otherwise inaccessible, Rant will trigger a runtime error.