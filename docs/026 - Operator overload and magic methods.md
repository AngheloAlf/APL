# Operator overload and magic methods

To see classes's predefined magic methods and overloded operators, see the `BaseClass` at the standard library chapter.

Operator overloading only works with initalizated objects.

In the following signatures:
- `Self` refers to this class.
- `T` refers to any type.
- `a` and `b` refers to an instance of `Self`.
- `c` referst to a variable that it is not an instance of `Self` (or a subclass of `Self`).

Most of the signature's parameters and return types can be overloaded with other types, but methods with any other number of parameters will not overload any operator.

## Arithmetic operators

### Unary operators

- `Self __unary_plus__();`: Unary plus (`+a`).
- `Self __unary_minus__();`: Unary minus (`-a`).
- `Self __suff_inc__();`: Suffix increment (`a++`).
- `Self __suff_dec__();`: Suffix decrement (`a--`).
- `Self __pre_inc__();`: Prefix increment (`++a`).
- `Self __pre_dec__();`: Prefix decrement (`--a`).

### Binary operators

- `Self __add__(const Self other);`: Addition (`a + b`).
- `Self __sub__(const Self other);`: Subtraction (`a - b`).
- `Self __mul__(const Self other);`: Multiplication (`a * b`).
- `Self __matmul__(const Self other);`: Matrix multiplication (`a @ b`).
- `Self __div__(const Self other);`: Division (`a / b`).
- `Self __floordiv__(const Self other);`: Floor division (`a // b`).
- `Self __mod__(const Self other);`: Modulus (`a % b`).
- `Self __pow__(const Self other);`: Exponentiation (`a ^^ b`).

- `Self __radd__(const T other);`: Addition (`c + a`).
- `Self __rsub__(const T other);`: Subtraction (`c - a`).
- `Self __rmul__(const T other);`: Multiplication (`c * a`).
- `Self __rmatmul__(const T other);`: Matrix multiplication (`c @ a`).
- `Self __rdiv__(const T other);`: Division (`c / a`).
- `Self __rfloordiv__(const T other);`: Floor division (`c // a`).
- `Self __rmod__(const T other);`: Modulus (`c % a`).
- `Self __rpow__(const T other);`: Exponentiation (`c ^^ a`).

## Comparison operators

- `bool __eq__(const Self other);`: Equal (`a == b`).
- `bool __ne__(const Self other);`: Not equal (`a != b`).
- `bool __lt__(const Self other);`: Less than (`a < b`).
- `bool __gt__(const Self other);`: Greater than (`a > b`).
- `bool __le__(const Self other);`: Less or equal than (`a <= b`).
- `bool __ge__(const Self other);`: Greater or equal than (`a >= b`).

Also exists the `__lt_eq_gt__` method which works as a method template for the above 6 methods. This method allows the use of the `<=>` operator.

Using the `__lt_eq_gt__` method, the compiler will generate methods for all the 6 comparison methods, and will replace the `<=>` operator for the corresponding operator (in `__lt__`, the `<=>` operator will be replaced with the `<` operator). The exceptions for this behavior are the ones declared by the programmer.

## Logical operators

- `bool __not__();`: Logical not (`!a`).

## Bitwise operators

- `Self __bit_and__(const Self other);`: Bitwise and (`a & b`).
- `Self __bit_or__(const Self other);`: Bitwise or (`a | b`).
- `Self __bit_not__();`: Bitwise not (`~a`).
- `Self __bit_xor__(const Self other);`: Bitwise xor (`a ^ b`).
- `Self __lshift__(const Self other);`: Arithmetic left shift (`a << b`).
- `Self __rshift__(const Self other);`: Arithmetic right shift (`a >> b`).
- `Self __lo_lshift__(const Self other);`: Logical left shift (`a <<< b`).
- `Self __lo_rshift__(const Self other);`: Logical right shift (`a >>> b`).

- `Self __rbit_and__(const T other);`: Bitwise and (`c & a`).
- `Self __rbit_or__(const T other);`: Bitwise or (`c | a`).
- `Self __rbit_xor__(const T other);`: Bitwise xor (`c ^ a`).
- `Self __rlshift__(const T other);`: Arithmetic left shift (`c << a`).
- `Self __rrshift__(const T other);`: Arithmetic right shift (`c >> a`).
- `Self __rlo_lshift__(const T other);`: Logical left shift (`c <<< a`).
- `Self __rlo_rshift__(const T other);`: Logical right shift (`c >>> a`).

## Assignment operators

- `Self __assignment__(const Self other);`: Assignment (`a = b`).

- `Self __iadd__(const Self other);`: Addition assignment (`a += b`).
- `Self __isub__(const Self other);`: Subtraction assignment (`a -= b`).
- `Self __imul__(const Self other);`: Multiplication assignment (`a *= b`).
- `Self __imatmul__(const Self other);`: Matrix multiplication assignment (`a @= b`).
- `Self __idiv__(const Self other);`: Division assignment (`a /= b`).
- `Self __ifloordiv__(const Self other);`: Floor division assignment (`a //= b`).
- `Self __imod__(const Self other);`: Modulus assignment (`a %= b`).
- `Self __ipow__(const Self other);`: Exponentiation assignment (`a ^^= b`).

