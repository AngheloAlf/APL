# Functions

TODO: write about functions.

(something like) regex:

- Declaration: `TYPE NAME((TYPE NAME?(, TYPE NAME?)*)*);`
- Definition: `TYPE NAME((TYPE NAME(, TYPE NAME)*)*){ STATEMENT; }`

- Function pointer type: `TYPE (\*)((TYPE(, TYPE)*)*)`
- Declare variable of type function pointer: `TYPE (\*NAME)((TYPE(, TYPE)*)*)`

## Call by value

When calling a function or method, every argument which has a basic type will be passed by value: This means the called function will get a copy of this value. Modifying this value has no effect to the caller original value.

Pointer to any type are also passed by value, in the sense that the called function will get a copy to the address contained in the pointer. Modifying the address has no effect to the caller original value, but modifying the value pointed by that address will have effects.

## Call by reference

Class types are passed by reference, and may be modified by the called function.

Arrays will are passed by reference (in a C way of thinking).

## Return by value

When returning a basic type or a pointer, it will be returned by value (a copy of it).

## Return by reference

When returning objects (classes) or arrays, a reference to it will be returned. Take in consideration that returning an object or an array will not stop the call to its destructor and the automatic freeing of its memory. You should not return neither an object or an array that has been created in this function.
