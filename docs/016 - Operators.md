# Operators

Like in other languages, there are a fuckton<sup>1</sup> <sup>2</sup> of operators, so, prepare yourself.

// How do I even organize all of this? // Markdown needs a comment system.

The following are all the operators availables in this language. Their descriptions describes what will do with any basic types and pointers types (even if it does not make sense), unless stated otherwise.

## Arithmetic operators

### Unary operators

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| `+` | Unary plus | Returns a value with the same type and value of the original | `a = +b;` |
| `-` | Unary minus | Changes the value's sign | `a = -b;` |
| `++` | Suffix increment | Use it, then update it. | `b++;` / `a = b++;` |
| `--` | Suffix decrement | Use it, then update it. | `b--;` / `a = b--;` |
| `++` | Prefix increment | Update it, then use it. | `++b;` / `a = ++b;` |
| `--` | Prefix decrement | Update it, then use it. | `--b;` / `a = --b;` |

### Binary operators

Types promotion rules work here.

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| `+` | Addition | Adds together two values | `a = x + y;` |
| `-` | Subtraction | Subtracts one value from another | `a = x - y;` |
| `*` | Multiplication | Multiplies two values | `a = x * y;` |
| `@` | Matrix multiplication | This operator does not work in basic types | `a = x @ y;` |
| `/` | Division | Divides one value from another | `a = x / y;` |
| `//` | Floor division | Divides one value from another and returns the floor of the result | `a = x // y;` |
| `%` | Modulus | Returns the division remainder | `a = x % y;` |
| `^^` | Exponentiation | Exponentiates one value to the other | `a = x ^^ y;` |

## Comparison operators

| Operator | Name | Example |
| --- | --- | --- |
| `==` | Equal | `a == b;` |
| `!=` | Not equal | `a != b;` |
| `<` | Less than | `a < b;` |
| `>` | Greater than | `a > b;` |
| `<=` | Less or equal than | `a <= b;` |
| `>=` | Greater or equal than | `a >= b;` |

## Logical operators

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| `&&` | Logical and | Returns `true` if both statements evaluates to `true`, `false` otherwise | `a <= c && b != d;` |
| `\|\|` | Logical or | Returns `true` if one of the statements evaluates to `true`, `false` otherwise | `a <= c \|\| b != d;` |
| `!` | Logical not | Returns `true` if the statement evaluates to `false`, `true` otherwise | `!a;` |

## Bitwise operators

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| `&` | Bitwise and |  | `a & b;` |
| `\|` | Bitwise or |  | `a \| b;` |
| `~` | Bitwise not |  | `~a;` |
| `^` | Bitwise xor |  | `a ^ d;` |
| `<<` | Arithmetic left shift |  | `a << b;` |
| `>>` | Arithmetic right shift |  | `a >> b;` |
| `<<<` | Logical left shift |  | `a <<< b;` |
| `>>>` | Logical right shift |  | `a >>> b;` |

~~If any of the elements involved in a shift operator are negative, your PC will format itself and install TempleOS.~~

## Assignment operators

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| `=` | Assignment |  | `a = b;` |
| `+=` | Addition assignment |  | `a + b;` |
| `-=` | Substration assignment |  | `a -= b;` |
| `*=` | Multiplication assignment |  | `a *= d;` |
| `@=` | Matrix multiplication assignment |  | `a @= d;` |
| `/=` | Division assignment |  | `a /= b;` |
| `//=` | Floor division assignment |  | `a //= b;` |
| `%=` | Modulus assignment |  | `a %= b;` |
| `^^=` | Exponentiation assignment |  | `a ^^= b;` |
| `&=` | Bitwise and assignment |  | `a &= b;` |
| `\|=` | Bitwise or assignment |  | `a \|= b;` |
| `^=` | Bitwise xor assignment |  | `a ^= d;` |
| `<<=` | Arithmetic left shift assignment |  | `a <<= b;` |
| `>>=` | Arithmetic right shift assignment |  | `a >>= b;` |
| `<<<=` | Logical left shift assignment |  | `a <<<= b;` |
| `>>>=` | Logical right shift assignment |  | `a >>>= b;` |

## Identity operators

