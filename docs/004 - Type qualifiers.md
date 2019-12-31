# Type qualifiers

- `const`
- `volatile`
- `restrict`
- `atomic`

## Functions and methods only

The following qualifiers can only be applied to functions or methods.

- `nodiscard`: If the returned value by the function (or method) is discarded by the caller, the compiler is encouraged to emit a warning.
- `nodestroy`: The compiler will not call the destructor for the returned object (it would normally do if the object was created in this function.). If combined with any type that has no destructors (basic types, pointers, etc), the compiler should emit a warning.
