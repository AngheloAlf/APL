# Abstract classes (and/or abstract methods)

The `abstract` keyword is a modifier for classes and methods.

`private` and `abstract` modifiers can't be together (?).

## Abstract methods

- When a method has the `abstract` modifier, the method can only be declared. 
- If the same class defines an `abstract` method, an error will be emitted. 
- A class with at least one `abstract` method must be declared `abstract`.

## Abstract classes

- If a class has the `abstract` modifier, the class can't be instantiated.
- A class with the `abstract` modifier may have `abstract` methods.
- An `abstract` class can be used as a type for declaring a variable, but the initialization must be done with a child class that `extends` the abstract class and implements every `abstract` method.
  - In that case, only the methods and attributes that are available to that `abstract` class are available to that variable.
- A class that `extends` an `abstract` class may not implement every `abstract` method of that class, in which case, the new class is `abstract` too and must be tagged `abstract`.

## `extends`

The `extends` keyword may also be used for extending classes that are not `abstract`.
