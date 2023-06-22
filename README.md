## 1. What are function constructors?
In JavaScript, function constructors are a way to create objects with a specific structure and behavior using a constructor function. A constructor function is a regular JavaScript function that is used with the new keyword to create instances of objects.

Here's an example of a constructor function:
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Creating instances using the constructor function
var person1 = new Person('John', 25);
var person2 = new Person('Jane', 30);
## 2. Explain call(), apply() and, bind() methods. Give an example of call(), apply(), bind()
In JavaScript, the call(), apply(), and bind() methods are used to manipulate the execution context and scope of functions. They allow you to explicitly specify the value of this and pass arguments to a function. Here's an explanation of each method:

call(): The call() method is used to invoke a function with a specified this value and individual arguments passed in comma-separated form. The first argument to call() sets the value of this, and subsequent arguments are passed as individual parameters to the function.
Example of using call():
function greet(name) {
  console.log('Hello, ' + name + '! My name is ' + this.name + '.');
}

var person = {
  name: 'John'
};

greet.call(person, 'Alice');
// Output: Hello, Alice! My name is John.
In the example above, call() is used to invoke the greet() function with the person object as the execution context (this value) and passing 'Alice' as an argument.

apply(): The apply() method is similar to call(), but it accepts an array-like object as the second argument, where each element of the array corresponds to an argument passed to the function.
Example of using apply():
function greet(name) {
  console.log('Hello, ' + name + '! My name is ' + this.name + '.');
}

var person = {
  name: 'John'
};

greet.apply(person, ['Alice']);
// Output: Hello, Alice! My name is John.
In this example, apply() is used to invoke the greet() function with the person object as the execution context and passing ['Alice'] as the argument. The argument is an array with a single element.

bind(): The bind() method returns a new function with a specified this value and any initial arguments. Unlike call() and apply(), bind() does not immediately invoke the function. Instead, it creates a new function that can be invoked later.
Example of using bind():
function greet(name) {
  console.log('Hello, ' + name + '! My name is ' + this.name + '.');
}

var person = {
  name: 'John'
};

var greetPerson = greet.bind(person);
greetPerson('Alice');
// Output: Hello, Alice! My name is John.

## 3. What is the purpose of async/await keywords?
he async/await keywords in JavaScript provide a more elegant and synchronous-like way to work with asynchronous code, specifically when dealing with promises. They were introduced in ECMAScript 2017 (ES8) to simplify asynchronous programming and make it easier to write and understand asynchronous code.

Here's a breakdown of the purpose of async/await:

Asynchronous Code Handling: The async keyword is used to define an asynchronous function. It allows the function to use the await keyword inside its body to pause the execution of the function until a promise is resolved. This eliminates the need for explicit handling of callbacks or chaining promises, resulting in code that is more readable and easier to follow.

Awaiting Promises: The await keyword is used within an async function to pause the execution and wait for a promise to be fulfilled or rejected. It can only be used inside an async function. When await is used on a promise, the function is blocked until the promise is resolved. If the promise is fulfilled, the resolved value is returned, allowing you to assign it to a variable. If the promise is rejected, an exception is thrown, which can be caught using a try/catch block.

Error Handling: Using try/catch blocks with async/await allows for clean and centralized error handling. If an error occurs within the await expression, it throws an exception that can be caught using a surrounding try/catch block. This makes it easier to handle and propagate errors in asynchronous code compared to traditional callback-based or promise-chaining approaches.

Sequential Code Flow: With async/await, you can write asynchronous code that looks similar to synchronous code in terms of its structure and flow. It enables you to write asynchronous operations in a sequential manner, making the code easier to reason about and reducing the need for nested callbacks or complex promise chains.
function getUser(userId) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (userId === 1) {
        resolve({ id: 1, username: 'john' });
      } else {
        reject(new Error('User not found'));
      }
    }, 1000);
  });
}

async function displayUserInfo(userId) {
  try {
    const user = await getUser(userId);
    console.log('User:', user);
  } catch (error) {
    console.error('Error:', error.message);
  }
}

displayUserInfo(1);