Identity operators are used to compare the objects, not if they are equal, but if they are actually the same object, with the same memory location.

- This operators does not work on basic types or pointers.
- This operators are defined by default in every class.

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| `is` / `===` | Identity equality | Returns `true` if both values are exactly the same (both have the same memory address) | `a is b;` / `a === b;` |
| `is not` / `!==` | Identity inequality | Returns `true` if both values are not the same one (they do not have the same memory address) | `a is not b;` / `a !== b;` |

## Membership operators

Membership operators are used to test if a element is present in an object.

- This operators does not work on basic types or pointers.

| Operator | Name | Description | Example |
| --- | --- | --- | --- |
| `in` | Membership | Returns `true` if the first element is contained in the second one | `a in b;` |
| `not in` | Non-membership | Returns `true` if the first element is _not_ contained in the second one | `a not in b;` |

## Other operators

| Operator | Name | Description | Example | Basic types | Pointers |
| --- | --- | --- | --- | --- | --- |
| `? :` | Conditional operator | If the first element evaluates to `true`, returns the second element, otherwise the third one is returned | `d = a ? b : c;` | [x] | [x] |
| `[]` | Brackets subscript | Retrieves (or assigns) the value from (or to) a collection or array. The value inside the brackets may be multiples values separated by colons. | `a = b[i];` / `a[i] = c;` | [ ] | [x] |
| `()` | Function call | Does a function call. Pointer to functions use this syntax too | `a();` | [ ] | [x] |
| `.` | Member access via object name |  | `a.b;` | [ ] | [ ] |
| `->` | Member access via pointer | Pointers note: only pointer to objects | `a->b;` | [ ] | [x] |
| `*` | Dereference |  | `a = *b;` | [ ] | [x] |
| `&` | Address of |  | `a = &b;` | [x] | [x] |
| `::` | Scope resolution |  | `a::b` | [ ] | [ ] |
| `(type)` | Type cast |  | `b = (int64)a;` | [x] | [x] |
| `new` | Dynamic memory allocation |  | `a = new Thing();` | [ ] | [x] |
| `new[]` | Dynamic array memory allocation |  | `a = new[n] Thing();` | [ ] | [x] |
| `renew[]` | Dynamic array memory reallocation |  | `a = renew[i] a;` | [ ] | [ ] |
| `delete` | Dynamic memory deallocation |  | `delete a;` | [ ] | [x] |
| `delete[]` | Dynamic array memory deallocation |  | `delete[] a;` | [ ] | [x] |
| `throw` | Throw operator |  |  | [ ] | [ ] |
| `instanceof` | Instanceof operator |  | `a instanceof Thing` | [ ] | [ ] |

## Classes

Most of the above operators will not work with user defined classes. But you can overload (almost all of) them to make them work. This topic will be discussed in the Magic methods chapter.

## Type promotion

Type promotion is a implicit type cast, applied when 2 basic types values or variables are operated together. The original variable remains intact. The type promotion's rules are the following:
- The smaller type is casted to the bigger type. For example, adding an `int8` and an `int16`, the first element will be casted to `int16` to perform the addition.
- Equal signedness remains the same.
- If the types has different signedness, the unsigned one will be casted to a signed type. This could lead to data loss.

As a recommendation, you should not operate basic types with machine related types. This could yield unexpected results.

More information of type cast in the Casting chapter.


## Operator precedence

~~Oh boy~~

Operator precendence is a compile-time concept, which allows the compiler know in what order operators are used.

Operators are listed from top to bottom, in descending precedence.

