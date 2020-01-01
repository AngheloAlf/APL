# Operator overload and magic methods

To see classes's predefined magic methods and overloded operators, see the `BaseClass` at the standard library chapter.

Operator overloading only works with initalizated objects.

In the following signatures:
- `Self` refers to the class that is defining this methods.
- `T` refers to any type.
- `a` and `b` refers to an instance of `Self`.
- `c` referst to a variable that it is not an instance of `Self` (or a subclass of `Self`).

## Arithmetic operators

### Unary operators

- `Self __unary_plus__();`: Unary plus (`+a`).
- `Self __unary_minus__();`: Unary minus (`-a`).
- `Self __suff_inc__();`: Suffix increment (`a++`).
- `Self __suff_dec__();`: Suffix decrement (`a--`).
- `Self __pre_inc__();`: Prefix increment (`++a`).
- `Self __pre_dec__();`: Prefix decrement (`--a`).

### Binary operators

- `Self __add__(Self other);`: Addition (`a + b`).
- `Self __sub__(Self other);`: Subtraction (`a - b`).
- `Self __mul__(Self other);`: Multiplication (`a * b`).
- `Self __matmul__(Self other);`: Matrix multiplication (`a @ b`).
- `Self __div__(Self other);`: Division (`a / b`).
- `Self __floordiv__(Self other);`: Floor division (`a // b`).
- `Self __mod__(Self other);`: Modulus (`a % b`).
- `Self __pow__(Self other);`: Exponentiation (`a ^^ b`).

- `Self __radd__(T other);`: Addition (`c + a`).
- `Self __rsub__(T other);`: Subtraction (`c - a`).
- `Self __rmul__(T other);`: Multiplication (`c * a`).
- `Self __rmatmul__(T other);`: Matrix multiplication (`c @ a`).
- `Self __rdiv__(T other);`: Division (`c / a`).
- `Self __rfloordiv__(T other);`: Floor division (`c // a`).
- `Self __rmod__(Self other);`: Modulus (`c % a`).
- `Self __rpow__(T other);`: Exponentiation (`c ^^ a`).

## Comparison operators

- `bool __eq__(Self other);`: Equal (`a == b`).
- `bool __ne__(Self other);`: Not equal (`a != b`).
- `bool __lt__(Self other);`: Less than (`a < b`).
- `bool __gt__(Self other);`: Greater than (`a > b`).
- `bool __le__(Self other);`: Less or equal than (`a <= b`).
- `bool __ge__(Self other);`: Greater or equal than (`a >= b`).

Also exists the `__lt_eq_gt__` method which works as a method template for the above 6 methods. This method allows the use of the `<=>` operator.

Using the `__lt_eq_gt__` method, the compiler will generate methods for all the 6 comparison methods, and will replace the `<=>` operator for the corresponding operator (in `__lt__`, the `<=>` operator will be replaced with the `<` operator). The exceptions for this behavior are the ones declared by the programmer.

## Logical operators

- `bool __not__();`: Logical not (`!a`).

## Bitwise operators

- `Self __bit_and__(Self other);`: Bitwise and (`a & b`).
- `Self __bit_or__(Self other);`: Bitwise or (`a | b`).
- `Self __bit_not__();`: Bitwise not (`~a`).
- `Self __bit_xor__(Self other);`: Bitwise xor (`a ^ b`).
- `Self __lshift__(Self other);`: Arithmetic left shift (`a << b`).
- `Self __rshift__(Self other);`: Arithmetic right shift (`a >> b`).
- `Self __lo_lshift__(Self other);`: Logical left shift (`a <<< b`).
- `Self __lo_rshift__(Self other);`: Logical right shift (`a >>> b`).

- `Self __rbit_and__(T other);`: Bitwise and (`c & a`).
- `Self __rbit_or__(T other);`: Bitwise or (`c | a`).
- `Self __rbit_xor__(T other);`: Bitwise xor (`c ^ a`).
- `Self __rlshift__(T other);`: Arithmetic left shift (`c << a`).
- `Self __rrshift__(T other);`: Arithmetic right shift (`c >> a`).
- `Self __rlo_lshift__(T other);`: Logical left shift (`c <<< a`).
- `Self __rlo_rshift__(T other);`: Logical right shift (`c >>> a`).

## Assignment operators

- `Self __assignment__(Self other);`: Assignment (`a = b`).

- `Self __iadd__(Self other);`: Addition assignment (`a += b`).
- `Self __isub__(Self other);`: Subtraction assignment (`a -= b`).
- `Self __imul__(Self other);`: Multiplication assignment (`a *= b`).
- `Self __imatmul__(Self other);`: Matrix multiplication assignment (`a @= b`).
- `Self __idiv__(Self other);`: Division assignment (`a /= b`).
- `Self __ifloordiv__(Self other);`: Floor division assignment (`a //= b`).
- `Self __imod__(Self other);`: Modulus assignment (`a %= b`).
- `Self __ipow__(Self other);`: Exponentiation assignment (`a ^^= b`).

- `Self __ibit_and__(Self other);`: Bitwise and assignment (`a &= b`).
- `Self __ibit_or__(Self other);`: Bitwise or assignment (`a |= b`).
- `Self __ibit_xor__(Self other);`: Bitwise xor assignment (`a ^= b`).
- `Self __ilshift__(Self other);`: Arithmetic left shift assignment (`a <<= b`).
- `Self __irshift__(Self other);`: Arithmetic right shift assignment (`a >>= b`).
- `Self __ilo_lshift__(Self other);`: Logical left shift assignment (`a <<<= b`).
- `Self __ilo_rshift__(Self other);`: Logical right shift assignment (`a >>>= b`).

## Identity operators

- `bool __is__(Self other);`: Identity equality (`a is b`/`a === b`).
- `bool __is_not__(Self other);`: Identity inequality (`a is not b`/`a !== b`).

## Membership operators

- `bool __in__(Self other);`: Membership (`a in b`/`a === b`).
- `bool __not_in__(Self other);`: Non-membership (`a not in b`/`a !== b`).

## Brackets operator

- `nodestroy T __getitem__(usize_t index);`: Brackets subscript getter (`a[index]`).
- `nodestroy T []__getitem__(usize_t start, usize_t stop);`: Brackets subscript getter (`a[start:stop]`).
- `nodestroy T []__getitem__(usize_t start, usize_t stop, usize_t... more);`: Brackets subscript getter (`a[start:stop:more]`).
- `void __setitem__(T value, usize_t index);`: Brackets subscript setter (`a[index] = value`).
- `void __setitem__(T value, usize_t start, usize_t stop);`: Brackets subscript setter (`a[start:stop] = value`).
- `void __setitem__(T value, usize_t start, usize_t stop, usize_t... more);`: Brackets subscript setter (`a[start:stop:more] = value`).

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

- `nodestroy std::String __str__();`: Called by the function `str(a)`.
- `nodestroy std::Bytes __bytes__();`: Called by the function `bytes(a)`.
- `usize_t __len__();`: Called by the function `len(a)`.
- `nodestroy T __for_each__(usize_t elem)`: Called in `foreach` syntax.
- `Self __abs__();`: Called by the function `abs(a)`.
- `T __round__(self)`: Called by the function `round(a)`.
- `T __round__(self, ndigits)`: Called by the function `round(a, ndigits)`.
- `T __trunc__(self)`: Called by the function `trunc(a)`.
- `T __floor__(self)`: Called by the function `floor(a)`.
- `T __ceil__(self)`: Called by the function `ceil(a)`.

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
