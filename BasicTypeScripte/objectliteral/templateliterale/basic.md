## Template Literal in TypeScript (Beginner → Advanced)

Template Literal হলো string লেখার একটি modern উপায়, যেখানে
👉 backtick ` ব্যবহার করা হয়
👉 ${} দিয়ে variable বা expression বসানো যায়
```
1️⃣ Basic Template Literal
const name = "Mamun";
const age = 25;

const message = `My name is ${name} and I am ${age} years old.`;

console.log(message);


🔹 Output:

My name is Mamun and I am 25 years old.


✅ আগের মতো "My name is " + name লিখতে হয় না
✅ বেশি readable

2️⃣ Multi-line String
const address = `
Dhaka
Bangladesh
Asia
`;

console.log(address);


👉 Template literal দিয়ে multi-line string খুব সহজ

3️⃣ Expression ব্যবহার
const a = 10;
const b = 20;

console.log(`Sum is ${a + b}`);


🔹 Output:

Sum is 30


👉 ${} এর ভিতরে যেকোনো valid expression লিখতে পারো

4️⃣ Function Call inside Template Literal
function greet(name: string): string {
  return `Hello ${name}`;
}

console.log(`${greet("Mamun")} 👋`);

🔥 Advanced (TypeScript Feature)

TypeScript-এ Template Literal শুধু string না,
👉 Type level programming-এও ব্যবহার হয়।

5️⃣ Template Literal Types
type Status = "success" | "error";

type Message = `Request-${Status}`;


এখন:

let msg: Message;

msg = "Request-success"; // ✅
msg = "Request-error";   // ✅
msg = "Request-pending"; // ❌ Error


👉 এখানে string literal type combine হচ্ছে

6️⃣ Dynamic Key Generate করা
type User = {
  id: number;
  name: string;
};

type UserKeys = keyof User; 
// "id" | "name"

type Getter = `get${Capitalize<UserKeys>}`;
// "getId" | "getName"


👉 বড় project-এ খুব powerful

7️⃣ Real-life Example (API URL)
const baseUrl = "https://api.example.com";
const userId = 10;

const url = `${baseUrl}/users/${userId}`;

8️⃣ React Example (UI Rendering)
const product = {
  name: "Laptop",
  price: 50000
};

return <h1>{`Product: ${product.name} - ৳${product.price}`}</h1>;
```
