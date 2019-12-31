# Variables

- To declare a variable: `T var;`
  - This can be mixed with pointers and arrays.
- To assign a value to a variable, simply `var = some_value;`
  - In most cases, declaration and assignation can be mixed, for example `T var = some_value`.

If a variable is declared but not defined, it may have a default value depending of it's type.
- Basic types: `0`.
  - `bool` defaults to `false`.
- Pointers: `nullptr`.
- Arrays: `nullptr`.
- Classes does not have a default value.