- `Self __ibit_and__(const Self other);`: Bitwise and assignment (`a &= b`).
- `Self __ibit_or__(const Self other);`: Bitwise or assignment (`a |= b`).
- `Self __ibit_xor__(const Self other);`: Bitwise xor assignment (`a ^= b`).
- `Self __ilshift__(const Self other);`: Arithmetic left shift assignment (`a <<= b`).
- `Self __irshift__(const Self other);`: Arithmetic right shift assignment (`a >>= b`).
- `Self __ilo_lshift__(const Self other);`: Logical left shift assignment (`a <<<= b`).
- `Self __ilo_rshift__(const Self other);`: Logical right shift assignment (`a >>>= b`).

## Identity operators

- `bool __is__(const Self other);`: Identity equality (`a is b`/`a === b`).
- `bool __is_not__(const Self other);`: Identity inequality (`a is not b`/`a !== b`).

## Membership operators

- `bool __in__(const T other);`: Membership (`a in b`).
- `bool __not_in__(const T other);`: Non-membership (`a not in b`).

## Brackets operator

- `T __getitem__(usize_t index);`: Brackets subscript getter (`a[index]`).
- `T []__getitem__(usize_t start, usize_t stop);`: Brackets subscript getter (`a[start:stop]`).
- `T []__getitem__(usize_t start, usize_t stop, usize_t... more);`: Brackets subscript getter (`a[start:stop:more]`).
- `void __setitem__(T value, usize_t index);`: Brackets subscript setter (`a[index] = value`).
- `void __setitem__(T value, usize_t start, usize_t stop);`: Brackets subscript setter (`a[start:stop] = value`).
- `void __setitem__(T value, usize_t start, usize_t stop, usize_t... more);`: Brackets subscript setter (`a[start:stop:more] = value`).

There may be any number of colon-separated values inside the brackets.

## Function call operator

- `T __call__(/*params*/);`: Function call (`a(/*params*/)`).

## Member access operators

The following method's return types can't be `void`.

None of this methods can be overloaded.

- `T __ptr_access__();`: Member access via pointer (`a->c`).
  - If a user-defined ` __ptr_access__()` is provided, the ` __ptr_access__()` is called again on the value that it returns, recursively, until a ` __ptr_access__()` is reached that returns a plain pointer. After that, built-in semantics are applied to that pointer. 
    - `T *__ptr_access__();`.
- `T __dereference__();`: Dereference (`*a`).
- `T *__address_of__()`: Address of (`&a`).

## Memory allocation operators

- `Self *__new__(usize_t size);`: Dynamic memory allocation (`new Self(/**/)`).
- `Self *__new__(usize_t size, usize_t elements);`: Dynamic array memory allocation (`new[elements] Self(/**/)`).
- `Self *__renew__(Self *ptr, usize_t size, usize_t elements);`: Dynamic array memory reallocation (`renew[elements] a`).
- `void __delete__(Self *ptr);`: Dynamic memory allocation (`delete a`).
- `void __delete__(Self *ptr, usize_t elements);`: Dynamic array memory allocation (`delete[] a`).

## Magic methods

This methods are called by their respective global scope functions. See more in the global scope chapter.

- `std::String __str__();`: Called by the function `str(a)`.
- `std::Bytes __bytes__();`: Called by the function `bytes(a)`.
- `usize_t __len__();`: Called by the function `len(a)`.
- `T __for_each__(usize_t elem)`: Called in `foreach` syntax.

### Basic math

- `T __abs__();`: Called by the function `abs(a)`.
- `T __round__()`: Called by the function `round(a)`.
- `T __round__(usize_t ndigits)`: Called by the function `round(a, ndigits)`.
- `T __trunc__()`: Called by the function `trunc(a)`.
- `T __floor__()`: Called by the function `floor(a)`.
- `T __ceil__()`: Called by the function `ceil(a)`.

### Types conversions

- `int8 __int8__();`: Called by the function `int_8(a)`.
- `int16 __int16__();`: Called by the function `int_16(a)`.
- `int32 __int32__();`: Called by the function `int_32(a)`.
- `int64 __int64__();`: Called by the function `int_64(a)`.
- `uint8 __uint8__();`: Called by the function `uint_8(a)`.
- `uint16 __uint16__();`: Called by the function `uint_16(a)`.
- `uint32 __uint32__();`: Called by the function `uint_32(a)`.
- `uint64 __uint64__();`: Called by the function `uint_64(a)`.
- `float32 __float32__();`: Called by the function `float_32(a)`.
- `float64 __float64__();`: Called by the function `float_64(a)`.
- `bool __bool__();`: Called by the function `boolean(a)`.
- `imaginary32 __imaginary32__();`: Called by the function `imaginary_32(a)`.
- `imaginary64 __imaginary64__();`: Called by the function `imaginary_64(a)`.
- `complex64 __complex64__();`: Called by the function `complex_64(a)`.
- `complex128 __complex128__();`: Called by the function `complex_128(a)`.

- `T __integer__();`: Called by the function `integer(a)`.
- `T __uinteger__();`: Called by the function `uinteger(a)`.
- `T __floating__();`: Called by the function `floating(a)`.
- `T __imaginary__();`: Called by the function `imaginary(a)`.
- `T __complex__();`: Called by the function `complex(a)`.
