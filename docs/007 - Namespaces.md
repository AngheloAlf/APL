# Namespaces

A namespace is a named scope, allowing to make declarations and definitions without name collisions (Note: the name of the namespace could collide with other namespace).

Most of the code can only be declared or executed inside namespaces, removing the posibility to do it in the global scope. The language itself is the only one that can put functions or classes in the global scope.

To use namespaces:

```
namespace name{
T some_function(T var);
}
```

Since namespaces are the very basic block and will be everywhere, it is recommended to not indent.

It is recommended to have one namespace per file. But a namespace can be defined across multiples files. // TODO: provide example.

To use a function or class from other namespace, you should refer to it as `otherNamespace::someFunction();`.

You can have namespaces inside namespaces.

- Variables may be declared inside a namespace.
- Variables with any of the basic types and defined with the `const` qualifier may be defined alongside its declaration.
- Variables of any other type can't be defined alongside its declaration. 
  - It may be defined inside a function.
  - Using an unitializated variable is _Undefined behavior_. // TODO: change this to be an exception or a compile time error.
