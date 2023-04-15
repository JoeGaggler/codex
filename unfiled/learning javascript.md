quick notes while learning javascript

this is one of my [[goals for 2023]]

# language features

## statements
end with semicolon, or you're going to have a bad time

## constants
```js
const foo = 123;
foo = 456; // ERROR

// Cannot forward-declare a const
const bar; // ERROR
```

## `var` and `let`
`let` is like `var` in C#
avoid `var` in your own code

## rest parameters
variable number of parameters are stored an array

must be the last parameter

```js
function foo(bar, ...allMyValues) {
	allMyValues.forEach( id => console.log(id));
}
foo(0, 1, 2, 3); // prints 1 2 3, but not 0
```

## destructuring

### arrays
```js
let foo = [1, 2, 3];
let [x, y, z] = foo; // 1, 2, 3
let [first, ...rest] = foo; // 1, [2, 3]
let [, ...all] = foo; // [2, 3]
let [,, ...all] = foo; // [3]
```

### objects
```js
let foo = { id: 0, name: "Joe" };
let { id, name } = foo; // names match between variables and properties
let { id2, name2 } = foo; // both will be `undefined`
( { id, name } = foo ); // parentheses required to avoid ambiguity with code-blocks
```

## spread
```js
let foo = [1, 2, 3];
let bar = "abc";
function fun(x, y, z) { }
fun(...foo) // spreads array values (1, 2, 3) across the three parameters
fun(...bar) // spreads iterable (a, b, c) across x, y, z
```

## `typeof()`
```
typeof(1) // number
typeof(true) // boolean
typeof('Hello') // string
typeof( function() {} ) // function
typeof( {} ) // object
typeof( null ) // object (surprise!)
typeof( undefined ) // undefined
typeof( NaN ) // number (surprise!)
```

## conversions
```
foo.toString() // anything to a string
Number.parseInt('123') // string to number
Number.parseFloat('123.456') // string to number
Number.parseFloat('123.456ABCDEFG') // string to number, ignoring trailing garbage
```

## loops

### for
```js
for (let i = 0; i < 10; i++) {
	console.log(i)
}
```

Supports `continue` and `break` as expected.

## operators

### Equality

```js
if (x == 0) { } // will perform type conversions (to string)
if (x === 0) { } // triple equals will not type-convert
if (x !== 0) { } // not equals
```

### unary
```js
++foo; // increment
foo++; // post-increment
-foo; // negation
+"123"; // type-convert, since plus-unary works on numbers (surprise!)
```

### logical and relational
```js
if (1 < 2 && 2 < 3) { } // Same as C#
if (!false) { } // unary not
```

### truthy/falsey
```js
let foo = null;
if (foo) { } // not executed
if (foo || 1) { } // executed
```

### other
```js
// Same as C#:
let foo = (1 < 2) ? 'less' : 'greater'; // ternary
foo += 10; // assignment
foo <<= 1; // shift
foo >>>= 1; // shift keep sign
```

## functions
variables have function scope, as expected.

variables with the same name in a nested function are hidden, as expected.

functions capture referenced variables in outer scopes, as expected for closures.

variables declared with `let` are also block scoped, as expected. Reminder to avoid `var` declarations.

default values can be used in ES2015, must be on right-side of parameter list to avoid `undefined`.

## IIFE
immediately invoked function expression
```js
(function() { // anonymous
	console.log('hi');
})()

let result = (function() { // anonymous
	return { id: 0 }
})()

let thing = (function () { // anonymous
    let message = "hi";
    return { wave: (function () { console.log(message); }) };
})();
thing.wave();
```

## this
```js
let foo = {
    id: 13,
    getId: function () { return this.id; }
};
console.log(foo.getId()); // 13
```

`call` and `apply` and `bind` change `this`:
```js
let foo = {
    id: 13,
    getId: function () { return this.id; }
};
console.log(foo.getId()); // 13

let bar = { id: 10 };
console.log(foo.getId.call(bar)); // 10, because it uses foo's function to change `this` to bar

console.log(foo.getId.apply(bar, [1, 2, 3])); // same as call, but supports parameters

let copy = foo.getId.bind(bar);
console.log(copy()) // same as call
```

`bind` makes a copy of a function with a new context for `this`

## arrow functions
```js
let foo = () => 123;
let bar = x => x + 1;
let blah = (x, y) => x + y;
let blue = () => { return "hello"; };
```

arrow functions do NOT have their own `this` value!

## interpolation
```js
let x = 1;
let y = 2;
let z = `${x}, ${y}`; // Note the backticks instead of quotes
```

# modules

## export
```js
const foo = () => {

};

export { foo }; // exports function
export default foo; // exports function as the default
```

## import
```js
import { foo } from './module' // No '.js'
foo();

import bar from './module' // Import the default with a different name
bar();
```

# visual studio code
install `eslint`

# built-in
arrays have `map` :
```js
let a = [1, 2, 3];
let b = a.map((n) => n + 1);
let c = a.map((n, index) => n + index);
```
