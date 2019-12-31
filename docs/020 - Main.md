# Main

The `main` function is the entry point of any program written in this language.

Since every function must be declared and defined inside namespaces, a special `main` namespace exists. In the `main` namespace can only contain one function, the `main` function.

The `main` function can only be defined once in the whole program.

The `main` function can have one of the following signatures:
- `int32 main();`
- `int32 main(usize_t argc, char **argv);`
  - `argc` contains how many arguments are passed to the program.
    - The program's name usually counts as a parameter.
  - `argv` contains the arguments passed to the program.
    - `argv[0]` has the program's name.
    - `argv[argc]` has `nullptr`.
      - The last argument is always `nullptr`;
    - `argv[i]`, with `0 < i < argc`, contains a program parameter.
    - `argv[i]`, with `i > argc` or `i < 0`, is _undefined behavior_.
- `int32 main(char *argv[]);`
  - `argv.len` contains how many arguments (plus one) are passed to the program.
    - The program's name usually counts as a parameter.
  - `argv` contains the arguments passed to the program.
    - `argv[0]` has the program's name.
    - `argv[argv.len-1]` has `nullptr`.
      - The last argument is always `nullptr`;
    - `argv[i]`, with `0 < i < argv.len - 1`, contains a program parameter.
    - `argv[i]`, with `i >= argv.len` or `i < 0`, will throw an exception.
      - `i >= argv.len` will throw `IndexOverflowException`.
      - `i < -var.len` will throw `IndexUnderflowException`.

Meaning of the return value of `main`:
- Zero. Indicate successful termination.
- Non-zero. Indicate unsuccessful termination.

The `main` function can be called from any point of the program.
