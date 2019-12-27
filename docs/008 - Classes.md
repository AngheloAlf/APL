# Classes

Classes must follow the following rules:

## Syntax

```
class NAME{
    T some_member;
    T *other_member;
    /*more attributes*/

    constructor(/* parameters */){
        /*Do constructor stuff*/
    }

    desctructor(){
        /*Do destructor stuff*/
    }

    void myCoolMethod(){
        /*stuff*/
    }

    /*more methods...*/
}
```

## Objects

An object is a class' instance.

To declare an object, just declare a variable of the type of your class. For example `ClassType myObject;`. Please note, this is just a declaration, it does not initializes the `ClassType` object like C++ would do, it just allocates enough memory for the object to be created.

Using an uninitalizated object must emit a compilation error.

There are two ways two initializate an object:

- Call it (recommended way): 
  - `ClassType myObject = ClassType(/*parameters*/);` or `myObject = ClassType(/*parameters*/);` if it already was declared.
  - This way the desctructor will be automatically called at the end of the scope.
  - You can also call `ClassType(/*parameters*/);` without assigning it, or when passing it to a function call. This way the destructor will be called at the end of the scope too.
- `constructor` it yourself:
  - If you just declared an object, you can manually call the constructor: `myObject.constructor(/*parameters*/);`.
  - The only difference is that is your responsability to call the `desctructor` before leaving the scope. If you don't, there's a high chance you will introduce memory leaks.

Either way, you can't return an object initialized this way out of its original scope. You have to return a heap-allocated pointer to your object if you want it to live outside the scope.

## Use

To use the members of an object you have to use a dot. For example `obj.myCoolMethod();`.

To use the members of an object pointer, you use `->`. For example `ptr->someMember;`.

## Attributes

- The attributes are the variables contained in a class.
- Must be declared before any method declaration or definition.
- Can't be initialized in the declaration, they can only be defined in methods (or external if they are public).
- There are no "static" variables.

## Constructor/Desctructor

- The constructor/destructor are special methods that are called when the object get created/destroyed.
- Each class may declare/define one or more constructors and a desctructor.
- The constructor(s) (if defined) must be named `constructor`, it does not have a return type, and can have any number of parameters.
- The desctructor (if defined) must be named `destructor`, it does not have a return type, and can't have parameters.
- The destructor can't be overloadded.

## Methods members

- Are like the functions of a class.
- Has the same signature declaration as a normal function.
- May refer to attributes by it's name, or by the use of the implicit `this`.
- There are no "static" methods.
- The rules of functions also apply to methods.

## Members

A member refers to a method or an attribute of a class.

## `this` and `self`

You may write and read data to attributes, or call methods using the implicit `this` which exists in every method (including `constructor` and `destructor`).

Besides `this`, also exists `self`<sup>1</sup>, which serves the same function.

You can also use the class' methods and attributes without using `this` or `self` if there is not something with the same name in scope.

Both `this` and `self` are of type "pointer to class".

## Case

The recommended case for the class name is "UpperCamelCase".

The recommended case for the methods names is "LowerCamelCase" (the very first letter is lower case).

## Visibility

There are 3 visibility modifiers:

- `public`: Anything internal or external may use, modify and/or call members tagged public.
- `private`: Only the class itself may use, modify and or call members tagged private. If a class is tagged private, only other classes or functions in the same namespace may use it.
- `protected`: Only the class itself and classes extending this class may use, modify and or call members tagged protected<sup>2</sup>. A class cannot be tagged protected.

When using the visibility modifiers, they must be the first modifier of the member.

The following are the defaults visibilities:

| Class | `public` |
| Method member | `public` |
| Attribute | `protected` |

## Inside an object

An object instance only has the attributes. Methods are not part of it, rather are part of the class.

Looking at this from a C point of view, objects are instances of `struct`s which contains the class attributes. Methods are just functions with an extra parameter.

## When the destructor is called

The destructor is called after the function's return.

## ptrConstructor/ptrDestructor

Besides the special methods `constructor` and `desctructor`, there also exists the special methods `ptrConstructor` and `ptrDestructor`. They are only called when the variable is a pointer to a class.

- There is no need to define them if you don't want to use it.
- `ptrConstructor`:
  - Is called when the user creates a new object using the `new` operator. Specifically, just after the call to `constructor`.
  - Is called when the pointer is passed to a function. Specifically, at the very start of the called function.
  - Is called when the pointer is assigned to other variable. Specifically, just before the assignation.
  - Is called when the pointer is returned by a function. Specifically, just before the return.
- `ptrDestructor`:
  - Is called when the scope containing the pointer ends. Specifically, just after the return.
  - It is **not** called when using the `delete` operator.
- Both take no parameters and have no return type.
- They can not be overloadded.


<sup>1</sup> Yeah, I like Python. Sue me.

<sup>2</sup> see the Inheritance chapter.
