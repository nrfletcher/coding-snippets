### Data types and ways to interact with them

## 5.1 Primitive methods

JavaScript contains 7 primitive types: string, number, bigint, boolean, symbol, null, and undefined

Objects can: store multiple values and be created using {} braces. Functions are types of objects

Functions can be stored as properties
```javascript
let User = {
    name: 'John';
    sayHi: function() {
        alert('Hello!');
    }
};

User.sayHi();
```
In JavaScript primitives are actually primitive, but object wrappers are used to allow methods to be called on them

This allows easier manipulation of primitives while retaining their light memory footprint

We do not use the Java-esque syntax of stating, variable = new Object() as it will cause unwanted issues
```javascript
// Not recommended
let zero = new Number(0);

// Fine to do
let zero = Number(0);
```
Null and undefined, while primitive, have no wrapper object

## 5.2 Numbers

There are various functions for working with numbers
```javascript
// Both valid (syntactic sugar)
let billion = 1000000000;
let billion = 1_000_000_000;

// Use 'e' as shorthand for lengthy numbers
let billion = 1e9;

// Same for small numbers
let tiny = 1e-6;

// Hexadecimal, binary, octal
let bin = 0b11111111;
let hex = 0xFF;
let oct = 0o377;

// toString(base) allows string representation of a number in a given base
let num = 255;
num.toString(16); // ff
num.toString(2); // 11111111

1234..toString(36); // must use two dots when calling a number directly (non variable)

// JavaScript has plenty of rounding related functions
let someNum = 25.25;
Math.floor(someNum); // round down
Math.ceil(someNum); // round up
Math.round(someNum); // nearest int
Math.trunc(someNum); // gets rid of anything after decimal
+someNum.toFixed(3); // round to certain decimal, returns a string so we have to convert to number

// Reading numbers with extra info
parseInt('100px'); // 100
parseFloat('12.5em'); // 12.5
parseInt('0xff', 16); // Optional radix argument

// Other helpful functions
Math.random();
Math.max(1, 4, 6, -2);
Math.pow(number, power);
```
