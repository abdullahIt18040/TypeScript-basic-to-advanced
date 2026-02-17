## Rest Operator (...) in TypeScript

Rest (...) ব্যবহার করা হয় একাধিক value কে একসাথে collect করার জন্য।
এটা দুই জায়গায় ব্যবহার হয়:
```
Function parameter-এ → Rest Parameter

Destructuring-এ → Remaining value collect করা

1️⃣ Rest Parameter (Function-এ)

যখন জানি না কতগুলো argument আসবে:

function sum(...numbers: number[]): number {
  return numbers.reduce((total, n) => total + n, 0);
}

console.log(sum(10, 20));        // 30
console.log(sum(1, 2, 3, 4));    // 10


👉 numbers হচ্ছে number[]
👉 সব argument একসাথে array হিসেবে নেয়

⚠ সবসময় শেষ parameter হতে হবে:

// ❌ ভুল
function test(...nums: number[], name: string) {}

2️⃣ Normal + Rest একসাথে
function greet(message: string, ...names: string[]) {
  for (const name of names) {
    console.log(`${message}, ${name}`);
  }
}

greet("Hello", "Mamun", "Rahim");

3️⃣ Array Destructuring-এ Rest
const numbers = [10, 20, 30, 40];

const [first, ...rest] = numbers;

console.log(first); // 10
console.log(rest);  // [20, 30, 40]


👉 বাকি সব value rest-এ চলে যায়।

4️⃣ Object Destructuring-এ Rest
const user = {
  name: "Mamun",
  age: 25,
  city: "Dhaka"
};

const { name, ...otherInfo } = user;

console.log(name);       // Mamun
console.log(otherInfo);  // { age: 25, city: "Dhaka" }


👉 Remaining property collect হয়।

🔥 Advanced
5️⃣ Tuple + Rest
function studentInfo(...info: [string, number, boolean]) {
  const [name, age, isActive] = info;

  console.log(name, age, isActive);
}

studentInfo("Mamun", 25, true);


👉 এখানে argument order strict থাকবে।

6️⃣ Generic Rest Parameter
function combine<T>(...items: T[]): T[] {
  return items;
}

console.log(combine(1, 2, 3));
console.log(combine("a", "b"));


👉 Type automatically detect হয়।
```
## Spread Operator (...) in TypeScript (Beginner → Advanced)

Spread (...) ব্যবহার করা হয় কোনো iterable (Array, Object, String) কে
👉 expand (ভেঙে আলাদা করা) করার জন্য।

📌 মনে রাখবে:

Rest → collect করে

Spread → expand করে
```
1️⃣ Array Spread
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

const merged = [...arr1, ...arr2];

console.log(merged);
// [1, 2, 3, 4, 5, 6]


👉 দুইটা array merge করার সবচেয়ে clean উপায়।

2️⃣ Copy Array (Shallow Copy)
const numbers = [10, 20, 30];

const copy = [...numbers];

copy.push(40);

console.log(numbers); // [10,20,30]
console.log(copy);    // [10,20,30,40]


⚠ এটা shallow copy, deep copy না।

3️⃣ Object Spread
const user = {
  name: "Mamun",
  age: 25
};

const updatedUser = {
  ...user,
  age: 26
};

console.log(updatedUser);


👉 existing object copy + value update

4️⃣ Object Merge
const address = {
  city: "Dhaka",
  country: "Bangladesh"
};

const userProfile = {
  ...user,
  ...address
};


👉 multiple object merge করা যায়।

⚠ যদি same key থাকে → last value override করবে।

5️⃣ Function Call-এ Spread
function sum(a: number, b: number, c: number) {
  return a + b + c;
}

const numbers = [10, 20, 30];

console.log(sum(...numbers)); // 60


👉 array কে আলাদা argument বানিয়ে দেয়।

6️⃣ Spread with String
const name = "Mamun";

const chars = [...name];

console.log(chars);
// ["M", "a", "m", "u", "n"]

🔥 Advanced TypeScript
7️⃣ Spread with Tuple
type Person = [string, number];

const person: Person = ["Mamun", 25];

const updated = [...person, true];

console.log(updated);
// ["Mamun", 25, true]

8️⃣ Spread with Generic Function
function merge<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const result = merge(
  { name: "Mamun" },
  { age: 25 }
);

console.log(result);
// { name: "Mamun", age: 25 }


👉 return type automatically combine হয়।

🔁 Spread vs Rest (Confusion Clear)
Spread	Rest
Expand করে	Collect করে
Function call-এ	Function parameter-এ
Array/Object copy	Multiple argument নেয়
🚀 Real-life Example (React State Update)
const [user, setUser] = useState({
  name: "Mamun",
  age: 25
});

setUser({
  ...user,
  age: 26
});


👉 React-এ immutable update করতে খুব গুরুত্বপূর্ণ।

⚠ Important: Shallow Copy Problem
const user = {
  name: "Mamun",
  address: {
    city: "Dhaka"
  }
};

const copy = { ...user };

copy.address.city = "Chittagong";

console.log(user.address.city);
// Chittagong ❗


👉 nested object copy হয় না (shallow copy)
```
