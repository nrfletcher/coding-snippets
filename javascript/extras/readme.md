### Extra JavaScript notes that don't fit any particular section

## Object Getters and Setters
```javascript
let truckObject = {

    propName: "placeholder",
    firstName: null,
    lastName: null,

    get propName() {
        return this.propName;
    },

    set propName(propName) {
        this.propName = propName;
    },

    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    },

    set fullName(value) {
        [this.firstName, this.lastName] = value.split(" ");
    },
};

truckObject.fullName = "Riley Fletcher";
console.log(truckObject.fullName);
```
## Prototypes
The important thing to remember is that when making a prototype, the methods are shared but object state is not - properties remain unique
```javascript
// animal has methods
let animal = {
  walk() {
    if (!this.isSleeping) {
      alert(`I walk`);
    }
  },
  sleep() {
    this.isSleeping = true;
  }
};

let rabbit = {
  name: "White Rabbit",
  __proto__: animal
};

// modifies rabbit.isSleeping
rabbit.sleep();

alert(rabbit.isSleeping); // true
alert(animal.isSleeping); // undefined (no such property in the prototype)

let hamster = {
  stomach: [],

  eat(food) {
    this.stomach.push(food);
  }
};

let speedy = {
  __proto__: hamster,
  stomach: []
};

let lazy = {
  __proto__: hamster,
  stomach: []
};

// Speedy one found the food
speedy.eat("apple");
alert( speedy.stomach ); // apple

// Lazy one's stomach is empty
alert( lazy.stomach ); // <nothing>
```
* In JavaScript, all objects have a hidden [[Prototype]] property that’s either another object or null.
* We can use obj.__proto__ to access it (a historical getter/setter, there are other ways, to be covered soon).
* The object referenced by [[Prototype]] is called a “prototype”.
* If we want to read a property of obj or call a method, and it doesn’t exist, then JavaScript tries to find it in the prototype.
* Write/delete operations act directly on the object, they don’t use the prototype (assuming it’s a data property, not a setter).
* If we call obj.method(), and the method is taken from the prototype, this still references obj. So methods always work with the current object even if they are inherited.
* The for..in loop iterates over both its own and its inherited properties. All other key/value-getting methods only operate on the object itself.

