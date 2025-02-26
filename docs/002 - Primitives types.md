# Primitives types (and arrays)

## Basic types

One problem that C has is it basic types ensures they are at least in a range of values, and each platform/compiler may use this range or extend it. Here basic types sizes will be fixed.

All types are signed, unless stated otherwise.

When a type overflows or underflows, it should roll over to the other limit

The built-in basic types are:

| Type | Size | Values | Notes |
| --- | --- | --- | --- |
| `int8` | 8 bits | [−128, 127] range  |  |
| `int16` | 16 bits | [−32 768  32 767] range  |  |
| `int32` | 32 bits | [−2 147 483 648, 2 147 483 647] range  |  |
| `int64` | 64 bits | [−9 223 372 036 854 775 808, 9 223 372 036 854 775 807] range  |  |
| `uint8` | 8 bits | [0, 255] range  | unsigned |
| `uint16` | 16 bits | [0, 65 535] range  | unsigned |
| `uint32` | 32 bits | [0, 4 294 967 295] range  | unsigned |
| `uint64` | 64 bits | [0, 18 446 744 073 709 551 615] range  | unsigned |
| `float32` | 32 bits | IEEE 754 | IEEE 754 single-precision binary floating-point |
| `float64` | 64 bits | IEEE 754 | IEEE 754 double-precision binary floating-point |
| `bool` | 8 bits | `false` and `true` |  |
| `void` | none | none | Not a type, but used by functions which don't have return value, and `void *`. |
| `imaginary32` | 32 bits | (IEEE 754)*i | Handles imaginary numbers described by $b * i$ |
| `imaginary64` | 64 bits | (IEEE 754)*i | Handles imaginary numbers described by $b * i$ |
| `complex64` | 64 bits | IEEE 754 + (IEEE 754)*i | Handles complex numbers described by $a + b * i$ |
| `complex128` | 128 bits | IEEE 754 + (IEEE 754)*i | Handles complex numbers described by $a + b * i$ |


### Complex and imaginary types

// TODO

`I`


### Machine related 

- `usize_t`: Refers to memory sizes. It can hold any positive array index. It actual size is the highest size that the host machine can natively handle. Unsigned.
- `uptr_t`: It can hold any pointer. Unsigned.
- `sptr_t`: Intended to be used in `uptr_t` differences. Signed.
- `ptrdiff_t`: For storing pointer differences. Signed.


### Built-in alias types

The language includes some types that are aliases to other basic types, just for convenience.

They can be seen as a typedef of it's original type, but they are keywords.

| Alias type | Refers to | Notes |
| --- | --- | --- |
| `byte` | `int8` |  |
| `ubyte` | `uint8` | unsigned |
| `char` | `int8` |  |
| `uchar` | `uint8` | unsigned |

This types, being just aliases, can be interchanged with their original type or even other alias.

For example, consider the function `uchar someFunction(byte param1, uchar param2[]);`. As first parameter you can pass a variable of type `byte`, `int8` or even `char`, since they are all the same. With the second parameter the same happens, for example variables with types `uchar []`, `uint8 []` and `ubyte []` are valid arguments. This also works for the return type, you can store it in a `ubyte` or a `uint8` variable too.

Even if they are interchangeable, the recommendation is to always match the same types.


## Pointers

A pointer is just an address memory. It is considered unsigned.

### Declaration

Simply `T *var`. This declares `var` is the address where a value of type `T` lives. If this is not defined, `var` has _garbage_, trying to get the value pointed by this _garbage_ is _undefined behavior_.

You can stack pointers. For example `T ***var`.

A small distintion between declaring a pointer here vs C, is there must be at least one space between `T` and `*`.

### Use

To access the value pointed by a pointer, just `*var` or `var[0]`.

You can also tread a pointer as an array if the memory pointed is a multiple of the `sizeof(T)`. Simply use `var[i]` or `*(var + i)` (but the first one is highly encouraged).

### Protection

The language itself provides no runtime protection (like exceptions) when goofing with pointers, it's programmer dutty to not shoot himself (or herself) in the foot.

### Memory allocation

The syntax to allocate heap memory for a pointer is `T *ptr = new T;`. This just declares the pointer and assign memory to it (is like calling C `malloc`).

The syntax to allocate heap memory and define a pointer is:
- For basic types: `int64 *number = new int64(42);`.
- For objecs: `T *ptrToObject = new T(/*parameters*/);`.

Remember to `delete ptr;` when you have finished using it.


## Arrays

Arrays works C arrays, but with extra features... and overhead.

### Declaration

