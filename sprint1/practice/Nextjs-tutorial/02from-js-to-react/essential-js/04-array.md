# Array

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array

The `Array` object, as with arrays in other programming languages, enables <u>storing a collection of multiple items under a single variable name</u>, and has members for <u>performing common array operations</u>.

## Description

In JavaScript, arrays aren't <u>primitives</u> but are instead `Array` objects with the following core characteristics:

* JavaScript arrays are resizable and can contain a mix of different data types. (When those characteristics are undesirable, use typed arrays instead.)
* JavaScript arrays are not associative arrays and so, array elements cannot be accessed using strings as indexes, but must be accessed using integers as indexes.
* JavaScript arrays are zero-indexed: the first element of an array is at index `0`, the second is at index `1`, and so on — and the last element is at the value of the array's `length` property minus `1`.
* JavaScript array-copy operations create shallow copies. (All standard built-in copy operations with any JavaScript objects create shallow copies, rather than deep copies).

## Constructor

## Static properties

## Static methods

## Instance properties

## Instance methods

## Examples

This section provides some examples of common array operations in JavaScript.

### Create an array

This example shows three ways to create new array: first using array literal notation, then using the `Array()`constructor, and finally using `String.prototype.split()` to build the array from a string.

```js
// 'fruits' array created using array literal notation.
const fruits = ['Apple', 'Banana'];
console.log(fruits.length);
// 2

// 'fruits' array created using the Array() constructor.
const fruits = new Array('Apple', 'Banana');
console.log(fruits.length);
// 2

// 'fruits' array created using String.prototype.split().
const fruits = 'Apple, Banana'.split(', ');
console.log(fruits.length);
// 2
```

### Create a string from an array

This example uses the `join()` method to create a string from the fruits array.

```js
const fruits = ['Apple', 'Banana'];
const fruitsString = fruits.join(', ');
console.log(fruitsString);
// "Apple, Banana"
```

### Access an array item by its index

This example shows how to access items in the `fruits` array by specifying the index number of their position in the array.

```js
const fruits = ['Apple', 'Banana'];

// The index of an array's first element is always 0.
fruits[0]; // Apple

// The index of an array's second element is always 1.
fruits[1]; // Banana

// The index of an array's last element is always one
// less than the length of the array.
fruits[fruits.length - 1]; // Banana

// Using a index number larger than the array's length
// returns 'undefined'.
fruits[99]; // undefined
```

### Find the index of an item in an array

This example uses the `indexOf()` method to find the position (index) of the string `"Banana" `in the `fruits` array.

```js
const fruits = ['Apple', 'Banana'];
console.log(fruits.indexOf('Banana'));
// 1
```

### Check if an array contains a certain item

This example shows two ways to check if the `fruits` array contains `"Banana"` and `"Cherry"`: first with the `includes()` method, and then with the `indexOf()` method to test for an index value that's not `-1`.


Another Examples That I Know

## Other Examples

### Creating a two-dimensional array

### Using an array to tabulate a set of values

## Notes

`Array` objects cannot use strings as element indexes (as in an associative array) but must use integers. Setting or accessing via non-integers using bracket notation (or dot notation) will not set or retrieve an element from the array list itself, but will set or access a variable associated with that array's object property collection. The array's object properties and list of array elements are separate, and the array's traversal and mutation operations cannot be applied to these named properties.

Array elements are object properties in the same way that `toString` is a property (to be specific, however, `toString()` is a method). Nevertheless, trying to access an element of an array as follows throws a syntax error because the property name is not valid:

```js
console.log(arr.0); // a syntax error
```

There is nothing special about JavaScript arrays and the properties that cause this. JavaScript properties that begin with a digit cannot be referenced with dot notation and must be accessed using bracket notation.

For example, if you had an object with a property named `3d`, it can only be referenced using bracket notation.

```js
const years = [1950, 1960, 1970, 1980, 1990, 2000, 2010];
console.log(years.0);   // a syntax error
console.log(years[0]);  // works properly
```

```js
renderer.3d.setTexture(model, 'character.png');     // a syntax error
renderer['3d'].setTexture(model, 'character.png');  // works properly
```

In the `3d` example, `'3d'` had to be quoted (because it begins with a digit). But it's also possible to quote the array indexes as well (e.g., `years['2']` instead of `years[2]`), although it's not necessary.

The `2` in `years[2]` is coerced into a string by the JavaScript engine through an implicit `toString` conversion. As a result, `'2'` and `'02'` would refer to two different slots on the `years` object, and the following example could be `true`:

```js
console.log(years['2'] != years['02']); // true
```

### Relationship between length and numerical properties

A JavaScript array's `length` property and numerical properties are connected.

Several of the built-in array methods (e.g., `join()`, `slice()`, `indexOf()`, etc.) take into account the value of an array's `length` property when they're called.

Other methods (e.g., `push()`, `splice()`, etc.) also result in updates to an array's `length` property.

```js
const fruits = [];
fruits.push('banana', 'apple', 'peach');
console.log(fruits.length); // 3
```

When setting a property on a JavaScript array when the property is a valid array index and that index is outside the current bounds of the array, the engine will update the array's `length` property accordingly:

```js
fruits[5] = 'mango';
console.log(fruits[5]);            // 'mango'
console.log(Object.keys(fruits));  // ['0', '1', '2', '5']
console.log(fruits.length);        // 6
```

Increasing the length.

### blahblah

### Creating an array using the result of a match

The result of a match between a `RegExp` and a string can create a JavaScript array that has properties and elements which provide information about the match. Such an array is returned by `RegExp.exec()` and `String.match()`.

To help explain these properties and elements, see the following example and then refer to the table below:

```js
// Match one d followed by one or more b's followed by one d
// Remember matched b's and the following d
// Ignore case

const myRe = /d(b+)(d)/i;
const myArray = myRe.exec('cdbBdbsbz');
```

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#creating_an_array_using_the_result_of_a_match