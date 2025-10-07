#  TypeScript `tsconfig.json` --- Basic to Advanced Explanation (with Bangla Example)
{
  "compilerOptions": {

  
  
   

    /*  Core settings */
    
     "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,

    /*  Module system */
    "module": "esnext",
    "moduleResolution": "bundler",

    /*  Extra features */
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,

    /*  Plugin for Next.js */
    "plugins": [
      {
        "name": "next"
      }
    ],

    /* Path aliases (optional but handy) */
    "paths": {
      "@/*": ["./src/*"]
    }
  },

  /* Included files */
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],

  /*  Excluded folders */
  "exclude": ["node_modules"]

  
}



## **Basic Options (মূল সেটিংস)**

### 1. `"lib": ["dom", "dom.iterable", "esnext"]`

 এটি TypeScript-কে জানায় কোন JavaScript ফিচার ও ব্রাউজার API ব্যবহার
করা যাবে।

**উদাহরণ:**

``` ts
const button = document.createElement("button"); // "dom" এর কারণে কাজ করবে
button.innerText = "Click Me";
document.body.appendChild(button);
```

যদি `"dom"` না দাও, তাহলে TypeScript এরর দেখাবে: \> "Cannot find name
'document'."

------------------------------------------------------------------------

### 2. `"allowJs": true`

 TypeScript প্রোজেক্টে `.js` ফাইল ব্যবহার করার অনুমতি দেয়।

**Project structure:**

    project/
     ├─ src/
     │   ├─ index.ts
     │   ├─ helper.js

**index.ts:**

``` ts
import { greet } from "./helper"; // helper.js থেকেও import করা যাবে
```

------------------------------------------------------------------------

###  3. `"skipLibCheck": true`

টাইপ ডিফিনিশন ফাইলগুলোর (`.d.ts`) টাইপ চেক না করে স্কিপ করে --- ফলে
বিল্ড দ্রুত হয়।

**উদাহরণ:** যদি কোনো থার্ড-পার্টি প্যাকেজে ভুল টাইপ ডিফিনিশন থাকে, তবুও
এরর দেবে না।

``` bash
# build করার সময় কোনো টাইপ এরর এড়ানো যাবে
```

------------------------------------------------------------------------

### 4. `"strict": true`
 সব ধরনের টাইপ চেক চালু করে।

**উদাহরণ:**

``` ts
let name: string;
name = "Mamun"; //  ঠিক আছে
name = null; //  Error, কারণ strictNullChecks চালু আছে
```

------------------------------------------------------------------------

### 5. `"noEmit": true`

 TypeScript শুধু টাইপ চেক করবে, কিন্তু কোনো `.js` আউটপুট ফাইল তৈরি
করবে না।

**উদাহরণ:**

``` bash
tsc
# কোনো .js ফাইল তৈরি হবে না, শুধু এরর চেক করবে
```

 Next.js বা Vite-এর মতো প্রোজেক্টে এটি সাধারণত ব্যবহৃত হয় কারণ তারা
নিজেরা বিল্ড করে।

------------------------------------------------------------------------

### 6. `"esModuleInterop": true`

CommonJS ও ES Modules একসাথে কাজ করতে দেয়।

**উদাহরণ:**

``` ts
// CommonJS স্টাইল
const express = require("express");

// ES Module স্টাইল
import express from "express"; //  এটি এখন কাজ করবে
```

------------------------------------------------------------------------

### 7. `"module": "esnext"`

 সর্বশেষ ES মডিউল সিস্টেম ব্যবহার করতে দেয় (`import/export`)।

**উদাহরণ:**

``` ts
// file: math.ts
export const add = (a: number, b: number) => a + b;

// file: app.ts
import { add } from "./math";
console.log(add(2, 3));
```

------------------------------------------------------------------------

### 8. `"moduleResolution": "bundler"`

 TypeScript মডিউল কিভাবে রিজলভ করবে সেটি বলে দেয়।\
`"bundler"` মানে আধুনিক টুল যেমন **Next.js**, **Vite**, **Webpack** এর
নিয়মে ফাইল খোঁজবে।

**উদাহরণ:**

``` ts
import Button from "@/components/Button";
```

এটি `paths` সেটিং অনুযায়ী resolve হবে।

------------------------------------------------------------------------

### 9. `"resolveJsonModule": true"`

