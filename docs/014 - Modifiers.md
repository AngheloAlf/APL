# Modifiers

Modifiers are use to set specific or modify behavior for classes, methods and functions (attributes too in some rare occasions). This changes will be enforced by the compiler.

- Visibility modifiers: Go read them in the classes chapter, I'm too lazy to copy-paste them here.
- `abstract`

## Functions and methods only modifiers

The following qualifiers can only be applied to functions or methods.

- `nodiscard`: If the returned value by the function (or method) is discarded by the caller, the compiler is encouraged to emit a warning.
- `nodestroy`: The compiler will not call the destructor for the returned object (it would normally do if the object was created in this function.). If combined with any type that has no destructors (basic types, pointers, etc), the compiler should emit a warning.

## Method only modifiers

- `overridecall`
  - If a sub class overrides this method, the original overrided method will be automatically called at the start of the overrider method (unless the overrider method make an explicit call to the overrided method). The overrider method will inherit this behavior (it's recommended to tag the overredier method with this modifier explicity).
- `overloadcall`
  - If a sub class overloads this method, the original overloaded method will be automatically called at the start of each overloader method (unless the overloader method make an explicit call to the overloaded method). 
  - In the super class: A method tagged with this modifier can't be overloaded by the same class, only by sub classes.