## 4. Explain prototypes
In JavaScript, prototypes are a mechanism for object inheritance. Every object in JavaScript has an associated prototype, which acts as a blueprint or template for that object. Prototypes allow objects to inherit properties and methods from other objects.

Here are the key points to understand about prototypes:

Prototype Chain: JavaScript follows a prototype-based inheritance model, where objects can inherit properties and methods from their prototypes. Each object has an internal link to its prototype, forming a chain known as the "prototype chain." If a property or method is not found on an object, JavaScript will look up the prototype chain until it finds the property or until it reaches the end of the chain (which is usually the Object.prototype).

prototype Property: Every function in JavaScript has a special prototype property. When a function is used as a constructor with the new keyword, the newly created object's prototype is set to the function's prototype property. This allows instances created by the constructor function to inherit properties and methods defined on the prototype object.

__proto__ Property: Each object (except for some special cases like Object.prototype) has a hidden __proto__ property that points to its prototype. It provides a direct link to the object's prototype in the prototype chain. While the __proto__ property is not standardized, most modern JavaScript environments support it.

Prototypal Inheritance: When accessing a property or method on an object, JavaScript first checks if the property exists on the object itself. If not, it looks up the prototype chain until it finds the property or reaches the end of the chain. This allows objects to inherit and share properties and methods defined on their prototypes.

Constructor Functions and Prototypes: Constructor functions, when invoked with the new keyword, create objects that inherit properties and methods from their prototype. By defining properties and methods on the constructor function's prototype property, all instances created by that constructor function will have access to those properties and methods.
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log('Hello, my name is ' + this.name + '.');
};

var person1 = new Person('John');
var person2 = new Person('Jane');

person1.greet(); // Output: Hello, my name is John.
person2.greet(); // Output: Hello, my name is Jane.
## 5. What is prototype chain
The prototype chain is a mechanism in JavaScript that allows objects to inherit properties and methods from their prototype objects. It forms a hierarchical structure where each object has an internal link to its prototype, creating a chain-like relationship.

When you access a property or method on an object, JavaScript first checks if the property exists on the object itself. If it doesn't, it will continue the search by following the prototype chain. It looks up the prototype of the current object, and if the property is found there, it is returned. If not, it continues up the chain to the prototype's prototype and so on until it finds the property or reaches the end of the chain.

The end of the prototype chain is typically the Object.prototype, which is the ultimate fallback for property lookup. The Object.prototype contains common methods and properties that are available on all JavaScript objects, such as toString() and hasOwnProperty().
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log('Hello, my name is ' + this.name + '.');
};

var person = new Person('John');

console.log(person.name); // Output: John
person.greet(); // Output: Hello, my name is John.
## 6. Give an example of inheritance using function constructor
// Parent Constructor
function Shape(color) {
  this.color = color;
}

// Method defined on the parent's prototype
Shape.prototype.getColor = function() {
  return this.color;
};

// Child Constructor
function Circle(radius, color) {
  // Inherit properties from the parent
  Shape.call(this, color);
  this.radius = radius;
}

// Inherit methods from the parent's prototype
Circle.prototype = Object.create(Shape.prototype);

// Method specific to the child
Circle.prototype.getArea = function() {
  return Math.PI * Math.pow(this.radius, 2);
};

// Create instances of the child object
var myCircle = new Circle(5, 'red');

console.log(myCircle.getColor()); // Output: red
console.log(myCircle.getArea());  // Output: 78.53981633974483
In this example, we have a parent constructor function called Shape, which accepts a color parameter and assigns it to the instance's color property. It also defines a method getColor() on the Shape.prototype.

Then, we have a child constructor function called Circle, which accepts radius and color parameters. To inherit properties from the parent, we use Shape.call(this, color) within the Circle constructor, which invokes the Shape constructor with the appropriate color value.

To inherit methods from the parent's prototype, we use Object.create(Shape.prototype) to create a new object that has the same prototype as Shape.prototype, and assign it to the Circle.prototype. This establishes the inheritance relationship between Circle and Shape.

After that, we define a method specific to the child, getArea(), on the Circle.prototype.