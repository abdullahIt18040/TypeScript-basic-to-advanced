# Type Inference in TypeScript

## Definition
TypeScript can automatically **guess the type** of a variable, parameter, or return value without you explicitly specifying it.  
This is called **type inference**.

---

## Basic Variable Inference
```ts
let message = "Hello TypeScript"; // TypeScript infers type as string
// message = 123; //  Error: number is not assignable to string
Here, message automatically has type string because we assigned a string value.

Number & Boolean Inference
ts

let count = 10;       // inferred as number
let isActive = true;  // inferred as boolean

// count = "ten"; //  Error
// isActive = 1;  //  Error
TypeScript sees the initial value and infers the type automatically.

Function Return Type Inference
ts

function add(a: number, b: number) {
  return a + b; // TypeScript infers return type as number
}

let result = add(5, 10);
// result = "15"; //  Error
You don’t need to explicitly write : number — TypeScript infers it automatically.

Array Type Inference
ts

let numbers = [1, 2, 3, 4]; // inferred as number[]
numbers.push(5);             // valid
// numbers.push("6");        //  Error: string not assignable to number
TypeScript infers numbers as number[] automatically.

Object Type Inference
ts
Copy code
let user = {
  name: "Abdullah",
  age: 25
};

// TypeScript infers type as:
// { name: string; age: number }

user.name = "Mamun";  //  valid
// user.age = "25";    //  Error
When TypeScript Cannot Infer
Sometimes TypeScript cannot guess the type correctly:

ts

let data; // inferred as 'any'
data = 10;
data = "Hello"; //  valid because type is any
To avoid this, it’s better to explicitly specify types:

ts
let data: number;
data = 10;     //  valid
// data = "Hi"; //  Error


Explicit & Union Types in TypeScript
🔹 1️⃣ Explicit Types (স্পষ্টভাবে টাইপ ঘোষণা)
🧠 অর্থ

TypeScript-এ যখন আপনি স্পষ্টভাবে কোনো ভেরিয়েবলের টাইপ বলে দেন, তখন সেটিকে Explicit Type বলা হয়।
অর্থাৎ, TypeScript যেন নিজে থেকে টাইপ অনুমান না করে — আপনি নিজেই বলে দেন কোন টাইপ হবে।

🧩 Syntax
let variableName: type = value;

🧩 Example
let username: string = "Abdullah";
let age: number = 25;
let isDeveloper: boolean = true;

📝 ব্যাখ্যা

username কেবল string হতে পারবে

age কেবল number হতে পারবে

isDeveloper কেবল boolean হতে পারবে

❌ নিচের মতো করলে error হবে:

age = "twenty five"; // ❌ Type error

🔹 2️⃣ Explicit Type with Arrays & Objects
🧩 Array Example
let scores: number[] = [90, 85, 95];
scores.push(88);     // ✅ Valid
// scores.push("80"); // ❌ Error: string not allowed

🧩 Object Example
let user: { name: string; age: number; isAdmin: boolean } = {
  name: "Abdullah",
  age: 25,
  isAdmin: true,
};

🔹 3️⃣ Union Types (একাধিক টাইপের ভেরিয়েবল)
🧠 অর্থ

যখন একটি ভেরিয়েবল একাধিক টাইপের মান নিতে পারে, তখন সেটিকে Union Type বলা হয়।

🧩 Syntax
let variableName: type1 | type2 | type3 = value;

🧩 Example
let id: string | number;
id = 101;       // ✅ allowed (number)
id = "E101";    // ✅ allowed (string)
id = true;      // ❌ not allowed (boolean not included)

🔹 4️⃣ Union Type with Array & Object
🧩 Array Example
let data: (string | number)[] = ["Abdullah", 25, "Mamun", 30];
data.push("Developer"); // ✅ allowed
data.push(100);         // ✅ allowed
// data.push(true);     // ❌ Error

🧩 Object Example
let product: { id: string | number; name: string; price: number } = {
  id: "P101",
  name: "Laptop",
  price: 75000,
};

🔹 5️⃣ Function Example with Union Type
function printId(id: string | number) {
  console.log(`Your ID is: ${id}`);
}

printId(123);       // ✅ number
printId("abc123");  // ✅ string
// printId(true);   // ❌ error

🔹 6️⃣ Union Type + Type Narrowing Example

TypeScript বুঝতে পারে কোন টাইপ বর্তমানে ব্যবহৃত হচ্ছে — একে বলে Type Narrowing।

function getLength(value: string | number): number {
  if (typeof value === "string") {
    return value.length; // string হলে length পাওয়া যাবে
  } else {
    return value; // number হলে সরাসরি মান return
  }
}

console.log(getLength("Hello")); // Output: 5
console.log(getLength(10));      // Output: 10
🔹 1️⃣ Explicit Type with Array

যখন আমরা স্পষ্টভাবে বলে দেই একটি array-এর ভিতরে কোন টাইপের মান থাকবে।

// Only numbers allowed
let scores: number[] = [90, 85, 88];
scores.push(95);     // ✅ valid
// scores.push("99"); // ❌ Error: string not allowed

// Only strings allowed
let names: string[] = ["Abdullah", "Mamun"];
names.push("Hasan");  // ✅ valid
// names.push(25);     // ❌ Error


👉 এখানে TypeScript জানে scores শুধু number[] আর names শুধু string[]।

🔹 2️⃣ Union Type with Array

একটি array-এর মধ্যে একাধিক টাইপের মান রাখতে চাইলে Union Type ব্যবহার করা হয়।

// Can hold both numbers and strings
let mixedArray: (string | number)[] = ["Abdullah", 25, "Mamun", 100];

mixedArray.push("Hello");  // ✅ valid
mixedArray.push(50);       // ✅ valid
// mixedArray.push(true);   // ❌ Error: boolean not allowed


👉 এখানে mixedArray-এর প্রতিটি আইটেম string অথবা number হতে পারে।

🔹 3️⃣ Explicit Type with Object
let user: {
  name: string;
  age: number;
  isVerified: boolean;
} = {
  name: "Abdullah",
  age: 25,
  isVerified: true,
};

// user.age = "twenty"; // ❌ Error: string not allowed


👉 এখানে user অবজেক্টের প্রতিটি প্রপার্টির টাইপ স্পষ্টভাবে ঘোষণা করা হয়েছে।

🔹 4️⃣ Union Type with Object

যখন কোনো প্রপার্টি একাধিক টাইপ নিতে পারে:

let employee: {
  id: string | number;
  name: string;
  salary?: number; // optional
} = {
  id: "E101",
  name: "Mamun",
};

employee.id = 102;  // ✅ valid
employee.id = "E102"; // ✅ valid
// employee.id = true; // ❌ Error
