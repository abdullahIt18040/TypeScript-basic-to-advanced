

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
----------------
