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
## 5.3 Strings

All textual data is stored as strings, there is no 'char' character like in Java or C

The internal format is always UTF-16, it is not tied to page encoding
```javascript
// With strings we can use single or double quotes, but backticks allow expression embedding
function sum(a, b) {
    return a + b;
}

console.log(`1 + 2 = ${sum(1, 2)}.`);

// The length attribute of strings is a property, not a function - therefor no parantheses
'length'.length // 6

// Character access
let string = 'this is a string';

let char = string[0];
char = string.charAt(0);

// To iterate over characters in a string
for (let char of string) {
    console.log(char);
}

// Such as in Python, strings are immutable (unchangeable)
string[3] = 's'; // error

// Case changing
string.toUpperCase();
string.toLowerCase();

// Substring searching
string = 'New string';
string.indexOf('New'); // 0
string.includes('string'); // True

// Getting substrings
let substring = 'Substring';

substring.slice(0, 5); // subst
substring.slice(2); // bstring
substring.substring(0, 2);
substring.substr(0, 2);
```
## Arrays

Storing ordered collections of data

There are a lot of things we can do with arrays in JavaScript
```javascript
// Declaration
let arr = [];
let arr2 = new Array();

let fruits = ['Orange', 'Apple', 'Pear'];
let orange = fruits[0];

// Arrays can hold multiple types
let types = ['Apple', { name: 'John'}, true, function() { console.log('item')}];

// Access
console.log(types[types.length-1])
console.log(types.at(-1));

// JS arrays act simiarly to dequeues
types.pop();
types.push('Another');

fruits = ['Orange', 'Apple', 'Pear'];
fruits.shift() // Removes orange
fruits.unshift('Orange'); // Back to front

// Ways to loop through array items (don't use 'for in')
let items = [1, 2, 3];

for (let i = 0; i < items.length; i++) {
    console.log(items[i]);
}

for (let item of items) {
    console.log(item);
}

// Because the length is based off the largest index present + 1
let ar = [1, 2, 3];
ar.length = 0; // Clear array

// Multidimensional arrays
let matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

// This will call the function since utlimately arrays are objects
let arr = ["a", "b"];

arr.push(function() {
  alert( this );
});

arr[2]();

// Sum input numbers
let nums = [];
let response = alert('Enter a number');

while (String(response) in '1234567890') {
    nums.push(+response);
    response = alert('Another');
}

let sum = 0;
for (let num in nums) {
    sum += num;
}
```
Iterating, searching, transforming, etc. with arrays
```javascript
// Splice can insert, remove, & replace
let arr = ['I', 'Study', 'JavaScript'];
arr.splice(1, 1); // ['I', 'JavaScript']

let arr = ["I", "study", "JavaScript", "right", "now"];

// starting at 0, remove three and insert these 
arr.splice(0, 3, "Let's", "dance");

// starting at two, remove none, add these
arr.splice(2, 0, 'complex', 'language');

let arr = [1, 2];

// create an array from: arr and [3,4]
alert( arr.concat([3, 4]) ); // 1,2,3,4

// create an array from: arr and [3,4] and [5,6]
alert( arr.concat([3, 4], [5, 6]) ); // 1,2,3,4,5,6

// create an array from: arr and [3,4], then add values 5 and 6
alert( arr.concat([3, 4], 5, 6) ); // 1,2,3,4,5,6

// Here we can do something for each element of an array
arr.forEach(function(item, index, array) {
    // do work
});

// Print each item
['Bilbo', 'Gandalf', 'Sauron'].forEach(console.log());

// Searching
let arr = [1, 0, false];

alert( arr.indexOf(0) ); // 1
alert( arr.indexOf(false) ); // 2
alert( arr.indexOf(null) ); // -1

alert( arr.includes(1) ); // true

// find() function, quite useful
let users = [
    {id: 1, name: "John"},
    {id: 2, name: "Pete"},
    {id: 3, name: "Mary"}
];
  
let user = users.find(item => item.id == 1);
  
alert(user.name); // John

// filter() looks for anything that makes a statement true
let users = [
    {id: 1, name: "John"},
    {id: 2, name: "Pete"},
    {id: 3, name: "Mary"}
];
  
// returns array of the first two users
let someUsers = users.filter(item => item.id < 3);
  
alert(someUsers.length); // 2

// Map allows us to do something to many items
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
alert(lengths); // 5,7,6

// JavaScript also has split(), join(), and reverse() array functions
let arr = [1, 2, 3, 4, 5];
arr.reverse();

let names = 'Bilbo, Gandalf, Nazgul';
let arr = names.split(', ');

let arr = ['Bilbo', 'Gandalf', 'Nazgul'];
let str = arr.join(';'); // glue the array into a string using ;
```
