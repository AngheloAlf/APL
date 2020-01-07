# Global scope

The user can't declare nothing in the global scope. But the language provides built-in functions that lives in the global scope.

The following functions are defined in the global scope:

## Basic functions

- `std::String str<T>(const T obj);`: Returns a string representation of the parameter.
  - This function is overloaded with every basic type.
- `std::Bytes bytes<T>(const T obj);`: Returns a bytes representation of the parameter.
  - This function is overloaded with every basic type.
- `usize_t len<T>(const T obj);`: Returns the length of the object.
  - This function is overloaded with arrays types, `usize_t len<T>(T[] obj);`.

### Basic math

The following functions are overloaded to accept any basic type:

- `U abs<T, type U>(const T obj);`: Returns the absolute value of `obj`.
- `U round<T, type U>(const T obj)`: Returns the rounded value of `obj`.
- `U round<T, type U>(const T obj, usize_t ndigits)`: Returns the rounded value of `obj`, rounded with `ndigits`.
- `U trunc<T, type U>(const T obj)`: Returns the truncated value of `obj`.
- `U floor<T, type U>(const T obj)`: Returns the rounded down value of `obj`.
- `U ceil<T, type U>(const T obj)`: Returns the rounded up value of `obj`.
- `U real<T, type U>(const T obj)`: Returns the real part of `obj`.
- `U imag<T, type U>(const T obj)`: Returns the imaginary part of `obj`.

### Types conversions

For basic types, the following functions works as casting.

- `U int_8<T, type U>(const T obj);`.
- `U int_16<T, type U>(const T obj);`.
- `U int_32<T, type U>(const T obj);`.
- `U int_64<T, type U>(const T obj);`.
- `U uint_8<T, type U>(const T obj);`.
- `U uint_16<T, type U>(const T obj);`.
- `U uint_32<T, type U>(const T obj);`.
- `U uint_64<T, type U>(const T obj);`.
- `U float_32<T, type U>(const T obj);`.
- `U float_64<T, type U>(const T obj);`.
- `U boolean<T, type U>(const T obj);`.
- `U imaginary_32<T, type U>(const T obj);`.
- `U imaginary_64<T, type U>(const T obj);`.
- `U complex_64<T, type U>(const T obj);`.
- `U complex_128<T, type U>(const T obj);`.

The following functions does not works with basic types, only with classes that have implemented the respective method.

- `U integer<T, type U>(const T obj);`.
- `U uinteger<T, type U>(const T obj);`.
- `U floating<T, type U>(const T obj);`.
- `U imaginary<T, type U>(const T obj);`.
- `U complex<T, type U>(const T obj);`.

## Non-overridable functions

- `T *addressof<type T>(const T var);`: Receives any variable, returns the pointer to the variable.
- `std::String classname<T>(const T obj);`: Receives an object, returns the class's name.
- `bool isconstr<T>(const T obj)`: Returns if an object has been constructed.
