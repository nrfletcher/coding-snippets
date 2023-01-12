## Functions in JavaScript
### Rest Parameters
We can take additional (or many) arguments to a function and put them in an array
```javascript
function sumAllNums(...args) {
    let sum = 0;

    for (let arg of args) {
        sum += arg;
    }

    return sum;
}

console.log(sumAllNums(1, 2, 3, 5));
```
or do something with a few and use the rest as 'rest parameters'
```javascript
function showUserInfo(firstName, lastName, ...residences) {

    console.log("First name: " + firstName + "\nLast name: " + lastName);
    console.log("Residences: ");

    for (let residence of residences) {
        console.log(residence);
    }

    console.log("\n");
}

showUserInfo("Riley", "Fletcher", "Fredericksburg", "Alexandria");
```
We also have an array-like object that we call 'arguments' which contains all args by their index
```javascript
function printArgsByIndex() {
    for (let i = 0; i < arguments.length; i++) {
        console.log(arguments[i]);
    }
}

printArgsByIndex(1, 2, 3, 4, 5);
```
Important note about arguments: because arrow functions () => func() don't have a 'this', they do not have an 'arguments' either

## Spread Syntax
Spread is somewhat the opposite of rest parameters, when using '...arr' in our function call it expands an iterable into a list of args
```javascript
let nums = [2, 4, 6, 8];
console.log(Math.max(...nums)); // 8

let nums2 = [1, 3, 5];
console.log(Math.max(44, ...nums, 19, ...nums2)); // Combining spreads and normal values

let arr = [0, ...nums, 5, ...nums2]; // We can build arrays out of other arrays (merging)

// We can also make array copies
let ar = [1, 2, 3];
let arCopy = [...ar];
console.log(JSON.stringify(ar) == JSON.stringify(arCopy)); // True
console.log(ar == arCopy); // Not true (different references, totally seperate objects)
```
