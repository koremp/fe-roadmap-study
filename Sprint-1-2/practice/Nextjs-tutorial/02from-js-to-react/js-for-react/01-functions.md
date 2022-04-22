# Functions 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions

Functions are one of the fundamental building blocks in JavaScript. A function in JavaScript is similar to a procedure—a set of statements that performs a task or calculates a value, but for a procedure to qualify as a function, it should take some input and return an output where there is some obvious relationship between the input and the output. To use a function, you must define it somewhere in the scope from which you wish to call it.

See also the exhaustive reference chapter about JavaScript functions to get to know the details.

## Defining Functions

A function definition (also called a function declaration, or function statement) consists of the function keyword, followed by:

* The name of the function.
* A list of parameters to the function, enclosed in parentheses and separated by commas.
* The JavaScript statements that define the function, enclosed in curly brackets, `{...}`.

Parameters are essentially passed to functions by value — so if the code within the body of a function assigns a completely new value to a parameter that was passed to the function, `the change is not reflected` globally or in the code which called that function.

## Function expressions

While the function declaration above is syntactically a statement, functions can also be created by a function expression.

### Anonymous function

Such a function can be anonymous; it does not have to have a name. For example, the function square could have been defined as:

```js
const square = function(number) { return number * number }
var x = square(4) // x gets the value 16
```

### Function expression with a name

However, a name can be provided with a function expression. Providing a name allows the function to refer to itself, and also makes it easier to identify the function in a debugger's stack traces:

```js
const factorial = function fac(n) { return n < 2 ? 1 : n * fac(n - 1) }

console.log(factorial(3))
```

### Function as an argument to another function

Function expressions are convenient when passing a function as an argument to another function. The following example shows a map function that should receive a function as first argument and an array as second argument:

```js
function map(f, a) {
  let result = []; // Create a new Array
  let i; // Declare variable
  for (i = 0; i != a.length; i++)
    result[i] = f(a[i]);
  return result;
}
```

In the following code, the function receives a function defined by a function expression and executes it for every element of the array received as a second argument:

```js
function map(f, a) {
  let result = []; // Create a new Array
  let i; // Declare variable
  for (i = 0; i != a.length; i++)
    result[i] = f(a[i]);
  return result;
}
const f = function(x) {
   return x * x * x;
}
let numbers = [0, 1, 2, 5, 10];
let cube = map(f,numbers);
console.log(cube);
```

### Function defined based on a condition

In JavaScript, a function can be defined based on a condition. For example, the following function definition defines myFunc only if num equals 0:

```js
var myFunc;
if (num === 0) {
  myFunc = function(theObject) {
    theObject.make = 'Toyota';
  }
}
```

A `method` is a function that is a property of an object. Read more about objects and methods in [Working with objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects
).

## Calling functions

Defining a function does not execute it. Defining it names the function and specifies what to do when the function is called.

`Calling` the function actually performs the specified actions with the indicated parameters. For example, if you define the function `square`, you could call it as follows:

```js
square(5);
```

The preceding statement calls the function with an argument of 5. The function executes its statements and returns the value 25.

Functions must be in scope when they are called, but the function declaration can be `hoisted` (appear below the call in the code), as in this example:

```js
console.log(square(5));
/* ... */
function square(n) { return n * n }
```

The scope of a function is the function in which it is declared (or the entire program, if it is declared at the top level).

