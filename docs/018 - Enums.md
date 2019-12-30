# Enums

The following will create the type `some_enum`, and the constants `firstEnumarator`, `second`, `fourth`, `small`, `other`, `letsGoBack`, `lastOne`.

```
enum some_enum{
    // The number in the comment states the assigned number to that constant.
    firstEnumarator; // 0
    second; // 1
    fourth; // 2
    small = 0b0111; // 7
    other; // 8
    letsGoBack = 1; // 1
    lastOne; // 2
}

// Then you can use it (almost) like an normal type.

some_enum a_variable = letsGoBack;
some_enum other_example = some_enum::fourth;
```

- The `enum`'s constants are given integer numbers, starting from 0.
- A constants may get it's value assigned manually.
  - This allows any interger literal.
  - This also allow operations that can be calculated in compile-time that involves integer literals and constants (from this enum) that have already been processed.
- If the actual constant did not get assigned manually, the last value is taken, added one and stored in the actual constant.

## Underlying type

The `enum` type generated has a default underlying type of `int64`.

You can use any other basic type for your `enum`s.

The following `enum` has type `uint8` underlying.

```
enum enum_name<uint16>{
    negative;
    positive;
    neutral;
}
```

## Restrictions

- The `enum` type can't be used as a template type.
- An `enum` constant or a "`enum` type" variable can't be assigned to a variable that is not of the type of the `enum` which created it.
  - Unless casted explicitly.
- An "`enum` type" variable can only be assigned an `enum` constanst which is related to that `enum`, or a variable with the same type.
  - Casting does not work here.

## The `bitwise` modifier

It is a common practice to create an `enum` and give each `enum` constant a 1 bit value, so each constant has a different bit assigned to it. So, let's make that part of the language!

```
bitwise enum some_config{
    nothing; // 0
    first_option; // 1
    second_option; // 2
    third_option; // 4
}

some_config selection = third_option | first_option;
```

The `bitwise` modifier allows this behavior in an automatic way. The `bitwise` modifier guaranties that all constants will only have one bit on and there will not be any values repeated.

You can also set your own values to the constants, but ensure that this value has 1 bit on only, and do not interferes with the previously assigned values (the values assigned to the constants behind this one) or a compilation error will be emitted.

As with normal `enum`s, the underlying type for a `bitwise enum` is `int64` too, allowing a max of 65 constants for this `enum`. If you want to use other basic type as the underlying type, you can do it with the same syntax presented above.

```
bitwise enum magic_numbers<uint8>{
    magic;
    number;
    dizzy;
    other_one;
}
```
