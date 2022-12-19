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
