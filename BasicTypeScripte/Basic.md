

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
```
In TypeScript, the any type is used when you don’t know the type of a value in advance — or
 when you want to disable type checking for a particular variable.

It tells TypeScript:

“Don’t check the type for this variable — it can hold anything.”

 Definition:
 
let variableName: any = value;


You can assign any type of value (number, string, object, etc.) later.

TypeScript won’t give errors for type mismatches.

 Example 1: Basic usage
 
let data: any = 5;
console.log(data);  // 5

data = "Hello";
console.log(data);  // Hello

data = true;
console.log(data);  // true


 Here, the variable data can hold number, string, or boolean — no type restriction.

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
```
## How to use Functions - TypeScript
 In javascripte when we are not return any thing it default return type is undefine. but in typescripe default return type is void.
undefine means it is value but not define, void is not value .
What is a Function?
```
A function is a reusable block of code that performs a specific task.

In TypeScript, you can define functions with types — so TypeScript knows:

what type of arguments (inputs) the function expects

and what type of value it will return
```
##  Basic Function Syntax
```
function functionName(parameterName: type): returnType {
  // function body
  return value;
}
Example 1: Simple Function
function sayHello(name: string): string {
  return `Hello, ${name}!`;
}

console.log(sayHello("Abdullah"));
```
## Explanation:
```
name: string → The parameter must be a string

: string (after the parentheses) → The function will return a string

return → Sends the result back

Output:

Hello, Abdullah!
```
 ## Function Returning a Number
 ```
function add(a: number, b: number): number {
  return a + b;
}

console.log(add(5, 10)); // 15
```
 Explanation:

Both a and b are numbers

Function returns a number type result (a + b)

 ## Function Returning Nothing (void)
 ```
 
function printMessage(message: string): void {
  console.log("Message:", message);
}

printMessage("TypeScript is powerful!");
```
Explanation:

void means the function does not return any value.

It only performs an action (here: logs a message).

 ## Optional Parameter (?)
 ```
function greet(name: string, age?: number): string {
  if (age) {
    return `Hello ${name}, you are ${age} years old.`;
  } else {
    return `Hello ${name}!`;
  }
}

console.log(greet("Abdullah"));     // Hello Abdullah!
console.log(greet("Abdullah", 25)); // Hello Abdullah, you are 25 years old.

Explanation:

age? → means age is optional (you can pass it or not).
```
## Default Parameter Value
```
function greetUser(name: string = "Guest"): string {
  return `Welcome, ${name}!`;
}

console.log(greetUser());        // Welcome, Guest!
console.log(greetUser("Mamun")); // Welcome, Mamun!

Explanation:

If no value is passed, "Guest" will be used as default.

 Example 6: Arrow Function (Short Form)
const multiply = (x: number, y: number): number => {
  return x * y;
};

console.log(multiply(4, 5)); // 20

 Explanation:

This is the arrow function version of a normal function.

Works the same, but uses =>.
```
## Example 7: Function Type (Stored in Variable)
```
let subtract: (a: number, b: number) => number;

subtract = function (x, y) {
  return x - y;
};

console.log(subtract(10, 4)); // 6

 Explanation:

(a: number, b: number) => number defines a function type.

It says: this variable must store a function that takes two numbers and returns a number.
```
##  Example 8: Passing Object as Parameter
```
type User = {
  name: string;
  age: number;
};

function showUserInfo(user: User) {
  console.log(`Name: ${user.name}, Age: ${user.age}`);
}

showUserInfo({ name: "Abdullah", age: 24 });
```
## What is a Type Alias?

A Type Alias allows you to create a new name for a type.
It’s like giving a nickname to a type — useful when:

You want to reuse the same type in multiple places

Your type is long or complex

You want to make your code more readable
```
 Basic Syntax
type TypeName = type;

```
Then you can use it anywhere you’d normally use a type.

## Example 1: Simple Type Alias
```
type ID = number;

let userId: ID = 101;
let orderId: ID = 202;

console.log(userId, orderId);
```
 Explanation:

type ID = number; → creates an alias ID for number

Now you can use ID instead of number

## Example 2: Object Type Alias
```
type User = {
  name: string;
  age: number;
};

const user1: User = {
  name: "Abdullah",
  age: 24,
};

console.log(user1);
```
 Explanation:

User is a type representing an object with name and age.

