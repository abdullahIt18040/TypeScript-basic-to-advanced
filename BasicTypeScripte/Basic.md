

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
```

## Explicit Type and Union 
```
let id: string | number;
id = 101;       // allowed (number)
id = "E101";    // allowed (string)
id = true;      // not allowed (boolean not included)
ব্যাখ্যা:
এখানে id হয় string বা number হতে পারে, কিন্তু অন্য কিছু নয়।
```
## Function Example with Union Type
```
function printId(id: string | number) {
  console.log(`Your ID is: ${id}`);
}

printId(123);       // number
printId("abc123");  // string
// printId(true);   // error
```
## Union Type + Type Narrowing Example
```

TypeScript বুঝতে পারে কোন টাইপ বর্তমানে ব্যবহৃত হচ্ছে।

function getLength(value: string | number): number {
  if (typeof value === "string") {
    return value.length; // string হলে length পাওয়া যাবে
  } else {
    return value; // number হলে সরাসরি মান return
  }
}

console.log(getLength("Hello")); // Output: 5
console.log(getLength(10));      // O

যখন আমরা স্পষ্টভাবে বলে দেই একটি array-এর ভিতরে কোন টাইপের মান থাকবে।

// Only numbers allowed
let scores: number[] = [90, 85, 88];
scores.push(95);     // valid
// scores.push("99"); //  Error: string not allowed

// Only strings allowed
let names: string[] = ["Abdullah", "Mamun"];
names.push("Hasan");  //  valid
// names.push(25);     //  Error


এখানে TypeScript জানে scores শুধু number[] আর names শুধু string[]।

## Union Type with Array

একটি array-এর মধ্যে একাধিক টাইপের মান রাখতে চাইলে Union Type ব্যবহার করা হয়।

// Can hold both numbers and strings
let mixedArray: (string | number)[] = ["Abdullah", 25, "Mamun", 100];

mixedArray.push("Hello");  // valid
mixedArray.push(50);       // valid
// mixedArray.push(true);   // Error: boolean not allowed


এখানে mixedArray-এর প্রতিটি আইটেম string অথবা number হতে পারে।
```
## Explicit Type with Object
```

let user: {
  name: string;
  age: number;
  isVerified: boolean;
} = {
  name: "Abdullah",
  age: 25,
  isVerified: true,
};

// user.age = "twenty"; // Error: string not allowed


 এখানে user অবজেক্টের প্রতিটি প্রপার্টির টাইপ স্পষ্টভাবে ঘোষণা করা হয়েছে।

## Union Type with Object
`
যখন কোনো প্রপার্টি একাধিক টাইপ নিতে পারে:

let employee: {
  id: string | number;
  name: string;
  salary?: number; // optional
} = {
  id: "E101",
  name: "Mamun",
};

employee.id = 102;  //  valid
employee.id = "E102"; // valid
// employee.id = true; //  Error
let employee2: Object;

employee2 = {
  id: "E101",
  name: "Mamun",
};

 এখানে id প্রপার্টি হয় string বা number হতে পারে।
salary প্রপার্টি optional, তাই দেওয়া বা না দেওয়া — দুইটাই ঠিক আছে।

```
## any type
`
In TypeScript, the any type is used when you don’t know the type of a value in advance — or when you want to disable type checking for a particular variable.

It tells TypeScript:

“Don’t check the type for this variable — it can hold anything.”

🧠 Definition:
let variableName: any = value;


You can assign any type of value (number, string, object, etc.) later.

TypeScript won’t give errors for type mismatches.

🧩 Example 1: Basic usage
let data: any = 5;
console.log(data);  // 5

data = "Hello";
console.log(data);  // Hello

data = true;
console.log(data);  // true


👉 Here, the variable data can hold number, string, or boolean — no type restriction.

Example 2: With objects
let user: any = { name: "Abdullah" };
console.log(user.name); // Abdullah

user = "Now I’m just a string!";
console.log(user); // Now I’m just a string!


 user can be an object or a string — TypeScript won’t complain.

 Example 3: Function parameter
function printValue(value: any) {
  console.log("Value:", value);
}

printValue(123);
printValue("Hello");
printValue({ id: 1, title: "TypeScript" });


printValue() accepts any type of input.

 Caution

Using any too much defeats the purpose of TypeScript — it removes type safety.
Instead of any, it’s often better to use:

unknown — when you’ll check the type before using it.

Union types (e.g. string | number) — when you know possible types.

Better Alternative Example
function printValue(value: string | number) {
  console.log(value);
}


 This allows only string or number — safer and still flexible.
 `
