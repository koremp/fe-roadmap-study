# Object

The `Object` class represents one of JavaScript's data types. It is used to store various keyed collections and more complex entities. Objects can be created using the `Object()` constructor or the object initializer / literal syntax.

## Description

Nearly all objects in JavaScript are instances of `Object`; a typical object inherits properties (including methods) from `Object.prototyp`e, although these properties may be shadowed (a.k.a. overridden). However, an `Object` may be deliberately created for which this is not true (e.g. by `Object.create(null)`), or it may be altered so that this is no longer true (e.g. with O`bject.setPrototypeOf`).

Changes to the `Object` prototype object are seen by `all` objects through prototype chaining, unless the properties and methods subject to those changes are overridden further along the prototype chain. This provides a very powerful although potentially dangerous mechanism to override or extend object behavior.

The `Object` constructor creates an object wrapper for the given value.

* If the value is `null` or `undefined`, it will create and return an empty object.
* If the value is an object already, it will return the value.
* Otherwise, it will return an object of a Type that corresponds to the given value.

When called in a non-constructor context, Object behaves identically to `new Object()`.

See also the object initializer / literal syntax.

### Deleting a property from an object

There isn't any method in an Object itself to delete its own properties (such as `Map.prototype.delete()`). To do so, one must use the delete operator.

## Constructor

### `Object()`

Creates a new `Object` object. It is a wrapper for the given value.

## Static methods

### `Object.assign()`

Copies the values of all enumerable own properties from one or more source objects to a target object.

### `Object.create()`

Creates a new object with the specified prototype object and properties.

### `Object.defineProperty()`

Adds the named `property` described by a given `descriptor` to an object.

### `Object.defineProperties()`

Adds the named `properties` described by the given `descriptors` to an object.

### `Object.entries()`

Returns an array containing all of the `[key, value]` pairs of a given object's `own` enumerable string properties.

### `Object.freeze()`

Freezes an object. Other code cannot delete or change its properties.

### `Object.fromEntries()`

Returns a new object from an iterable of `[key, value]` pairs. (This is the reverse of `Object.entries`).

```
이렇게 하다간 끝도 없을 것 같음

그냥 Examples로 Jump함
```

## Examples

### Using `Object` given `undefined` and `null` types

The following examples store an empty `Object` object in `o`:

```js
let o = new Object()
let o = new Object(undefined)
let o = new Object(null)
```

### Using `Object` to create `Boolean` objects

The following examples store `Boolean` objects in `o`:

```js
// equivalent to o = new Boolean(true)
let o = new Object(true)
// equivalent to o = new Boolean(false)
let o = new Object(Boolean())
```

### Object prototypes

When altering the behavior of existing `Object.prototype` methods, consider injecting code by wrapping your extension before or after the existing logic. For example, this (untested) code will pre-conditionally execute custom logic before the built-in logic or someone else's extension is executed.

기존 Object.prototype 메서드의 동작을 변경하고자 할 때에는 기존 내용의 앞이나 뒤에 확장할 내용을 래핑하여 코드를 주입하는 것을 고려하세요. 예를 들어, 이 (테스트되지 않은) 코드는 기본 제공 코드 또는 다른 사람의 확장 실행되기 전에 사전 조건부로 사용자 정의 코드를 실행합니다.

When a function is called, the arguments to the call are held in the array-like "variable" arguments. For example, in the call `myFn(a, b, c)`, the arguments within `myFn`'s body will contain 3 array-like elements corresponding to `(a, b, c)`.

함수가 호출되면 호출에 대한 매개변수가 유사배열 "변수" arguments 객체에 보관됩니다. 예를 들어, myFn(a, b, c)를 호출하면 myFn 본문 내의 arguments 객체에는 (a, b, c)에 해당하는 3개의 유사배열요소가 포함됩니다.

When modifying prototypes with hooks, pass `this` and the arguments (the call state) to the current behavior by calling `apply()` on the function. This pattern can be used for any prototype, such as `Node.prototype`, `Function.prototype`, etc.

hook을 통해 프로토타입을 수정하고자 할 때엔 해당 함수에서 apply()를 호출하면서 this와 arguments 객체를 현재 동작에 전달합니다. 이 패턴은 Node.prototype, Function.prototype 등 모든 프로토타입에 적용할 수 있습니다.


```js
var current = Object.prototype.valueOf;

// Since my property "-prop-value" is cross-cutting and isn't always
// on the same prototype chain, I want to modify Object.prototype:
Object.prototype.valueOf = function() {
  if (this.hasOwnProperty('-prop-value')) {
    return this['-prop-value'];
  } else {
    // It doesn't look like one of my objects, so let's fall back on
    // the default behavior by reproducing the current behavior as best we can.
    // The apply behaves like "super" in some other languages.
    // Even though valueOf() doesn't take arguments, some other hook may.
    return current.apply(this, arguments);
  }
}
```

Since JavaScript doesn't exactly have sub-class objects, prototype is a useful workaround to make a "base class" object of certain functions that act as objects. For example:

JavaScript에는 명확한 하위 클래스 객체가 없기 때문에, 프로토타입은 특정 기능의 "기본 클래스" 객체를 만드는 데 유용한 해결 방법입니다. 예를 들어:

```js
var Person = function(name) {
  this.name = name;
  this.canTalk = true;
};

Person.prototype.greet = function() {
  if (this.canTalk) {
    console.log('Hi, I am ' + this.name);
  }
};

var Employee = function(name, title) {
  Person.call(this, name);
  this.title = title;
};

Employee.prototype = Object.create(Person.prototype);
Employee.prototype.constructor = Employee; //If you don't set Object.prototype.constructor to Employee,
                                           //it will take prototype.constructor of Person (parent).
                                           //To avoid that, we set the prototype.constructor to Employee (child).

Employee.prototype.greet = function() {
  if (this.canTalk) {
    console.log('Hi, I am ' + this.name + ', the ' + this.title);
  }
};

var Customer = function(name) {
  Person.call(this, name);
};

Customer.prototype = Object.create(Person.prototype);
Customer.prototype.constructor = Customer; //If you don't set Object.prototype.constructor to Customer,
                                           //it will take prototype.constructor of Person (parent).
                                           //To avoid that, we set the prototype.constructor to Customer (child).

var Mime = function(name) {
  Person.call(this, name);
  this.canTalk = false;
};

Mime.prototype = Object.create(Person.prototype);
Mime.prototype.constructor = Mime; //If you don't set Object.prototype.constructor to Mime,
                                   //it will take prototype.constructor of Person (parent).
                                   //To avoid that, we set the prototype.constructor to Mime (child).

var bob = new Employee('Bob', 'Builder');
var joe = new Customer('Joe');
var rg = new Employee('Red Green', 'Handyman');
var mike = new Customer('Mike');
var mime = new Mime('Mime');

bob.greet();
// Hi, I am Bob, the Builder

joe.greet();
// Hi, I am Joe

rg.greet();
// Hi, I am Red Green, the Handyman

mike.greet();
// Hi, I am Mike

mime.greet();
```