The arguments of a function are not limited to strings and numbers. You can pass whole objects to a function. The `showProps()` function (defined in [Working with objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#objects_and_properties)) is an example of a function that takes an object as an argument.

A function can call itself. For example, here is a function that computes factorials recursively:

```js
function factorial(n) {
  if ((n === 0) || (n === 1))
    return 1;
  else
    return (n * factorial(n - 1));
}
```

There are other ways to call functions. There are often cases where a function needs to be called `dynamically`, or the number of arguments to a function vary, or in which the context of the function call needs to be set to a specific object determined at runtime.

It turns out that functions are themselves objects—and in turn, these objects have methods. (See the Function object.) One of these, the `apply()` method, can be used to achieve this goal.

## Function scope

Variables defined inside a function cannot be accessed from anywhere outside the function, because the variable is defined only in the scope of the function. However, a function can access all variables and functions defined inside the scope in which it is defined.

In other words, `a function defined in the global scope can access all variables defined in the global scope`. A function defined inside another function can also access all variables defined in its parent function, and any other variables to which the parent function has access.

## Scope and the function stack

### Recursion

A function can refer to and call itself. There are three ways for a function to refer to itself:

* The function's name
* `arguments.callee`
* An in-scope variable that refers to the function


However, some algorithms cannot be simple iterative loops. For example, getting all the nodes of a tree structure (such as the DOM) is easier via recursion:


Compared to the function `loop`, each recursive call itself makes many recursive calls here.

It is possible to convert any recursive algorithm to a non-recursive one, but the logic is often much more complex, and doing so requires the use of a stack.

In fact, recursion itself uses a stack: the function stack. The stack-like behavior can be seen in the following example:

## Nested functions and closures

You may `nest a function` within another function. The nested (inner) function is private to its containing (outer) function.

It also forms a `closure`. A closure is an expression (most commonly, a function) that can have `free variables` together with an environment that binds those variables (that "closes" the expression).


To summarize:

* The inner function can be accessed only from statements in the outer function.
* The inner function forms a closure: the inner function can use the arguments and variables of the outer function, while the outer function cannot use the arguments and variables of the inner function.

The following example shows nested functions:

```js
function addSquares(a, b) {
  function square(x) {
    return x * x;
  }
  return square(a) + square(b);
}
a = addSquares(2, 3); // returns 13
b = addSquares(3, 4); // returns 25
c = addSquares(4, 5); // returns 41
```

Since the inner function forms a closure, you can call the outer function and specify arguments for both the outer and inner function:

```js
function outside(x) {
  function inside(y) {
    return x + y;
  }
  return inside;
}
fn_inside = outside(3); // Think of it like: give me a function that adds 3 to whatever you give
                        // it
result = fn_inside(5); // returns 8

result1 = outside(3)(5); // returns 8
```

## Preservation of variables

Notice how `x` is preserved when `inside` is returned. A closure must preserve the arguments and variables in all scopes it references. Since each call provides potentially different arguments, a new closure is created for each call to `outside`. The memory can be freed only when the returned `inside` is no longer accessible.


## Multiply-nested functions

Functions can be multiply-nested. For example:

* A function (A) contains a function (B), which itself contains a function (C).
* Both functions B and C form closures here. So, B can access A, and C can access B.
* In addition, since C can access B which can access A, C can also access A.

Thus, the closures can contain multiple scopes; they recursively contain the scope of the functions containing it. This is called scope chaining. (The reason it is called "chaining" is explained later.)

Consider the following example:

```js
function A(x) {
  function B(y) {
    function C(z) {
      console.log(x + y + z);
    }
    C(3);
  }
  B(2);
}
A(1); // logs 6 (1 + 2 + 3)

```

In this example, C accesses B's y and A's x.

This can be done because:

* B forms a closure including A (i.e., B can access A's arguments and variables).
* C forms a closure including B.
* Because B's closure includes A, C's closure includes A, C can access both B and A's arguments and variables. In other words, C chains the scopes of B and A, in that order.

The reverse, however, is not true. A cannot access C, because A cannot access any argument or variable of B, which C is a variable of. Thus, C remains private to only B.

# Name conflicts

When two arguments or variables in the scopes of a closure have the same name, there is a name conflict. More nested scopes take precedence. So, the inner-most scope takes the highest precedence, while the outer-most scope takes the lowest. This is the scope chain. The first on the chain is the inner-most scope, and the last is the outer-most scope. Consider the following:

```js
function outside() {
  var x = 5;
  function inside(x) {
    return x * 2;
  }
  return inside;
}

outside()(10); // returns 20 instead of 10
```

The name conflict happens at the statement `return x * 2` and is between inside's parameter `x` and `outside`'s variable `x`. The scope chain here is {`inside`, `outside`, global object}. Therefore, `inside`'s `x` takes precedences over `outside`'s `x`, and 20 (`inside`'s `x`) is returned instead of 10 (`outside`'s `x`).