`.json` ফাইল সরাসরি import করতে দেয়।

**উদাহরণ:**

``` json
// data.json
{
  "name": "Mamun",
  "age": 25
}
```

``` ts
import data from "./data.json";
console.log(data.name); // "Mamun"
```

------------------------------------------------------------------------

###  10. `"isolatedModules": true"`

 প্রতিটি ফাইলকে আলাদা মডিউল হিসেবে ধরে।\
এটি React/Next.js প্রোজেক্টে প্রয়োজনীয়।

**উদাহরণ:**

``` ts
//  Error যদি কোনো ফাইল মডিউল না হয়
let x = 10;

// ঠিক করতে হবে
export {};
```

------------------------------------------------------------------------

###  11. `"jsx": "preserve"`

JSX কোড TypeScript ট্রান্সফর্ম না করে রাখে (Next.js নিজেই JSX
হ্যান্ডেল করে)।

**উদাহরণ:**

``` tsx
function App() {
  return <h1>Hello World</h1>;
}
```

TypeScript এটিকে JSX অবস্থায় রেখে দেবে, Next.js পরে এটিকে React কোডে
রূপান্তর করবে।

------------------------------------------------------------------------

## **Advanced Options**

### 12. `"incremental": true"`

আগের বিল্ডের আউটপুট সংরক্ষণ করে, যাতে পরের বিল্ডগুলো দ্রুত হয়।

**উদাহরণ:**\
প্রথমবার `tsc` চালালে সময় বেশি লাগবে,\
পরের বার শুধু পরিবর্তিত ফাইল রিকম্পাইল হবে।

------------------------------------------------------------------------

### 13. `"plugins": [{ "name": "next" }]`

 Next.js-এর জন্য TypeScript প্লাগইন ব্যবহার করে --- এটি Next.js-এর
টাইপ ইন্টেলিজেন্স বাড়ায়।\
যেমন: `getStaticProps`, `getServerSideProps` ইত্যাদি টাইপ চিনতে পারে।

------------------------------------------------------------------------

### 14. `"paths": { "@/*": ["./src/*"] }"`

 Path alias তৈরি করে, যাতে লম্বা relative path না লিখতে হয়।

**উদাহরণ:**

``` ts
// আগে:
import Button from "../../../components/Button";

// এখন:
import Button from "@/components/Button"; //  অনেক ছোট ও পরিষ্কার
```

------------------------------------------------------------------------

##  **সারসংক্ষেপ (Table View)**

  -----------------------------------------------------------------------------
  অপশন                  কাজ                  উদাহরণ
  --------------------- -------------------- ----------------------------------
  `lib`                 কোন JS ফিচার ও API   `"dom"`, `"esnext"`
                        ব্যবহার করা যাবে     

  `allowJs`             `.js` ফাইল ইমপোর্ট   `import from "./file.js"`
                        করা যাবে             

  `skipLibCheck`        টাইপ চেক স্কিপ       দ্রুত বিল্ড

  `strict`              কঠোর টাইপ চেক        `let x: string = null; // ❌`

  `noEmit`              `.js` ফাইল তৈরি বন্ধ শুধু টাইপ চেক

  `esModuleInterop`     CommonJS + ES        `import express from 'express'`
                        Modules একসাথে       

  `module`              মডিউল সিস্টেম        `"esnext"`

  `moduleResolution`    ফাইল খোঁজার পদ্ধতি   `"bundler"`

  `resolveJsonModule`   `.json` ফাইল ইমপোর্ট `import data from './data.json'`

  `isolatedModules`     প্রতিটি ফাইল আলাদা   `export {};`
                        মডিউল                

  `jsx`                 JSX ট্রান্সফর্ম      `"preserve"`

  `incremental`         দ্রুত বিল্ড          ক্যাশ ব্যবহার

  `plugins`             Next.js TypeScript   `{ "name": "next" }`
                        সাপোর্ট              

  `paths`               Path alias           `"@/*": ["./src/*"]`
  -----------------------------------------------------------------------------

------------------------------------------------------------------------

 **Tip:**\
এই কনফিগারেশনটি বিশেষভাবে **Next.js + TypeScript + Tailwind CSS**
প্রোজেক্টের জন্য খুবই উপযোগী।
https://medium.com/@kithma/beginners-guide-to-tsconfig-json-462489891663
