# Templates

Templates allow types to be a parameters for functions, methods, classes and interfaces.

## Templates types

- Templates types are the types pararameters. For example, in `<T, U>`, `T` and `U` are template types.
- Template types can only be "uppercase single letters of the english alphabet", with the exception of `I`. At the same time, "uppercase single letters of the english alphabet" can't be used for any other thing that are not templates types.
- By defualt, all template types are classes (and interfaces). To override this behavior, you must use _template types qualifiers_.

### Templates types qualifiers

| Qualifier | Meaning | Notes |
| --- | --- | --- |
| `class` | Template type is a class or an interface | Default behavior |
| `interface` | Template type is an interface |  |
| `basic` | Template type is a basic type |  |
| `type` | Template type may be of any type |  |

As a non-written rule (that I'm writting right now), classes template types are defined with the letter `T`, then `U`, `V` and so on. Basic types starts with `B`, `C`, `D` and so on. This is not enforced.

## Syntax

### Function templates

```
// A function with two type parameters
SomeType functionName<T, U>(T param, int64 someNumber, U otherParam);

// The return type can even be the template type.
T otherFunction<T>(T aRandomParam);
```

In functions templates, there must always be at least one parameter of each template type. For example, a function that has 3 template types, `T`, `U` and `V`, must declare at least one param of type `T`, at least one param of type `U` and at least one param of type `V`.

### Classes templates

```
class SomeClass<T, U>{
    T someMagicAttribute;
    T otherAttribute[];
}
```

As opposed to function templates, a class template is not obligated to use all of its template types.

### Method templates

Methods that are not in a template class works the same as a function template.

Methods that are in a template class:
- Has all the template types provided by the class.
  - For example, a method of a class class with types `T` and `U` have available `T` and `U` without the need to ask for them again.
    ```
    // Note that the methods does not have any <T, U>
    class SomeClass<T, U>{
        U methodName(char value);
        
        T otherMethod(T *blah, U blop[]);

        int64 simple(int32 fdsa);
    }
    ```
- If for some reason, a method needs an extra template type not provided by the class, it can ask it itself.
  - Equal to function templates, this method must have a parameter for every template type it ask for.
    ```
    class SomeClass<T, U>{
        U namingIsHard<basic M, basic W>(M mini, W wumbo);
    }
    ```

### Interface templates

Every rule of class templates and method templates apply for interfaces.

## `implements` and `extends`

If you want that the template type is a child class of a specific class, or implements a specific interface, you can specify it using the `implements` and `extends` keywords.

For example:
```
class Water<T extends OtherClass, U implements FancyInterface, CoolInterface>{
    // T must by a child class of "OtherClass"
    // U must implement the interfaces "FancyInterface" and "CoolInterface".
}

// You can combine them
class Wotah<T implements FancyInterface, Cool extends OtherClass, ChildClass>{
    // T must
}
```

If you use the `interface` qualifier on the template type, it can only use the `implements` keyword, not the `extends` keyword.

If the template type has the `basic` or `type` qualifier, it does not have avaliable the `implements` neither the `extends` keywords.


## Restrictions

- Templates types can't be declared as pointer or array in their first declaration.
    ```
    // <T *> is not allowed.
    // <U []> is not allowed either.
    class NamingIsHard<T *, U []>{

    }

    class HardIsNaming<T, U>{
        // Allowed.
        T *fdsa; 

        // valid
        void example(U param[]);

        // Why is this allowed?
        void oraoraora(T **(*(**name[])[][])[]);
    }
    ```
