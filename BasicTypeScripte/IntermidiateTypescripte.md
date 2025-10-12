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

```
### Interface with Class in TypeScript

 একটি interface বলে দেয়, একটি class-এর মধ্যে কী কী property ও method থাকবে।
যখন কোনো class সেই interface-কে implement করে, তখন class-টিকে সব property ও method বাস্তবায়ন (implement) করতে হয়।
```
Syntax:
interface InterfaceName {
  propertyName: type;
  methodName(): returnType;
}

class ClassName implements InterfaceName {
  // must include all properties & methods defined in the interface
}

Example 1: Simple Interface with Class
interface Person {
  name: string;
  age: number;
  greet(): void;
}

class Student implements Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const student1 = new Student("Abdullah", 24);
student1.greet();

 ব্যাখ্যা:

Person interface বলছে — যে কোনো class যদি এটা implement করে, তার থাকতে হবে:

name (string)

age (number)

greet() (method)

Student class Person interface implement করেছে, তাই তাকে সবগুলো property ও method define করতে হয়েছে।

 Example 2: Multiple Interfaces

একটি class একাধিক interface implement করতে পারে 

interface CanRun {
  run(): void;
}

interface CanEat {
  eat(): void;
}

class Human implements CanRun, CanEat {
  run(): void {
    console.log("Running fast...");
  }

  eat(): void {
    console.log("Eating food...");
  }
}

const human1 = new Human();
human1.run();
human1.eat();

 ব্যাখ্যা:

Human ক্লাসকে CanRun এবং CanEat — দুইটিই implement করতে হয়েছে, তাই দুইটা method-ই define করা হয়েছে।

 Example 3: Interface + readonly property
interface Car {
  readonly brand: string;
  start(): void;
}

class Toyota implements Car {
  readonly brand: string;

  constructor(brand: string) {
    this.brand = brand;
  }

  start(): void {
    console.log(`${this.brand} car started.`);
  }
}

const myCar = new Toyota("Corolla");
myCar.start();
```
## Generics কী?

Generics মানে হলো —
একটা function, class বা interface এমনভাবে লেখা, যাতে সেটা যে কোনো টাইপের ডেটা (যেমন number, string, boolean ইত্যাদি) নিয়েও কাজ করতে পারে।
```
const addId = (obj:object)=>{
let id = Math.floor(Math.random()*100);
return {...obj,id}
}

let user = addId({name:"awe",age: 23});
user.age
but whe we used Generic
const addId = <T>(obj:T)=>{
let id = Math.floor(Math.random()*100);
return {...obj,id}
}

let user = addId({name:"awe",age: 23});
we get only user.id, but
other user property not found ,to slove this problem we used Generic.
const addId = <T>(obj:T)=>{
let id = Math.floor(Math.random()*100);
return {...obj,id}
}
let user = addId({name:"awe",age: 23});
user.age now we we gell all user proberty.
const addId = <T >(obj:T)=>{
let id = Math.floor(Math.random()*100);
return {...obj,id}
}

let user = addId("abdullah");
that is string , but 

if we want to Set type in generic wc can do this.
const addId = <T extends object>(obj:T)=>{
let id = Math.floor(Math.random()*100);
return {...obj,id}
}
now it always received only object.
let user = addId("abdullah"); invalid 
let user2 = addId({name:"awe",age: 23}); valid.

if we want to set Type .
const addId = <T extends {name :string,age:number}>(obj:T)=>{
let id = Math.floor(Math.random()*100);
return {...obj,id}
}
let user = addId({name:"awe",age: 23});

```
## Generic Interface
normaly we used intrerface to struct objecg 
like 
```
interface ApiResponse{
  status:number,
  type:string,
  data:object
}
const myres:ApiResponse ={
  status:200,
  type:'ok',
  data:{
    id:101,
    name:"dasfdsf"
  }
}
but we dont nknow what are the Api response, object or anything .to solve we are used Generic


interface ApiResponse<T>{
  status:number,
  type:string,
  data:T
}
const myres:ApiResponse<Object> ={
  status:200,
  type:'ok',
  data:{
    id:101,
    name:"dasfdsf"
  }
}
if we pass response as string then 

interface ApiResponse<T>{
  status:number,
  type:string,
  data:T
}
const myres:ApiResponse<String> ={
  status:200,
  type:'ok',
  data:"abdullah"
}

: Generic Interface
interface Box<T> {
  content: T;
}

const stringBox: Box<string> = { content: "Hello" };
const numberBox: Box<number> = { content: 123 };
Generic Class
class DataHolder<T> {
  value: T;
  constructor(value: T) {
    this.value = value;
  }
}

const stringData = new DataHolder<string>("TypeScript");
const numberData = new DataHolder<number>(100);

```
Enum in TypeScript (সহজভাবে)
### Enum কী?

enum মানে হলো “Enumeration” বা নাম দেওয়া কনস্ট্যান্ট ভ্যালুগুলোর সেট।
TypeScript-এ enum ব্যবহার করা হয় ফিক্সড মানগুলোর তালিকা তৈরি করতে — যেগুলোর মান বদলাবে না।
 সহজভাবে বললে:

যখন তোমার কোডে একই ধরনের কিছু মান বারবার লাগে (যেমন রঙ, স্ট্যাটাস, দিক, ভূমিকা ইত্যাদি),
তখন Enum ব্যবহার করলে কোড clean, readable এবং কম ভুল হয়।

 Example 1 – Basic Enum
enum Direction {
  Up,
  Down,
  Left,
  Right
}

let move: Direction = Direction.Up;
console.log(move); // Output: 0


 এখানে Direction নামের enum-এ ৪টা মান আছে।
 ডিফল্টভাবে প্রথম মানের সংখ্যা হয় 0, এরপর 1, 2, 3।

 Example 2 – Custom Number Value
enum Direction {
  Up = 10,
  Down = 20,
  Left = 30,
  Right = 40
}

console.log(Direction.Left); // Output: 30


 তুমি চাইলে নিজে থেকেই মান দিতে পারো।

 Example 3 – String Enum
enum Status {
  Success = "SUCCESS",
  Error = "ERROR",
  Pending = "PENDING"
}

let currentStatus: Status = Status.Success;
console.log(currentStatus); // Output: "SUCCESS"


যখন তুমি চাও প্রতিটি মানের নির্দিষ্ট নাম থাকুক (যেমন "SUCCESS"), তখন string enum ব্যবহার করো।

Example 4 – Enum with Condition
enum Role {
  Admin = "ADMIN",
  User = "USER",
  Guest = "GUEST"
}

function checkPermission(role: Role) {
  if (role === Role.Admin) {
    console.log("Full Access");
  } else if (role === Role.User) {
    console.log("Limited Access");
  } else {
    console.log("Guest Access");
  }
}

checkPermission(Role.User); // Output: Limited Access


 এইভাবে enum ব্যবহার করে তুমি সহজে condition handle করতে পারো।

 Example 5 – Heterogeneous Enum (সংখ্যা + স্ট্রিং একসাথে)
enum Mixed {
  No = 0,
  Yes = "YES"
}

console.log(Mixed.No);  // 0
console.log(Mixed.Yes); // "YES"