- To declare an array, you should use `T var[]` or `T var[n]`.
- `T var[]`:
  - Declares the variable `var` is an array of elements of type `T`.
  - If it has not been defined, and user tries to use `var`, compiler must refuse to compile.
- `T var[n]`: 
  - `n` must be an integer literal greater than zero, known at compile time. It cannot be a variable. A compiler must refuse to compile if `n` is not an integer literal greater than zero.
  - If values has not been provieded to be stored, this will contain _garbage_, but there will be no issue using it.
- You can stack the brackets:
  - `T var[][][]` will declare a 3d array, but none of its dimensions or its data has been set.
  - `T var[5][3]` will declare a 2d array with setted dimensions. Specifically, it will be an array of 5 elements, and each of it's elements will be an array of 3 `T`.
  - At the first empty bracket, all of the nexts brackets must be empty too.
    - `T var[6][4][]` is valid.
    - `T var[6][][6]` is not valid.
- `T var[n]` lives as long it's scope is alive. It should live in the stack and not in the heap.
- `T var[n]` just provide the corresponding memory to `var`, but does not encorage `var` having a length of `n`. The real type of `var` is `T var[]`. So, the following is valid code:
    ```C
    T a[5];
    T b[15];
    a = b; // no errors, besides the difference of length.
    ```

### Implementation

Like C arrays, the array is pointing to the first element of the array. But, one element before the first one, the length of the array is stored.

If we try to emulate this behavior in C:

```C
void *make_array(size_t len, size_t type_size){
    size_t *arr = malloc(type_size * len + sizeof(size_t));
    arr[0] = len;
    return (void *)&arr[1];
}
```

This way, we can always know the length of the array at runtime.

### Features

- `var.len` returns the length of the array. It's type is `usize_t`.
- Negative index: If index is less than zero, this will return the value starting from the end of the array to the beggining (like Python's lists).
  - For example: `var[-1]` will return the last element of the array. This is the same as `var[var.len-1]`.
  - `var[-var.len]` will return the first element of the array. This is the same as `var[0]`.
- Overflow and underflow index protection: 
  - If `i >= var.len`, then `var[i]` will raise an `IndexOverflowException`.
  - If `i < -var.len`, then `var[i]` will raise an `IndexUnderflowException`.
- User can add and/or override array's behavior. This will be explained in it's own chapter.

### Array life

The array is automatically destroyed when the scope ends, but if the array contains elements that have been allocated with `new` (or a custom allocator), they will probably still exists after the array desctruction. You have to manually `destroy` those elements before the array desctruction.

You can also heap allocate an array using `T[] arr = new T[n];`. Please note that `n` can be a integer literal, or a variable. If you do this, remember to `delete arr;`.

Also, a heap-allocated array may escape the scope where it was allocated, and even returned from the function that created it. In that case, it's caller responsability to deallocate the memory.


## Arrays vs pointers

In C, arrays and pointers are pretty much interchangeable with a few exceptions, but not here... or not just out of the box.

### Array to pointer

This conversion is trivial, just assign the array to a pointer and you are ready to go.

```C
T a[16];
T *b = a; // No problem.
```

### Pointer to array

This is the tricky one.

When using an array, the language and the programmer asumes it can use the `.len` (for example) in any array, but if this array was originally a pointer, it is posible it does not contain this data and/or others needed attributes. So, if a function parameter is an array type, you can't simply pass it a pointer type.

So, what to do?

The standard library contains a function that can insert the data in the pointer, so it can be safelly used as an array. More about it will be discussed it the standard library chapter.

If, for some reason, you don't want to use the standard library, you can use some hacky code like the following: 

```C
T *ptr;
usize_t len = 5;

// Asign memory to ptr, it must be of size 5+1

ptr[0] = len;
T arr[];
arr = &ptr[1]; 
// T arr[] = ptr+1; // also valid.
```

But, this is discoraged because language semantics, features and implementation may change in newer versions.

### What to use?

Depends.

- If you want speed and as small memory usage as you can get, go for pointers. Pointers will always be as featureless as they have always been.
- If you want a bit more of safety and small features and you don't care about the RAM/CPU overhead, arrays is the way.


## Basic strings

Like in C, APL has the notion of strings like a "null-terminated characters array".

A basic string can be declared in two ways:
- `char *aString;`
- `char otherString[];`
Each one has it's own advantages that will be discussed below.

Please note that `int8 *str;` or `int8 str[]` also works since `int8` and `char` are the same.

You can also define string literals with `""`. The `const` qualifier is mandatory when using string literals. For example:
```
const char *strLiteral = "I am an example.";
const char otherLit[] = "This is other example.";
```

Besides basic strings, a `String` class exists, which will be discussed in the strings chapter.
