# Keywords

## How we document the examples

- `<types>`: Placeholder for one or more data types (e.g., `int`, `float`, `string`, etc.). It is optional to specify types. Use `void` if no type is needed and `auto` for safe return.
- `types`: Placeholder for one or more data types (e.g., `int`, `float`, `string`, etc.). It is mandatory to specify types.

# Basic for running sections

## `function`

A function is defined by the `function` keyword, followed by the function name, parameters in parentheses, and a block of code enclosed in curly braces. Functions can return values using the `return` statement.

```cosmolang
function <types> functionName(param1, param2) {
    return result;
}<;>
```

> Note: The semicolon (`;`) at the end of the function definition is optional.

## `return`

The `return` keyword is used to exit a function and optionally return a value to the caller.

## `label:`
A label is defined by a name followed by a colon (`:`). It is used as a target for the `goto` statement.

```cosmolang
labelName:
    // Code to execute when jumped to this label
```

Also possible is

```cosmolang
labelName: statement; // A single statement can follow the label
label: name;
    // Code to execute when jumped to this label
```

But what is not possible is chained labels:

```cosmolang
label1: label2: // This is not allowed
    // Code to execute when jumped to label1 or label2
```

> Important: Labels must be unique within the same function scope.
>
> If you have multiple labels one after another, they will be executed in sequence when jumped to the first label.
> If you don't want that, you need to jump back to the function sequentially execution.

> Note: There are two sequential execution types:
> 1. Sequential execution of a function (default behavior).
> 2. Sequential execution of raw code (e.g. labels one after another. Also, comparable to python noob code if you don't use functions).

## `goto` vs `function(...)`

The `goto` keyword is used for unconditional jumps to a labeled statement within the same function, while `function(...)` is used to call another function and can pass parameters and receive return values.

```cosmolang
goto labelName; // Jumps to the label within the same function
functionName(param1, param2); // Calls another function
```

## Examples with all

```cosmolang
function void exampleFunction() {};
label: start;
    // Code to execute
    goto start; // Jumps to the start label

label1:
label2:
    // Code to execute when jumped to label1 it goes to label2

```