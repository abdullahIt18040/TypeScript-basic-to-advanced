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
``
file: mathUtils.ts
export function add(a: number, b: number): number {
  return a + b;
}

export const PI = 3.1416;


 এখানে আমরা দুটি জিনিস export করেছি:

add() function

PI constant
``
## file: app.ts
``
import { add, PI } from './mathUtils';

console.log(add(5, 10)); // Output: 15
console.log(PI);         // Output: 3.1416

``
এখানে আমরা আগের ফাইলের function ও constant import করেছি।
## Example 2: Default Export

একটা ফাইলে default export দিলে সেটাকে নাম ছাড়া import করা যায়।
`
 file: logger.ts
export default function logMessage(message: string): void {
  console.log("Log:", message);
}

file: main.ts
import logMessage from './logger';

logMessage("Hello, TypeScript!");


 Output:

Log: Hello, TypeScript!
`
## Module Types

TypeScript বিভিন্ন ধরনের module system সাপোর্ট করে (যেমন):

Module Type	ব্যবহারের জায়গা
CommonJS	Node.js (পুরনো)
ESNext / ESModule	আধুনিক JavaScript/Browser
AMD, UMD	পুরনো browser-based system

তুমি তোমার tsconfig.json ফাইলে সেট করতে পারো:

{
  "compilerOptions": {
    "module": "esnext"
  }
}