Any variable with type User must have these two properties.

## Example 3: Using Type Alias in Function
```
type User = {
  name: string;
  age: number;
};

function printUserInfo(user: User): void {
  console.log(`Name: ${user.name}, Age: ${user.age}`);
}

printUserInfo({ name: "Mamun", age: 25 });
```
Explanation:

Function parameter user must match the User structure.
##  Example 4: Union Types with Alias
```
type Status = "active" | "inactive" | "pending";

let currentStatus: Status = "active";
// currentStatus = "done"; ❌ Error — not part of the union

console.log(currentStatus);
```
 Explanation:

Status can only have one of the three specific string values.

This makes your code safer and clearer.

## Example 5: Function Type Alias
```
type AddFunction = (a: number, b: number) => number;

const add: AddFunction = (x, y) => x + y;

console.log(add(5, 10)); // 15
```
 Explanation:

AddFunction is an alias for a function type.

Any function with the same structure can use it.

## Example 6: Combining Multiple Types
```
type Person = {
  name: string;
};

type Contact = {
  email: string;
  phone: string;
};

// Combine with intersection (&)
type Employee = Person & Contact;

const employee1: Employee = {
  name: "Abdullah",
  email: "abdullah@example.com",
  phone: "0123456789",
};

console.log(employee1);
```
Explanation:

& merges multiple type aliases together.

Employee must have all properties from both Person and Contact.
## NOTE
Function Return type and parameter is the function Signature of a Function.

## Fuction Signature in typescripte
In TypeScript, a function signature describes how a function should look — meaning what parameters it takes and what type of value it returns.
## 1: Function Signature with Implementation
```
function add(a: number, b: number): number {
  return a + b;
}

```
##  Explanation:

a: number → parameter a must be a number

b: number → parameter b must be a number

: number → function must return a number

 ## Example 2: Function Signature without Implementation

You can define just the signature (structure) first, then implement it later:
```
let multiply: (x: number, y: number) => number;

multiply = (x, y) => {
  return x * y;
};
```

Explanation:

(x: number, y: number) => number is the function signature.

It means the function takes two numbers and returns a number.
```

let userDetails12 : (id: string, info: {
    name : string,
    age :number
})=> void;

userDetails12 = (identification:string,info:{
    name:string,
    age: number
})=>{

}
console.log(userDetails12('123',{
   name: "asdasd",
   age: 123
}))
```
## Class কী?

Class হচ্ছে একটি blueprint (নকশা) — যার মাধ্যমে আমরা object তৈরি করি।
এই object-এর মধ্যে data (properties) এবং কাজ (methods) থাকে।

অর্থাৎ,

Class হলো object তৈরির জন্য একটি নকশা (template)।

 ```
Basic Syntax
class ClassName {
  // properties
  property1: type;
  property2: type;

  // constructor
  constructor(param1: type, param2: type) {
    this.property1 = param1;
    this.property2 = param2;
  }

  // method
  methodName() {
    console.log(this.property1);
  }
}

 Example: Student Class
class Student {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  displayInfo(): void {
    console.log(`Name: ${this.name}, Age: ${this.age}`);
  }
}

const student1 = new Student("Mamun", 23);
student1.displayInfo();
```
 Output
Name: Mamun, Age: 23

##  Access Modifiers (public, private, protected)

TypeScript-এ property বা method এর visibility নিয়ন্ত্রণ করা যায়:

Modifier	ব্যাখ্যা
public (default)	সব জায়গা থেকে access করা যায়
private	শুধু class এর ভিতরে access করা যায়
protected	class এবং তার subclass থেকে access করা যায়
class Person {
  public name: string;
  private age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  showAge() {
    console.log(this.age);
  }
}

const p1 = new Person("Mamun", 25);
console.log(p1.name); //  allowed
// console.log(p1.age); // Error (private property)
p1.showAge(); //  works

Inheritance (উত্তরাধিকার)

একটি class অন্য class থেকে বৈশিষ্ট্য (properties & methods) নিতে পারে।

class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Student extends Person {
  id: number;
  constructor(name: string, id: number) {
    super(name); // parent class constructor call
    this.id = id;
  }

  display() {
    console.log(`Name: ${this.name}, ID: ${this.id}`);
  }
}

const s1 = new Student("Abdullah", 101);
s1.display();

