# Casting

## Syntax

```
int32 example32;
char *example_ptr;
int64 example_arr[];

// set values for each variable

float64 casted_float = (float64)example32;
int32 *casted_ptr = (int32 *)example_arr;
uint64 casted_arr[] = (uint64 [])example_arr;
```

## Numeric types

### Integer types

Casting an integer type
- to another numeric type with equal or greater size has no problems.
- to another integer type with an smaller size will truncate its bytes.
- to an imaginary type will be the same as casting to a floating point.
- to a complex type, the number will be stored in the real part of the complex type, and the imaginary part will be set to zero.
- to a bool type will store `false` if the integer is zero, `true` otherwise.

### Floating point types

Casting a floating point type
- to another floating point type with equal or greater size has no problems.
- to another floating point type with an smaller size will 
- to an integer type will truncate the decimal part.
- to an imaginary type will be the same as casting to another floating point.
- to a complex type, the number will be stored in the real part of the complex type, and the imaginary part will be set to zero.
- to a bool type will store `false` if the integer is zero, `true` otherwise.

### Imaginary type

Casting an imaginary type
- to a complex type, the number will be stored in the imaginary part of the complex type, and the real part will be set to zero.
- to any other numeric type will behave as casting a floating point type to other type.

### Complex type

Casting a complex type
- to an imaginary type, the number stored in the imaginary part of the complex type will be used.
- to a non-imaginary number type, the number stored in the real part of the complex type will be used.
- to any other numeric type will behave as casting a floating point type to other type.

## Bool type

Casting a bool type to any other numeric type will store a `1` if the bool is `true`, `0` if the bool is `false`.

## Pointers

Casting a basic type pointer to any other basic type pointer is allowed, but the bytes pointed by the pointer will not be reinterpreted.

Casting a pointer to an array is allowed, but is your responsability that the original pointer contains the metadata that an array expects.

Casting a pointer to any basic type is allowed, but the type `uptr_t` is recommended.

## Arrays

Casting a basic type array to a to any other basic type array is allowed, but the data stored in each element of the array will not be reinterpreted.

Casting an array to a pointer has no problem.

Casting an array to any basic type is allowed, but the type `uptr_t` is recommended.

## Objects

Casting an object to a super class has no problem.

Casting an object to a sub class is not allowed.

