## for...of Loop in TypeScript (Beginner → Advanced)

for...of loop ব্যবহার করা হয় iterable data structure (যেমন: Array, String, Map, Set) এর ভ্যালু গুলো এক এক করে পাওয়ার জন্য।
```
👉 এটা value নিয়ে কাজ করে
👉 for...in key/index নিয়ে কাজ করে (এইটা আলাদা)

1️⃣ Basic Example (Array)
const numbers = [10, 20, 30];

for (const num of numbers) {
  console.log(num);
}


🔹 Output:

10
20
30


এখানে num হচ্ছে প্রতিটা element-এর value।

2️⃣ String এর উপর for...of
const name = "Mamun";

for (const char of name) {
  console.log(char);
}


🔹 Output:

M
a
m
u
n


👉 String ও iterable তাই কাজ করে।

3️⃣ Typed Array Example (TypeScript)
const users: string[] = ["Mamun", "Rahim", "Karim"];

for (const user of users) {
  console.log(user.toUpperCase());
}


✅ TypeScript জানে user হলো string
👉 তাই toUpperCase() error দেয় না।

4️⃣ Object এর ক্ষেত্রে সমস্যা ❌
const user = {
  name: "Mamun",
  age: 25
};

for (const item of user) { // ❌ Error
}


👉 Object iterable না, তাই for...of সরাসরি কাজ করে না।

✅ সমাধান:
for (const key of Object.keys(user)) {
  console.log(key, user[key as keyof typeof user]);
}

5️⃣ for...of vs for...in
for...of	for...in
Value দেয়	Key / Index দেয়
Array, String এ বেশি ব্যবহার	Object-এ বেশি ব্যবহার
Example:
const numbers = [10, 20, 30];

for (const index in numbers) {
  console.log(index); // 0,1,2
}

for (const value of numbers) {
  console.log(value); // 10,20,30
}

6️⃣ Map এর সাথে ব্যবহার
const map = new Map<string, number>();
map.set("apple", 100);
map.set("banana", 200);

for (const [key, value] of map) {
  console.log(key, value);
}


👉 Output:

apple 100
banana 200

7️⃣ Set এর সাথে ব্যবহার
const set = new Set<number>([1, 2, 3]);

for (const value of set) {
  console.log(value);
}

8️⃣ Advanced: Break / Continue
const numbers = [1, 2, 3, 4, 5];

for (const num of numbers) {
  if (num === 3) continue;
  if (num === 5) break;

  console.log(num);
}


👉 Output:

1
2
4

🧠 কখন ব্যবহার করবে?

✔ যখন শুধু value দরকার
✔ যখন array cleanভাবে loop করতে চাও
✔ React-এ list iterate করার আগে processing করতে

🚀 Real-life Example (Product Processing)
type Product = {
  id: number;
  name: string;
  price: number;
};

const products: Product[] = [
  { id: 1, name: "Laptop", price: 50000 },
  { id: 2, name: "Mobile", price: 20000 }
];

for (const product of products) {
  console.log(`${product.name} - ${product.price}`);
}
```
🔑 Summary
