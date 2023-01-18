### Classes
## Basic syntax
Classes are a way that we can define constructors, class methods, and class variables for an object type
```javascript
class SomeClass {

    age = 19;

    constructor(weight, height, length) {
        this.weight = weight;
        this.height = height;
        this.length = length;
    }

    set weight(value) {
        if (value < 100) {
            console.log('Too little weight');
            return;
        }
        this._weight = value;
    }

    get weight() {
        return this.weight;
    }

    doSomething() {
        return 'This is a class method';
    }
}

let classObject = new SomeClass(150, 22, 25);
classObject.weight = 25;

for (let key in classObject) {
    console.log(classObject[key]);
}

console.log(classObject.doSomething()); // This is a class method
```
## Class inheritance
One class can extend another, adding functionality on top of an existing class (the idea of parent and child classes is invoked here)
