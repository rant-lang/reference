# List of compiler messages

All messages (errors, warnings, etc) returned by the Rant compiler include a code that identifies the nature of the message.
For convenience, this page lists all currently used compiler message codes and what they mean.

## R0000 (unexpected token)

*Error*

A token was encountered by the compiler that it doesn't know what to do with.
The token in question is probably either:

* reserved for a specific purpose and can't be treated like text (e.g. a right brace outside with no matching left brace)
* not allowed in the current context (e.g. a semicolon after a function name)

## R0001 (expected token)

*Error*

A token was expected at a certain point in the code, but was missing.

## R0002 (unclosed block)

*Error*

An unclosed block was found. The block has a left brace (`{`) but no closing right brace (`}`).

## R0003 (unclosed function call)

*Error*

An unclosed function call was found. The function call has a left bracket (`[`) but no closing right bracket (`]`).

## R0004 (unclosed function signature)

*Error*

An unclosed function signature was found. The signature has a left bracket (`[`) but no closing right bracket (`]`).

## R0005 (unclosed accessor)

*Error*

An unclosed accessor was found. The accessor has a left angle bracket (`<`) but no closing right angle bracket (`>`).

## R0006 (unclosed string literal)

*Error*

An unclosed string literal was found. The literal has an opening quotation mark but was not terminated.

## R0007 (unclosed list expression)

*Error*

An unclosed list expression was found. The expression has an opening parenthesis (`(`) but no closing parenthesis (`)`).

## R0008 (unclosed map expression)

*Error*

An unclosed map expression was found. The expression has an opening parenthesis (`(`) but no closing parenthesis (`)`).

## R0021 (invalid parameter order)

*Error*

A function signature was found with parameters in an unsupported varity order.
This usually means that you tried to add required parameters after a variadic or optional parameter.

The expected ordering is:

1. required parameters
1. optional parameters
1. variadic parameter

## R0022 (missing function body)

*Error*

A function definition was found that has a signature but no body.

## R0023 (unclosed function body)

*Error*

A function body was found that has an opening brace (`{`) but no closing brace (`}`).

## R0024 (invalid parameter)

*Error*

A function signature contains a parameter with an invalid name.

## R0025 (duplicate parameter)

*Error*

A function parameter was found with a name matching a previous parameter in the same signature.

## R0026 (multiple variadic parameters)

*Error*

Multiple variadic parameters were found on the same function signature. 
Functions may only have at most one variadic parameter.

## R0040 (dynamic key with multiple elements)

*Error*

A dynamic key block was found with multiple elements. Dynamic keys may only contain a single element.

## R0041 (function body with multiple elements)

*Error*

A function body block was found with multiple elements. Function bodies may only contain a single element.

## R0060 (anonymous value assignment)

*Error*

A setter was found attempting to set a value on an anonymous expression.

## R0061 (missing identifier)

*Error*

An accessor was found that has no identifier.

## R0062 (invalid identifier)

*Error*

An accessor with an invalid identifier was found.

## R0063 (accessor starts with index)

*Error*

An accessor was found that has an index for the first part of the path.
An accessor path may only start with a variable name or anonymous value expression.

## R0064 (accessor starts with slice)

*Error*

An accessor was found that has a slice for the first part of the path.
An accessor path may only start with a variable name or anonymous value expression.

## R0065 (invalid slice bound)

*Error*

A slice expression was found that includes an invalid bound value.

## R0066 (nothing to pipe)

*Error*

A function call chain attempted to reference a piped value in the first call.

## R0067 (fallible optional parameter access)

*Error*

A accessor references an optional parameter, but the parameter has no fallback expression and the accessor in question provides no fallback.
Safe access cannot be guaranteed.

## R0100 (constant reassignment)

*Error*

A setter attempted to reassign a constant.

## R0101 (constant redefinition)

*Error*

A definition attempted to redefine a constant in the same scope.

## R0130 (invalid sink)

*Error*

A sink operator was found before a program element that does not support sinking.

## R0131 (invalid hint)

*Error*

A hint operator was found before a program element that does not support hinting.

## R0200 (invalid keyword)

*Error*

A `@keyword` not recognized by the compiler was found.

## R0201 (weight not allowed)

*Error*

A `@weight` expression was found in a context where it is not allowed.

## R1000 (unused variable)

*Warning*

A variable was defined but not referenced by its containing scope.

## R1001 (unused parameter)

*Warning*

A parameter defined by a function was not referenced by its body.

## R1002 (unused function)

*Warning*

A function was defined but never called within its containing scope.

## R1003 (empty function body)

*Warning*

A function was defined with an empty body (i.e. it doesn't do anything).

## R1004 (nested function definition was marked constant)

*Warning*

A function defined inside of a collection was marked as constant; 
this is not supported and the function will be mutable.

## R2100 (file not found)

*Error*

A file requested by the compiler could not be found.

## R2101 (filesystem error)

*Error*

A filesystem error (e.g. permission error, file in use, ...) occurred while the compiler was trying to access a file.
The message description will specify the exact nature of the error.