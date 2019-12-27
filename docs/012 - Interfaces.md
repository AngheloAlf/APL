# Interfaces

Interfaces allows to provide methods declarations without providing an implementation. The implementation for each method should be provided in a class that `implements` it.

## Syntax

```
interface Cool{
    /*Some cool methods*/
}

class VeryCoolClass implements Cool{
    /*Implement Cool interface's methods*/

    /*Add new methods, and/or overload Cool interface's methods*/
}
```

A class may `implements` multiples interfaces, each one separated by a comma.

```
class OtherCoolClass implements Cool, Cooler, Coolest{
    /*...*/
}
```

- An interface can `implements` other interfaces.
- An interface can be used as a type, but an actual (not `abstract`) class that `implements` this interface must be used to initializate that variable.
  - In that case, only the methods that are available to that `interface` are available to that variable.

## Restrictions

- An interface can't have attributes.
- An interface can't have any special methods, like `constructor`.

## `implements` and `extends` together

If a class wants to `extends` one (or more) class(es) and `implements` one (or more) interfaces, it can be done. The `implements` keyword must be before the `extends` keyword. For example:

```
class SomeRandomStuff implements MyLittleInterface, AnotherInterface extends VeryClass, TheUltimateClass{
    /*...*/
}
```
