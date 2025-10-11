## Module System কী?

 Module System মানে হলো —
আমরা যখন কোডকে ছোট ছোট আলাদা ফাইলে ভাগ করে রাখি,
তারপর দরকারমতো import/export করে ব্যবহার করি।

অর্থাৎ,

Module System আমাদের কোডকে ভাগ করে সহজে ব্যবস্থাপনা (organize) করতে সাহায্য করে।

 কেন Module ব্যবহার করা হয়

কোড পরিষ্কার ও সংগঠিত থাকে
 Reusable (বারবার ব্যবহার করা যায়)
বড় প্রজেক্টে আলাদা আলাদা ফাইল থেকে কাজ করা সহজ হয়
 Dependency স্পষ্টভাবে বোঝা যায়

## Basic Concept

TypeScript (এবং JavaScript)-এ মডিউল তৈরি হয় যখন:

তুমি কোনো ফাইলে export ব্যবহার করো

আরেক ফাইলে import দিয়ে সেটা নিয়ে আসো

##  Example 1: Export and Import
```
file: mathUtils.ts
export function add(a: number, b: number): number {
  return a + b;
}

export const PI = 3.1416;


 এখানে আমরা দুটি জিনিস export করেছি:

add() function

PI constant
```
## file: app.ts
```
import { add, PI } from './mathUtils';

console.log(add(5, 10)); // Output: 15
console.log(PI);         // Output: 3.1416

```
এখানে আমরা আগের ফাইলের function ও constant import করেছি।
## Example 2: Default Export

একটা ফাইলে default export দিলে সেটাকে নাম ছাড়া import করা যায়।
```
 file: logger.ts
export default function logMessage(message: string): void {
  console.log("Log:", message);
}

file: main.ts
import logMessage from './logger';

logMessage("Hello, TypeScript!");


 Output:

Log: Hello, TypeScript!
```
## Module Types

TypeScript বিভিন্ন ধরনের module system সাপোর্ট করে (যেমন):

Module Type	ব্যবহারের জায়গা
CommonJS	Node.js (পুরনো)
ESNext / ESModule	আধুনিক JavaScript/Browser
AMD, UMD	পুরনো browser-based system
```
তুমি তোমার tsconfig.json ফাইলে সেট করতে পারো:

{
  "compilerOptions": {
    "module": "esnext"
  }
}
HTML page  must add 
type  ="module "
example :
  <script type="module" src="./dist/test.js"></script>
```
### What is an Interface in TypeScript?

 An interface is a way to define the shape (structure) of an object in TypeScript.
It tells what properties and methods an object should have — and their types.

Think of it like a blueprint for an object.
```
 Syntax:
interface InterfaceName {
  propertyName: type;
  methodName(): returnType;
}

Example 1: Basic Interface
interface Person {
  name: string;
  age: number;
}

const user: Person = {
  name: "Abdullah",
  age: 24
};


 Here:

Person is an interface.

It defines that any Person object must have:

a name of type string

an age of type number

If you forget any property or use the wrong type, TypeScript will show an error.

 Example 2: Optional property

Use ? to make a property optional.
```
interface Person {
  name: string;
  age?: number; // optional
}
```

const user1: Person = { name: "Abdullah" }; // valid
const user2: Person = { name: "Mamun", age: 25 }; // also valid

 Example 3: Interface with function
interface MathOperation {
  add(a: number, b: number): number;
}

const calculator: MathOperation = {
  add(a, b) {
    return a + b;
  }
};

console.log(calculator.add(5, 10)); // 15

 Example 4: Interface with readonly

You can make a property readonly, meaning it cannot be changed.

interface Car {
  readonly brand: string;
  model: string;
}

const myCar: Car = {
  brand: "Toyota",
  model: "Corolla"
};

myCar.model = "Camry"; //  allowed
// myCar.brand = "Honda";  Error - readonly property

 Example 5: Interface Inheritance

Interfaces can extend other interfaces.

interface Person {
  name: string;
}

interface Employee extends Person {
  salary: number;
}

const emp: Employee = {
  name: "Abdullah",
  salary: 50000
};
