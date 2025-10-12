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
```
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
```
### Tuple কী?

 Tuple হলো এক ধরনের array, কিন্তু পার্থক্য হলো —
এর মধ্যে কতগুলো মান থাকবে এবং কোন টাইপের মান থাকবে তা আগে থেকেই নির্ধারিত থাকে।

অর্থাৎ,
Tuple হলো “fixed size + fixed type array” 

 উদাহরণ:
 ```
let user: [string, number];
user = ["Abdullah", 25];


 এখানে প্রথম মান অবশ্যই string,
 দ্বিতীয় মান অবশ্যই number হতে হবে।
অন্য কোনো টাইপ বা বেশি/কম মান দিলে এরর দেবে।

 ভুল উদাহরণ:
user = [25, "Abdullah"]; //  টাইপ উল্টানো যাবে না
user = ["Mamun"];         //  একটি মান কম
user = ["Mamun", 25, "Extra"]; //  একটি মান বেশি

 Tuple Access করা:
console.log(user[0]); // "Abdullah"
console.log(user[1]); // 25

 Example – Tuple in Function Return
function getUser(): [string, number] {
  return ["Abdullah", 25];
}

const [name, age] = getUser();
console.log(name); // Abdullah
console.log(age);  // 25


 এখানে function দুটি মান (string ও number) একসাথে রিটার্ন করছে Tuple আকারে।

 Example – Tuple with Optional Value
let person: [string, number?, string?];
person = ["Mamun"];
person = ["Mamun", 25];
person = ["Mamun", 25, "Bangladesh"];


➡️ ? মানে ঐ মানটা optional (না দিলেও হবে)।

 Example – Tuple with Label (for readability)
let student: [name: string, age: number, passed: boolean];
student = ["Abir", 22, true];

 লেবেল দিলে কোড বুঝতে আরও সহজ হয়।

 Example – Tuple Array

যখন একাধিক tuple রাখতে চাও:

let employees: [string, number][] = [
  ["Abdullah", 101],
  ["Mamun", 102],
  ["Rafi", 103]
];

console.log(employees[1]); // ["Mamun", 102]

 কেন Tuple ব্যবহার করবে?
সুবিধা	ব্যাখ্যা
 Fixed size	নির্দিষ্ট সংখ্যক মান থাকবে Fixed type	প্রত্যেক মানের টাইপ আগেই নির্ধারিত
 Readable	ডেটা গঠন সহজে বোঝা যায়
 Function return-এ সুবিধাজনক	একাধিক মান রিটার্ন করা সহজ
 সহজভাবে মনে রাখো:
let data: [string, number, boolean] = ["Hello", 123, true];


এটি হলো এমন এক array যেখানে:
 প্রথম মান string
 দ্বিতীয় মান number
 তৃতীয় মান boolean
```
Intersection Type কী?

## Intersection Type (&) মানে হলো —
দুই বা তার বেশি টাইপকে একত্র করে একটি টাইপ তৈরি করা।

অর্থাৎ,
যদি তুমি চাও কোনো ভেরিয়েবলে একাধিক টাইপের প্রোপার্টি একসাথে থাকুক — তখন Intersection Type ব্যবহার করা হয়।
```
Basic Example
type Person = {
  name: string;
  age: number;
};

type Employee = {
  employeeId: number;
  department: string;
};

type Staff = Person & Employee;

```
এখন Staff টাইপে Person + Employee — দুইটার প্রোপার্টিই থাকবে ✅
```
 Example: Using the Combined Type
const staff1: Staff = {
  name: "Abdullah",
  age: 25,
  employeeId: 101,
  department: "IT"
};


এখানে তুমি দেখতে পাচ্ছো, staff1-এর মধ্যে Person ও Employee দুইটাই একসাথে কাজ করছে।

 আরেকটা Example — Function Parameter এ
type Student = { name: string };
type Marks = { score: number };

function showInfo(data: Student & Marks) {
  console.log(`${data.name} scored ${data.score}`);
}

showInfo({ name: "Mamun", score: 95 });

 এখানে data-তে দুই টাইপের (Student + Marks) প্রোপার্টি থাকতে হবে।

 Intersection with Interface
interface Address {
  city: string;
}

interface Contact {
  phone: string;
}

type User = Address & Contact;

const user: User = {
  city: "Dhaka",
  phone: "01712345678"
};


Interface এর ক্ষেত্রেও একদম একইভাবে কাজ করে।
```
## Literal Type আসলে কী করে?

