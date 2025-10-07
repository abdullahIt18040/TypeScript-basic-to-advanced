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

## What’s Wrong with JavaScript (and Why We Use TypeScript)
 ## No Type Checking

JavaScript হলো dynamically typed language —
মানে variable-এর type ঠিক হয় runtime-এ, compile-time এ নয়।

let name = "Abdullah";
name = 123; // No error! But will cause unexpected bugs later


 Problem:
এই ভুলগুলো শুধু কোড চালানোর সময় ধরা পড়ে — অর্থাৎ runtime errors,
যা debugging কে কঠিন করে তোলে।

## TypeScript Solution:
TypeScript compile করার আগেই বলে দেয় কোথায় ভুল type assign করা হয়েছে।

let name: string = "Abdullah";
name = 123; //  Error at compile-time

## Hard to Maintain Large Projects

 বড় প্রজেক্টে বা টিমে কাজ করার সময়
একটি variable, function, বা object কী ধরনের data নেয় — এটা মনে রাখা কঠিন হয়।

function add(a, b) {
  return a + b;
}

add("5", 10); // 😬 gives '510' instead of 15


## TypeScript Solution:

function add(a: number, b: number): number {
  return a + b;
}


TypeScript enforce করে type — ফলে ভুল ব্যবহার আটকায়।

## No IntelliSense or Auto-Completion Help

 JavaScript-এ editor (যেমন VS Code) কোড autocomplete করতে পারে না
যদি তুমি type না জানো।

## TypeScript Solution:
TypeScript automatically জানে variable ও function-এর type,
তাই IDE তে autocomplete, type hints, ও documentation দেখা যায়।

## Missing Advanced Features (Before ES6)

পুরনো JavaScript version-এ ছিল না:

class, interface

enum, generic

access modifiers (public/private/protected)

## TypeScript Solution:
TypeScript এইসব modern OOP features যুক্ত করেছে,
যা কোডকে করে আরও structure-based এবং reusable।

interface User {
  name: string;
  age: number;
}

##  Runtime Errors Instead of Compile-Time Errors

 JavaScript-এ কোড চালানোর সময়েই (runtime) error ধরা পড়ে,
মানে bug তখনই বোঝা যায় যখন কোড already browser বা server-এ চলছে 😩

TypeScript Solution:
TypeScript compile করার আগেই error detect করে:

Compile-time safety = Fewer runtime crashes 🚀

## Difficult for Big Teams

বড় টিমে অনেক dev একসাথে কাজ করলে,
type না থাকলে কে কী data পাঠাবে, কী return করবে — এটা বোঝা কঠিন হয়।

TypeScript Solution:
Type annotations automatically document করে দেয়।
তাই collaboration সহজ হয়।


## In short:

TypeScript gives you a safer, cleaner, and more powerful version of JavaScript — perfect for professional projects.
https://www.typescriptlang.org/docs/handbook/tsconfig-json.html
