# Inheritance

## Syntax

To declare a class that inherits from other class you have to use the keyword `extends`:

```
class ChildExample extends ParentClass{
    /*new member variables*/

    /*new and/or overriden methods*/

    void someCoolFunc(){
        /*cool function stuff*/
    }
}
```

You can also inherits from multiples classes:

```
class MultipleExample extends ChildClass, SomeOtherClass, JustAnotherOne{
    /*new member variables*/

    /*new and/or overriden methods*/
}
```

Either way, the new class inherits all the public and protected members from its parents. The special methods are a special case.

## Method override

You can override any method from the parents classes.

The new method may call the old method. There are two ways to accomplish this.
- Explicity call the original class and method. ``ParentClass::toBeOverloadedMethod(/*params*/);`
- Use the `super->method(/*params*/);` keyword that is available for all child classes.

For example:
```
class Overloading extends ChildClass{
    void someCoolFunc(){
        super->someCoolFunc();
        // ChildClass::someCoolFunc(); // this one works too!

        /*even cooler stuff*/
    }
}
```

When inheriting from multiples classes, it is recommended to use the `Class::method();` syntax. But the `super->method(/*params*/);` one will work too (but take care when using it).

Just for clarification, there is no "variable member override".

## Special methods

- `constructor`.
  - The `constructor` is weird (I'm warning you).
  - Simple inheritance:
    - If there are no `constructor`s in the child class, the child class inherits the parent `constructor`s.
    - If the child class has one or many `constructor`s, the parent `constructor`s are not inherited. In each child `constructor` you must call one parent `constructor`. You can use the `ParentClass::constructor(/*params*/);` syntax or the `super(/*params*/);` syntax.
      - If the parent does not have any `constructor`s, then the child must call the default `constructor`. For example, a call to `super();` without parameters.
      - Not calling a parent `constructor` in the child `constructor` (or not doing it as the very start of the `constructor`) must emit an error from the compiler.
  - Multiple inheritance:
    - The child class does not inherit any parent `constructor`.
    - The child class must have at least one `constructor`.
    - The child class must call one `constructor` from each parents in every `constructor`.
    - The calling order of the `constructor`s may be in any order, but it is recommeded to call the `constructor`s in the same order as they are `extends`ed, from left to right.
- `destructor`.
  - The parents `destructor`s are automatically called after the child class `destructor` is called.
  - The order of the call of `destructor`s is the same as they are `extends`ed, but from right to left.
  - The child can't call the parent `destructor`s.
- `ptrConstructor`:
  - The parents `ptrConstructor`s are automatically called before the child class `ptrConstructor` is called.
  - The order of the call of `ptrConstructor`s is the same as they are `extends`ed, from left to right.
  - The child can't call the parent `ptrConstructors`.
- `ptrDestructor`.
  - The parents `ptrDestructor`s are automatically called after the child class `ptrDestructor` is called.
  - The order of the call of `ptrDestructor`s is the same as they are `extends`ed, but from right to left.
  - The child can't call the parent `ptrDestructor`s.

## Name collisions

- Private members are not exposed to the childs classes. So, a parent class and the child class can have the members called the same, without collision (as long as the member of the parent class is private). This also applies for parents private members when the children do a multiple inheritance.
- Protected and public members:
  - Simple inheritance:
    - Methods with the same name may be overloaded and/or overrided without problems.
    - Child members can't have the same name as any of the parent variables members.
    - Child variables members can't have the same name as any of the parent members.
  - Multiple inheritance.
    - The rules of simple inheritance also apply here.
    - If two (or more) parents have methods with the same name, all of them will be inherited, and the methods with the same signature will be overriden in the same order as they are `extends`ed, from left to right.
      - When overloading a method and calling the overloaded method, you can use the `super->method(/*params*/);` which will call the method from the _rightest_ parent which implements it.
      - When overloading a method and calling the overloaded method, you can use the `Class::method(/*params*/);` to refer to a specific class implementation. You can even call all of them.
    - If a parent member has the same name as any of the variables members of any other parent member, they together can't be parents of a child class.
