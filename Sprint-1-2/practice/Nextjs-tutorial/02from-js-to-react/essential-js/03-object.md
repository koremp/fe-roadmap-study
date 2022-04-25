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

### ``