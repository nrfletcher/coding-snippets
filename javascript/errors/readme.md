### Error handling in JavaScript
Try..catch syntax allows us to catch possible errors in our code

It only works for runtime errors, as in the code must be runnable 
```javascript
try {
    incorrectstatement;
} catch (err) {
    console.log('Caught it');
}

// For scheduled functions, we must use try catch inside the function itself

setTimeout(function() {
    try {
        noSuchVariableHere;
    } catch (err) {
        console.log('Caught it');
    }
}, 1000);

// We can access the call stack of an error, as well as message and name

try {
    noSuchItem;
} catch (err) {
    console.log(err.stack);
}

// We can omit the error if we choose to

try {
    doSomething;
} catch {
    console.log('No error object');
}

// We can throw errors

let json = '{ "age": 30 }';

try {
    let user = JSON.parse(json);

    if (!user.name) {
        throw new SyntaxError('Incomplete data: no name');
    }

    console.log(user.name);
} catch (err) {
    console.log('JSON error: ' + err.message);
}

// We can rethrow errors

try {
    let user = JSON.parse(json);

    if (!user.name) {
        throw new SyntaxError('Incomplete data: no name');
    }

    blabla();
} catch (err) {

    if (err instanceof SyntaxError) {
        console.log('JSON error: ' + err.message);
    } else {
        throw err; // this is rethrowing
    }
}

// An additional clause to our try ... catch

let num = +prompt('Enter a positive integer number', 35);

let diff, result;

function fib(n) {
    if (n < 0 || Math.trunc(n) != n) {
        throw new Error('Must be positive and an integer');
    }
    return n <= 1 ? n : fib(n - 1) + fib(n - 2);
}

let start = Date.now();

try {
    result = fib(num);
} catch (err) {
    result = 0;
} finally {
    diff = Date.now() - start;
}

console.log(result || 'Error occured');
```
We can also make custom errors
```javascript
class ValidationError extends Error {
  constructor(message) {
    super(message); // (1)
    this.name = "ValidationError"; // (2)
  }
}

function test() {
  throw new ValidationError("Whoops!");
}

try {
  test();
} catch(err) {
  alert(err.message); // Whoops!
  alert(err.name); // ValidationError
  alert(err.stack); // a list of nested calls with line numbers for each
}
```
