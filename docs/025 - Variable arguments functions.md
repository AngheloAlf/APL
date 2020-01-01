# Variable arguments functions (aka varargs)

varargs is a special syntax for functions and methods which allows an undeterminated number of parameters which has the same type to be passed to the function or method. 

To do this, you have to use the ellipsis (`...`) notation.

Example:
```
float64 sumNumbers(float64 value, int64... args){
    foreach(int64 i: args){
        value += i;
    }
    return value;
}

float64 sumNumbers(float64 value, MyCoolNumberContainer... args){
    foreach(MyCoolNumberContainer i: args){
        value += i.getValue();
    }
    return value;
}

/* more code */

int64 some_number = 32;
int32 other_number = 123;

/* more code */

sumNumbers(100, 80, 50); // 230
sumNumbers(560, some_number, some_number, 50, other_number); // 797
sumNumbers(100); // Function not found
```

There can only be one argument declared with the ellipsis notation in a function/method declaration and must be the last parameter declared.

## How to use

A variable declared with the ellipsis notation (`int64... var`) is just a `std::List` behind the scenes (`std::List<int64> var`). So, all the `List`'s methods can be used.

So, the `int64... var` parameter can be passed to other functions/methods that accepts a ellipsis parameter, or a `std::List` parameter.

You can overload and override as normal.

## Internal implementation

The `sumNumbers` function defined above internally translates to:
```
float64 sumNumbers(float64 value, std::List<int64> args){
    foreach(int64 i: args){
        value += i;
    }
    return value;
}
```

And the functions call from the example translates to:
```
// sumNumbers(100, 80, 50);
std::List<int64> __tmp_args = std::List<int64>();
__tmp_args.append(80);
__tmp_args.append(50);
sumNumbers(100, __tmp_args);

// sumNumbers(560, some_number, some_number, 50, other_number);
std::List<int64> __tmp_args = std::List<int64>();
__tmp_args.append(some_number);
__tmp_args.append(some_number);
__tmp_args.append(50);
__tmp_args.append(other_number);
sumNumbers(560, __tmp_args);

// sumNumbers(100);
// Error, function not found.
```

## Templates

You can combine varargs with templates to achieve a function/method which can accept any number of parameters of any type.

Examples:
```
void templateVarargs<T>(T... args);
void example2<basic T>(T some, bool asdf, T... args);
void example42<T implements Cool extends CuteClass>(T... args);
```
