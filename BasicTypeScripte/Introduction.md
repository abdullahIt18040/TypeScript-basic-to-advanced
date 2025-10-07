## Why We Use TypeScript Over JavaScript
## Superset of JavaScript

TypeScript হলো JavaScript-এর একটি superset, অর্থাৎ JavaScript-এর সব features TypeScript-এ আছে, সাথে আরও নতুন ক্ষমতাও যোগ করা হয়েছে।
 Every JavaScript code is valid TypeScript code.

// Valid in both JavaScript & TypeScript
console.log("Hello World!");

## Allow Static & Strict Typing

TypeScript কোড লেখার সময় variable-এর টাইপ ঠিক করে দেয়,
ফলে ভুল ধরতে পারি compile-time এ (runtime এ নয়)।

let name: string = "Abdullah";
name = 123; //  Error: number is not assignable to string

## Support Extra Features Like enum, interface, generic, and tuple

এগুলো JavaScript-এ নেই, কিন্তু TypeScript-এ পাওয়া যায় —
এতে কোড structured, readable এবং reusable হয়।

// Enum
enum Role { Admin, User, Guest }

// Interface
interface User {
  name: string;
  age: number;
  role: Role;
}

// Tuple
let person: [string, number] = ["Abdullah", 25];

// Generics
function identity<T>(value: T): T {
  return value;
}

## Support Extra Features Like arrow function, let, and const

TypeScript আধুনিক JavaScript-এর সব নতুন feature (ES6+) support করে।

// Arrow Function
const greet = (name: string): string => `Hello, ${name}!`;

// let and const
let count = 0;
const appName = "TypeScript App";


## In short:

TypeScript gives you a safer, cleaner, and more powerful version of JavaScript — perfect for professional projects.
