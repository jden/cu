# Cu
Copper - collection utilities

Copper's API aims to be properly extensible using functions, not magic string parameters

## usage

    var Cu = require('cu')

## api

### `Cu.comparator(scalarFn: Function) => Comparator`

Returns a `Comparator: (itemA: Value, itemB: Value) => Boolean` - a function which compares two values for equality. For example, if you want to consider two objects equal if their `_id` properties are stringwise equal, you could create a Comparator with:

    var idComparator = Cu.comparator(function (obj) {
      return obj._id.toString()
    })

### `Cu.contains(colA: Array, item: Value, Comparator?) => Boolean`

Returns `true` if a collection contains a thing

### `Cu.containsAll(colA: Array, ColB: Array, Comparator?) => Boolean`

Returns `true` if a collection is a superset of a second collection

### `Cu.containsAny(colA: Array, colB: Array, Comparator?) => Boolean`

Returns `true` if a collection intersects with a second collection

### `Cu.fork(col: Array, predicate: Predicate, trueFn: (Array) => Value, falseFn: (Array) => Value) => [Value, Value]`


```
type Predicate: (Value) => Boolean
```

Splits by a predicate, then applies them to a function for the true and false subsets. It returns a 2-tuple of the return value of the `trueFn` and `falseFn`, respectively.

### `Cu.forkFlat(col: Array, predicate: Predicate, trueFn: (Array) => Value, falseFn: (Array) => Value) => Flat`

Splits by a predicate, then applies them to a function for the true and false subsets. It returns a 2-tuple of the return value of the `trueFn` and `falseFn`, respectively. Flattens the result by 1 level.


### `Cu.trim(col: Array) => Array`

Returns the compacted Array with all `null` or `undefined` elements removed

### `Cu.indexBy(col: Array, scalarFn: Function) => Object`

Returns a dictionary with keys generated by `scalarFn` and the original object as the value.

### `Cu.to(prop: String) => (Object) => Value`

Returns a scalar function mapping an object to a named property.

### `Cu.flat(Array<Array<T>) => Array<T>`

Flattens an array by one level

### `Cu.cartesianSquare(Array<A>, Array<B>) => Array<Array<A,B>>`

Returns the [Cartesian square (binary Cartesian product)](http://en.wikipedia.org/wiki/Cartesian_product) of two arrays

eg

```js
Cu.cartesianSquare([1,2],[3,4])
// => [
//      [1,3],
//      [1,4],
//      [2,3],
//      [2,4]
//    ]
```

## installation

    $ npm install cu


## running the tests

From package root:

    $ npm install
    $ npm test


## contributors

- jden <jason@denizac.org>


## license

MIT. (c) 2013 AgileMD <opensource@agilemd.com>. See LICENSE.md
