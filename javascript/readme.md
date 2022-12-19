# JavaScript Snippets

## 4.x Basics of objects

### 4.1 Objects

### 4.6 Optional chaining && short-circuits

Accessing an object property that doesn't exist results in an error
```javascript
let user = {};

console.log(user.address.street); // Error
```
While it may seem appealing to simply use conditional operators
```javascript
let user = {};

console.log(user.address ? user.address.street : undefined);
```
The more efficient and pretty way is to use optional chaining ?.
```javascript
let user = {};

console.log(user?.address?.street); // Returns undefined
```
As well as for undefined objects too
```javascript
let user = null;

console.log(user?.address); // undefined
```
Short-circuiting is the concept that evaluations shut off immedietely when a part fails
```javascript
let user = null;
let x = 0;

user?.sayHi(x++); // user doesn't exist
console.log(x); // this will still be 0
```
We can also use it to check for functions
```javascript
let userAdmin = {
  admin() {
    alert("I am admin");
  }
};

let userGuest = {};

userAdmin.admin?.(); // I am admin
userGuest.admin?.(); // nothing happens
```
### 4.7 Symbol type

Symbols are primitive types for unique identifiers. Symbols are always different
values, even if they have the same name. There are two main uses cases:
1. Hidden object properties
2. Alter some built-in behaviors like Symbol.iterator
```javascript
let user = {
  name: 'John'
};

let id = Symbol("id");
user[id] = 1;
console.log(user[id]); // access data using Symbol as the key

### 4.8 Object to primitive conversions
