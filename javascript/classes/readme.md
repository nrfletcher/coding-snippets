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
```javascript
class Animal {
    constructor(name) {
        this.speed = 0;
        this.name = name;
    }
    run(speed) {
        this.speed = speed;
        console.log(`${this.name} runs at ${this.speed} speed`);
    }
    stop() {
        this.speed = 0;
        console.log(`${this.name} has stopped moving`);
    }
}

let animal = new Animal("Bert");

class Rabbit extends Animal {
    constructor(name, earLength) {
        super();
        this.earLength = earLength;
    }
    hide() {
        console.log(`${this.name} hides`);
    }
    stop() {
        super.stop();
        this.hide();
    }
}

let rabbit = new Rabbit("Harry");
rabbit.run(5);
rabbit.stop();
rabbit.hide();

// Static properties and methods
class User {
    static methodStatic() {
        console.log("This is static");
    }
}

// This is not valid, static methods are not callable on objects
someUser.methodStatic(); // Error: this is not a function

// Private and protected 
class CoffeMachine {
    _waterAmount = 0; // variables with an _ prefacing the name are implied to be values which should be protected

    set waterAmount(value) {
        if (value <0) {
            value = 0;
        }
        this._waterAmount = value;
    }

    get waterAmount() {
        return this._waterAmount;
    }

    constructor(power) {
        this._power = power;
    }

    get power() { // If we want a value to only be initialized and gettable, make no setter method
        return this._power;
    }

}

let coffeeMachine = new CoffeMachine(25);
coffeeMachine.waterAmount = -10;
console.log(coffeeMachine.waterAmount); // 0

// Private 
class RocketShip {

    #fuelAmount = 0;

    get fuelAmount() {
        return this.#fuelAmount;
    }

    set fuelAmount(value) {
        this.#fuelAmount = value < 0 ? 0 : value;
    }

}

let rocketShip = new RocketShip(50);
rocketShip.fuelAmount; // Will raise an error

// Instanceof allows us to check what type of class we are inheriting from 
class Rabbit {}
let rabbit = new Rabbit();

// is it an object of Rabbit class?
alert( rabbit instanceof Rabbit ); // true
```
## Mixins
Mixins are the way of getting around JavaScript's lack of support for multiple inheritance 
```javascript
"use strict";

let sayHiMixin = {
    sayHi() {
        console.log("Hello");
    }
    ,
    sayBye() {
        console.log("Bye!");
    }
};

class User {
    constructor(name) {
        this.name = name;
    }
}

Object.assign(User.prototype, sayHiMixin);
new User("Person").sayHi();

// And we can implement inheritance within mixins
let sayMixin = {
    say(phrase) {
      alert(phrase);
    }
};

let sayHiMixin = {
    __proto__: sayMixin, // (or we could use Object.setPrototypeOf to set the prototype here)

    sayHi() {
      // call parent method
      super.say(`Hello ${this.name}`); // (*)
    },
    sayBye() {
      super.say(`Bye ${this.name}`); // (*)
    }
};

class User {
    constructor(name) {
      this.name = name;
    }
}

// copy the methods
Object.assign(User.prototype, sayHiMixin);

// now User can say hi
new User("Dude").sayHi(); // Hello Dude!
```
