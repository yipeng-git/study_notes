# Variable Scope

Any variable used inside a function is limited to the local function scope.

## The `globlal` keyword

By declaring a global variable within the function, all references to the variable will refer to the global version. There is no limit to the number of global variables that can be manipulated by a function.

The `$GLOBALS` array is an associative array with the name of the global variable being the key and the contents of that variable being the value of the array element. `$GLOABALS` is a **superglobal**.

## Using `static` variables

A static variable exists only in a local function scope, but it does **not** lose its value when program execution leaves this scope.

## References with `global` and `static` variables