| Precedence | Operator | Name | Associativity |
| --- | --- | --- | --- |
| 1 | `::` | Scope resolution | Left to right |
| --- | --- | --- | --- |
| 2 | `a++` | Suffix increment | Left to right |
| 2 | `a--` | Suffix decrement | Left to right |
| 2 | `a()` | Function call | Left to right |
| 2 | `a[...]` | Brackets subscript | Left to right |
| 2 | `.` | Member access | Left to right |
| 2 | `->` | Member access via pointer | Left to right |
| 2 | `a instanceof b` | Instanceof operator | Left to right |
| --- | --- | --- | --- |
| 3 | `++a` | Prefix increment | Right to left |
| 3 | `--a` | Prefix decrement | Right to left |
| 3 | `+a` | Unary plus | Right to left |
| 3 | `-a` | Unary minus | Right to left |
| 3 | `!a` | Logical not | Right to left |
| 3 | `~a` | Bitwise not | Right to left |
| 3 | `*a` | Dereference | Right to left |
| 3 | `&a` | Address of | Right to left |
| 3 | `(type)a` | Type cast | Right to left |
| 3 | `new` | Dynamic memory allocation | Right to left |
| 3 | `new[]` | Dynamic array memory allocation | Right to left |
| 3 | `renew[]` | Dynamic array memory reallocation | Right to left |
| 3 | `delete` | Dynamic memory deallocation | Right to left |
| 3 | `delete[]` | Dynamic array memory deallocation | Right to left |
| --- | --- | --- | --- |
| 4 | `a ^^ b` | Exponentiation | Right to left |
| --- | --- | --- | --- |
| 5 | `a * b` | Multiplication | Left to right |
| 5 | `a @ b` | Matrix multiplication | Left to right |
| 5 | `a / b` | Division | Left to right |
| 5 | `a // b` | Floor division | Left to right |
| 5 | `a % b` | Modulus | Left to right |
| --- | --- | --- | --- |
| 6 | `a + b` | Addition | Left to right |
| 6 | `a - b` | Substraction | Left to right |
| --- | --- | --- | --- |
| 7 | `a << b` | Arithmetic left shift | Left to right |
| 7 | `a >> b` | Arithmetic right shift | Left to right |
| 7 | `a <<< b` | Logical left shift | Left to right |
| 7 | `a >>> b` | Logical right shift | Left to right |
| --- | --- | --- | --- |
| 8 | `a < b` | Less than | Left to right |
| 8 | `a > b` | Greater than | Left to right |
| 8 | `a <= b` | Less or equal than | Left to right |
| 8 | `a >= b` | Greater or equal than | Left to right |
| 8 | `a is b` / `a === b` | Identity equality | Left to right |
| 8 | `a is not b` / `a !== b` | Identity inequality | Left to right |
| 8 | `a in b` | Membership | Left to right |
| 8 | `a not in b` | Non-membership | Left to right |
| --- | --- | --- | --- |
| 9 | `a == b` | Equal | Left to right |
| 9 | `a != b` | Not equal | Left to right |
| --- | --- | --- | --- |
| 10 | `a & b` | Bitwise and | Left to right |
| --- | --- | --- | --- |
| 11 | `a ^ b` | Bitwise xor | Left to right |
| --- | --- | --- | --- |
| 12 | `a \| b` | Bitwise or | Left to right |
| --- | --- | --- | --- |
| 13 | `a && b` | Logical and | Left to right |
| --- | --- | --- | --- |
| 14 | `a \|\| b` | Logical or | Left to right |
| --- | --- | --- | --- |
| 15 | `a ? b : c` | Conditional operator | Right to left |
| 15 | `throw` | Throw operator | Right to left |
| 15 | `=` | Assignment | Right to left |
| 15 | `+=` | Addition assignment | Right to left |
| 15 | `-=` | Substration assignment | Right to left |
| 15 | `*=` | Multiplication assignment | Right to left |
| 15 | `@=` | Matrix multiplication assignment | Right to left |
| 15 | `/=` | Division assignment | Right to left |
| 15 | `//=` | Floor division assignment | Right to left |
| 15 | `%=` | Modulus assignment | Right to left |
| 15 | `^^=` | Exponentiation assignment | Right to left |
| 15 | `&=` | Bitwise and assignment | Right to left |
| 15 | `\|=` | Bitwise or assignment | Right to left |
| 15 | `^=` | Bitwise xor assignment | Right to left |
| 15 | `<<=` | Arithmetic left shift assignment | Right to left |
| 15 | `>>=` | Arithmetic right shift assignment | Right to left |
| 15 | `<<<=` | Logical left shift assignment | Right to left |
| 15 | `>>>=` | Logical right shift assignment | Right to left |


<sup>1</sup> https://www.urbandictionary.com/define.php?term=fuckton

<sup>2</sup> https://www.urbandictionary.com/define.php?term=Metric%20Fuckton