Literal type হলো এক ধরনের "constant type" —
মানে: “এই মানটাই শুধু ঠিক আছে, অন্য কিছু নয়।”
```
Example 2 – Number Literal Type
let digit: 1 | 2 | 3;

digit = 1; //  ঠিক আছে
digit = 4; //  Error


 এখানে শুধু ১, ২, বা ৩ মান দেওয়া যাবে।

 Example 3 – Boolean Literal Type
let isActive: true;

isActive = true;  //  ঠিক আছে
isActive = false; //  Error


 এখানে শুধু true মান দেওয়া যাবে।

Example 4 – Function এ Literal Type
function move(direction: "up" | "down" | "left" | "right") {
  console.log("Moving " + direction);
}

move("up");    //  ঠিক আছে
move("right"); //  ঠিক আছে
// move("back");  Error


 এখন move() ফাংশনে শুধু নির্দিষ্ট চারটা শব্দই যাবে।

] Example 5 – Combine with Type Alias
type Status = "success" | "error" | "loading";

function showStatus(status: Status) {
  console.log(`Current status: ${status}`);
}

showStatus("success"); //  ঠিক আছে
showStatus("error");   //  ঠিক আছে
// showStatus("done");  Error


এভাবে তুমি একটি টাইপ বানিয়ে বারবার ব্যবহার করতে পারো।

 Literal Type এর সুবিধা
সুবিধা	ব্যাখ্যা
 নির্দিষ্ট মান নির্ধারণ করা যায়	ভুল মান দেওয়া রোধ করে
 টাইপ-সেফ কোড	TypeScript সাথে সাথে এরর ধরবে
Enum ছাড়া সহজ উপায়ে fixed মান ব্যবহার করা যায়	যেমন "success", "error" ইত্যাদি
Auto-suggestion কাজ করে	IDE তে মান সাজেস্ট করে দেয়
সহজভাবে মনে রাখো:
let direction: "left" | "right";

direction = "left";  // 
direction = "right"; // 
direction = "up";    // Error


Literal Type মানে —
ভেরিয়েবল শুধু নির্দিষ্ট কিছু মানই নিতে পারবে।
```
### Nullable Type in TypeScript

অর্থ:
Nullable টাইপ বলতে বোঝায় এমন ভেরিয়েবল যেটি একটি মান (value) বা null / undefined হতে পারে।
অর্থাৎ, কোনো ভেরিয়েবল যদি খালি (null) বা অনির্ধারিত (undefined) মানও নিতে পারে, তাহলে সেটি nullable type।
```
উদাহরণ ১: সাধারণ nullable type
let username: string | null = "Abdullah";
username = null; // এটা বৈধ


 এখানে username ভেরিয়েবলটি string বা null – দুই ধরনের মানই নিতে পারে।

উদাহরণ ২: null এবং undefined দুটোই
let age: number | null | undefined = 25;
age = null;       // valid
age = undefined;  // valid


মানে — age এর মান ২৫, null, বা undefined — যেকোনোটি হতে পারে।

 উদাহরণ ৩: ফাংশনে nullable parameter
function printName(name: string | null) {
  if (name) {
    console.log("Hello, " + name);
  } else {
    console.log("Hello, guest!");
  }
}

printName("Mamun");
printName(null);

```
 এখানে name প্যারামিটারটি হয় string, নয়তো null হতে পারে।

 কেন দরকার?

Nullable টাইপ ব্যবহারে TypeScript আপনাকে type safety দেয়।
যদি আপনি কোনো ভেরিয়েবল null হতে পারে জেনে সেটার প্রপার্টি এক্সেস করতে যান, TypeScript আগে থেকেই সতর্ক করবে।

 ভুল উদাহরণ:
let user: string | null = null;
console.log(user.toUpperCase()); // Error: Object is possibly 'null'


 কারণ user null হতে পারে, তাই TypeScript এই ভুলটি ধরবে।

সমাধান:
if (user !== null) {
  console.log(user.toUpperCase());
}
type User = {
  name: string;
  age: number | null; // age nullable
};

function showUserInfo(user: User) {
  if (user.age !== null) {
    console.log(`${user.name} is ${user.age} years old.`);
  } else {
    console.log(`${user.name} didn’t provide their age.`);
  }
}

const user1: User = { name: "Abdullah", age: 24 };
const user2: User = { name: "Mamun", age: null };

showUserInfo(user1);
showUserInfo(user2);


### Optional Chaining (?.) in TypeScript
 কি করে?

?. ব্যবহার করে তুমি nullable বা undefined প্রোপার্টি এক্সেস করতে পারো সেফলি,
যদি মান না থাকে (null বা undefined) → TypeError হবে না, শুধু undefined রিটার্ন করবে।
```
 Example ১ – Simple Object
type User = {
  name: string;
  address?: {
    city: string;
    zip?: string;
  };
};

const user1: User = {
  name: "Abdullah",
  address: { city: "Dhaka", zip: "1207" }
};

const user2: User = {
  name: "Mamun"
};

console.log(user1.address?.city); // Dhaka
console.log(user2.address?.city); // undefined (TypeError হবে না!)


 এখানে user2.address নেই, তাই .city এক্সেস করলে error হবে না, শুধু undefined রিটার্ন হয়।

 Example ২ – Function Call
type User = {
  name: string;
  greet?: () => void;
};

const user1: User = { name: "Abdullah", greet: () => console.log("Hello!") };
const user2: User = { name: "Mamun" };

user1.greet?.(); // Hello!
user2.greet?.(); // কিছু হবে না, error হবে না


 Optional chaining দিয়ে nullable function call safely করা হলো।

 Example ৩ – Array Access
const users: User[] = [{ name: "Abdullah" }];

console.log(users[0]?.name); // Abdullah
console.log(users[1]?.name); // undefined


 Array element না থাকলেও error হবে না।

 Example ৪ – Combination with Nullish Coalescing
const user2City = user2.address?.city ?? "Unknown city";
console.log(user2City); // Unknown city


 Optional chaining দিয়ে check + ?? দিয়ে default value set করা হলো।

 কেন ব্যবহার করবে?
সুবিধা	ব্যাখ্যা
 Safe access	nullable বা undefined প্রোপার্টি access safe করে
 Less code	অনেক if/else এর দরকার নেই
 Combine with ??	default value set করা যায় সহজে
 সহজে মনে রাখার নিয়ম
