 ES6 — the modern version of JavaScript introduced in 2015, also called ECMAScript 2015. 
It brought a lot of new features that make coding in JavaScript cleaner, easier, and more powerful. Let me break it down clearly:
```
1. Let and Const

Before ES6, we only had var, which had function scope. ES6 introduced:

let → block-scoped variable (can change value)

const → block-scoped constant (cannot be reassigned)

let age = 25;
const name = "Mamun";

2. Arrow Functions

Shorter syntax for writing functions:

// Old way
function sum(a, b) {
  return a + b;
}

// ES6 arrow function
const sum = (a, b) => a + b;


this behaves differently inside arrow functions (lexical this).

3. Template Literals

Use backticks ` to create strings with variables easily:

const name = "Mamun";
const greeting = `Hello, ${name}! Welcome to ES6.`;

4. Default Parameters

Functions can have default values:

function greet(name = "Guest") {
  return `Hello, ${name}`;
}

greet(); // Hello, Guest

5. Destructuring

Easily extract values from arrays or objects:

// Array destructuring
const [a, b] = [10, 20];
console.log(a, b); // 10 20

// Object destructuring
const person = { name: "Mamun", age: 25 };
const { name, age } = person;
console.log(name, age); // Mamun 25

6. Spread and Rest Operators

Spread ... → expand arrays/objects

Rest ... → collect remaining items

// Spread
const arr1 = [1,2];
const arr2 = [...arr1, 3,4]; // [1,2,3,4]

// Rest
function sum(...numbers) {
  return numbers.reduce((a,b) => a+b, 0);
}
sum(1,2,3); // 6

7. Classes

ES6 introduced a cleaner way to write constructor functions:

class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  
  greet() {
    return `Hi, I'm ${this.name}`;
  }
}

const mamun = new Person("Mamun", 25);
console.log(mamun.greet());

8. Modules

Import/export to organize code:

// export.js
export const name = "Mamun";
export function greet() { return "Hello!"; }

// main.js
import { name, greet } from './export.js';

9. Promises

For handling asynchronous operations:

const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("Data received!"), 1000);
  });
};

fetchData().then(data => console.log(data));

10. Enhanced Object Literals

Easier object creation:

const name = "Mamun";
const age = 25;

const person = { name, age }; // same as { name: name, age: age }
```
