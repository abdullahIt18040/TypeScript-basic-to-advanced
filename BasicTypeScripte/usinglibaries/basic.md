TypeScript প্রজেক্টে Third-Party Library ইনস্টল করা মানে হলো বাইরের কোনো package বা library ব্যবহার করা, যা অন্য কেউ তৈরি করেছে এবং আপনি আপনার প্রজেক্টে ব্যবহার করবেন।

সাধারণত এটি **Node.js ecosystem এর package manager যেমন npm বা Yarn দিয়ে করা হয়।

## ১. Third-Party Library কী?

Third-party library হলো এমন external code package যা আপনি নিজের code না লিখে ব্যবহার করতে পারেন।
```
Example:

HTTP request করার জন্য → Axios

Date handling → Moment.js

Utility functions → Lodash

২. Library Install করা (npm)

সবচেয়ে common উপায়:

npm install axios

অথবা shorthand:

npm i axios

এতে:

node_modules folder এ library install হবে

package.json এ dependency add হবে

Example:

"dependencies": {
  "axios": "^1.6.0"
}
৩. Library Import করা

Install করার পরে code এ ব্যবহার করা যায়।

import axios from "axios";

axios.get("https://api.example.com/data")
  .then(res => console.log(res.data));
৪. TypeScript এ Types Install করা

অনেক library JavaScript এ লেখা থাকে। তখন TypeScript types আলাদা করে install করতে হয়।

Example:

npm install --save-dev @types/lodash

এখানে:

@types package TypeScript type definition দেয়

Example:

import _ from "lodash";

const nums = [1, 2, 3];
console.log(_.reverse(nums));
৫. Dev Dependency Install করা

যদি library শুধু development এর জন্য লাগে (যেমন testing tool) তাহলে:

npm install --save-dev jest

Example tools:

Jest

ESLint

৬. Yarn দিয়ে Install করা

যদি **Yarn ব্যবহার করেন:

yarn add axios

Dev dependency:

yarn add -D jest
৭. Full Example

Step 1: Install library

npm install lodash

Step 2: Install types

npm install --save-dev @types/lodash

Step 3: Use in TypeScript

import _ from "lodash";

const arr = [1,2,3,4];

const reversed = _.reverse(arr);

console.log(reversed);

Output

[4,3,2,1]

✅ সংক্ষেপে

Third-party library install করার ধাপ:

1️⃣ npm install library-name
2️⃣ (প্রয়োজনে) @types/library-name install করা
3️⃣ import করে ব্যবহার করা

যদি চান, আমি আরও দেখাতে পারি:

TypeScript project setup with npm (step by step)

package.json deep explanation

Common npm commands every developer should know

Angular / React project এ library install করার নিয়ম।
```
