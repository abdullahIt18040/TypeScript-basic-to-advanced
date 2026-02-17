## Destructuring in TypeScript (Beginner → Advanced)

Destructuring মানে হলো — Array বা Object থেকে value গুলোকে আলাদা variable-এ সহজভাবে বের করে নেওয়া।

👉 Clean code
👉 Short syntax
👉 React / API / Function parameter-এ খুব বেশি ব্যবহার হয়
```
1️⃣ Array Destructuring
const numbers = [10, 20, 30];

const [a, b, c] = numbers;

console.log(a); // 10
console.log(b); // 20
console.log(c); // 30


👉 Index অনুযায়ী value assign হয়।

Skip Value
const numbers = [10, 20, 30];

const [first, , third] = numbers;

console.log(first); // 10
console.log(third); // 30

Default Value
const numbers = [10];

const [a, b = 50] = numbers;

console.log(a); // 10
console.log(b); // 50

2️⃣ Object Destructuring
const user = {
  name: "Mamun",
  age: 25
};

const { name, age } = user;

console.log(name); // Mamun


👉 Property name মিলতে হবে।

Rename Variable
const { name: userName } = user;

console.log(userName);

Default Value
const { city = "Dhaka" } = user;

console.log(city); // Dhaka

3️⃣ Function Parameter-এ Destructuring
type User = {
  name: string;
  age: number;
};

function printUser({ name, age }: User) {
  console.log(`${name} is ${age} years old`);
}

printUser({ name: "Mamun", age: 25 });


👉 React-এ এই pattern খুব common।

4️⃣ Nested Destructuring
const user = {
  name: "Mamun",
  address: {
    city: "Dhaka",
    country: "Bangladesh"
  }
};

const {
  address: { city }
} = user;

console.log(city); // Dhaka

5️⃣ Rest + Destructuring
Array
const numbers = [1, 2, 3, 4];

const [first, ...rest] = numbers;

console.log(first); // 1
console.log(rest);  // [2,3,4]

Object
const user = {
  name: "Mamun",
  age: 25,
  city: "Dhaka"
};

const { name, ...others } = user;

console.log(name);
console.log(others); // { age: 25, city: "Dhaka" }

6️⃣ Real-life Example (React Props)
type ButtonProps = {
  title: string;
  onClick: () => void;
};

function Button({ title, onClick }: ButtonProps) {
  return <button onClick={onClick}>{title}</button>;
}


👉 Direct destructuring করলে clean ও readable হয়।

7️⃣ Destructuring + Spread (Common Pattern)
const user = {
  name: "Mamun",
  age: 25
};

const updatedUser = {
  ...user,
  age: 26
};

```  
👉 React state update-এ খুব গুরুত্বপূর্ণ।
