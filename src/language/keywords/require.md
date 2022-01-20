# @require

The `@require` keyword is used to import a module.

## Examples

**Import a module with the original name**
```rant
# Imports as 'test-module'
@require "test-module"
```

**Import a module with an alias**
```rant
# Imports as 'tm'
@require tm: "test-module"
```

## See Also

* [Modules](./modules.md)