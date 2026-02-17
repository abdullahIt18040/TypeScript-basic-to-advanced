## Object Literal মানে হলো—কোডের মধ্যেই সরাসরি {} ব্যবহার করে একটি object তৈরি করা। TypeScript-এ object literal খুব শক্তিশালী, কারণ এখানে type safety, inference, এবং advanced typing পাওয়া যায়।
```
1️⃣ Basic Object Literal
const user = {
  name: "Mamun",
  age: 25,
  isActive: true
};


TypeScript এখানে automatically type infer করে:

// inferred type
{
  name: string;
  age: number;
  isActive: boolean;
}


✅ সুবিধা: আলাদা করে type না লিখলেও চলে
❌ সমস্যা: reuse করা কঠিন

2️⃣ Object Literal with Explicit Type
const user: {
  name: string;
  age: number;
} = {
  name: "Mamun",
  age: 25
};


✅ Strict checking
❌ বড় হলে messy হয়ে যায়

3️⃣ Using type with Object Literal (Best Practice)
type User = {
  name: string;
  age: number;
  isActive: boolean;
};

const user: User = {
  name: "Mamun",
  age: 25,
  isActive: true
};


✅ Reusable
✅ Clean & readable

4️⃣ Optional Properties (?)
type User = {
  name: string;
  age?: number;
};

const user1: User = { name: "Mamun" };
const user2: User = { name: "Rahim", age: 30 };


👉 age থাকতেও পারে, না থাকতেও পারে

5️⃣ Readonly Properties
type User = {
  readonly id: number;
  name: string;
};

const user: User = {
  id: 1,
  name: "Mamun"
};

// user.id = 2 ❌ Error


🔒 Immutable data নিশ্চিত করে

6️⃣ Object Literal with Methods
const user = {
  name: "Mamun",
  greet(): string {
    return `Hello ${this.name}`;
  }
};

user.greet(); // Hello Mamun


👉 this object-কেই refer করে

7️⃣ Nested Object Literal
type User = {
  name: string;
  address: {
    city: string;
    country: string;
  };
};

const user: User = {
  name: "Mamun",
  address: {
    city: "Dhaka",
    country: "Bangladesh"
  }
};

8️⃣ Index Signature (Dynamic Keys)
type ScoreBoard = {
  [playerName: string]: number;
};

const scores: ScoreBoard = {
  mamun: 90,
  rahim: 85
};


👉 Key আগে থেকে জানা না থাকলে ব্যবহার হয়

9️⃣ Object Literal + Interface
interface User {
  name: string;
  age: number;
}

const user: User = {
  name: "Mamun",
  age: 25
};


🟢 interface object structure define করার জন্য খুব জনপ্রিয়

🔟 Excess Property Check (Important!)
type User = {
  name: string;
};

const user: User = {
  name: "Mamun",
  age: 25 // ❌ Error
};


👉 Object literal-এ extra property থাকলে TypeScript error দেয়
(এটাই TypeScript-এর বড় advantage)

🧠 Advanced: as const
const config = {
  mode: "dark",
  version: 1
} as const;


Result:

mode: "dark"   // literal type
version: 1


👉 Values change করা যাবে না

🔁 Object Literal vs Class
Object Literal	Class
Lightweight	Heavy
Simple data	Business logic
Quick use	Reusable blueprint
✅ Real-life Usage (React / API)
const apiResponse = {
  status: 200,
  message: "Success",
  data: {
    id: 1,
    name: "Mamun"
  }
};
```
