# Type qualifiers

- `const`
- `volatile`
- `restrict`
- `atomic`
- `nodestroy`
  - The compiler will not call the destructor of an object tagged `nodestroy` at the end of its scope. It is programmer's responsability to destroy the object.
    - If a function is tagged `nodestroy`, the compiler will not call the destructor for the returned value.
    - If a function is not tagged `nodestroy`, but returns an object tagged `nodestroy`, inside that function the object will not be destroyed, but the object will be destroyed at the end of the scope which called the function.
      - In this case, the retuned value may be assigned to a variable declared `nodestroy`. If that happens, its constructor will not be called at the end of the scope.
    - If a function is tagged `nodestroy`, but returns an object that is **not** tagged `nodestroy`, the compiler must emit an error.
  - If combined with any type that has no destructors (basic types, pointers, etc), the compiler may emit a warning.
