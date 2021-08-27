# Types

## Introduction

PHP supports ten primitive types.

Four scalar types:

-   bool
-   int
-   float (floating-point number, aka double)
-   string

Four compound types:

-   array
-   object
-   callable
-   iterable

And finally two special types:

-   resource
-   NULL

## Booleans

Simplest type. A bool value can be either `true` or `false`.

### Converting to boolean

When converting to bool, the following values are considered `false`:

-   the boolean `false` it self
-   the integer 0 (zero)
-   the floats 0.0 and -0.0 (zero)
-   the empty string, and the string "0"
-   An array with zero elements
-   the special type NULL (including unset variables)
-   SimpleXML objects created from attributeless empty elements, i.e. elements which have neither children nor attributes.

Every other value is considered `true` (including any resource and `NAN`).

## Integers

### Syntax

ints can bei specified in decimal, hexadecimal, octal, or binary notation.

To use octal notation, precede the number with a `0` (zero). To use hexadecimal notation precede the number with `0x`. To use binary notation precede the number with `0b`.

As of PHP 7.4.0, integer literals may contain underscores (_) between digits, for better readability of literals. These underscores are removed by PHP's scanner.

The size of an int is platform-dependent, although a maximum value of about two billion is the usual value (32 bits based). 64-bit platforms usually have a maximum value about 9E18. PHP does not support unsigned ints. int size can be determined using the constant `PHP_INT_SIZE`, maximum value using the constant `PHP_INT_MAX`, and minimum value using the constant `PHP_INT_MIN`.

### Integer overflow

If PHP encounters a number beyond the bounds of the int type, it will interpreted as a float instead. Also, an operation which results in a number beyond the bounds of the int type will return a float instead.

The value of float number can be cast to an int to round it towards zero, or the `round()` function provides finer control over rounding.

### Converting to integer

To explicitly convert a value to int, use either the `(int)` or (`integer)` casts. Howwever, in most cases the cast is not needed, since a value will be automatically converted if an operator, function or control structure requires an int argument. A value can also be converted to int with the `interval()` function.

If a resource is converted to an int, then the result will be the unique resource number assigned to the resource by PHP at runtime.

#### From booleans

`false` will yield `0`, and `true` will yield `1`.

#### From floating point numbers

When converting from float to int, the number will be rounded *towards zero*.

If the float is beyond the boundaries of int (usually +/- 2.15e+9 = 2^31 on 32-bit platforms and +/- 9.22e+18 = 2^63 on 64-bit platforms), the result is undefined, since the float doesn't have enough precision to give an exact int result. No warning, not even a notice will be issued when this happens!

>   **Note**: NaN and Infinity will always be zero when cast to int.

#### From String

If the string is numeric or leading numeric then it wil resolved to the corresponding integer value, otherwise it is converted to zero(0).

#### From NULL

`null`

# Variable Scope

Any variable used inside a function is limited to the local function scope.

## The `globlal` keyword

By declaring a global variable within the function, all references to the variable will refer to the global version. There is no limit to the number of global variables that can be manipulated by a function.

The `$GLOBALS` array is an associative array with the name of the global variable being the key and the contents of that variable being the value of the array element. `$GLOABALS` is a **superglobal**.

## Using `static` variables

A static variable exists only in a local function scope, but it does **not** lose its value when program execution leaves this scope.

## References with `global` and `static` variables

