##  JavaScript কী?
```
👉 JavaScript হলো একটি programming language
👉 এটা browser-এ run করে এবং website কে dynamic করে

🔹 Example (Pure JavaScript)
<button id="btn">Click Me</button>
<p id="text"></p>

<script>
document.getElementById("btn").addEventListener("click", function() {
    document.getElementById("text").innerHTML = "Hello JavaScript!";
});
</script>

👉 এখানে:

button click করলে text change হয়
```
### 🔰jQuery কী?
```
👉 jQuery হলো JavaScript-এর উপর built একটি library
👉 এটা same কাজকে সহজ ও ছোট code দিয়ে করে

🔹 Same Example (jQuery দিয়ে)
<button id="btn">Click Me</button>
<p id="text"></p>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<script>
$("#btn").click(function() {
    $("#text").text("Hello jQuery!");
});
</script>

👉 এখানে:

$ = jQuery shortcut
code অনেক ছোট
```

### Why we use jQuery over JavaScript
```
👉 মূল idea:

jQuery = কম code + সহজ syntax + faster development

1️⃣ DOM Manipulation সহজ করা

👉 HTML element change করা JavaScript এ একটু verbose হয়

❌ JavaScript:
document.getElementById("text").innerHTML = "Hello";

👉 সমস্যা:

long code
বারবার document.getElementById লিখতে হয়
✅ jQuery:
$("#text").text("Hello");

👉 সুবিধা:
✔ ছোট
✔ readable
✔ দ্রুত লেখা যায়

🔥 Real Example
<p id="msg">Old Text</p>
<button id="btn">Change</button>

👉 JavaScript:

document.getElementById("btn").addEventListener("click", function() {
    document.getElementById("msg").innerHTML = "New Text";
});

👉 jQuery:

$("#btn").click(function() {
    $("#msg").text("New Text");
});

✔ jQuery clearly shorter 👍

2️⃣ Event Handling সহজ

👉 event handle করা JavaScript এ একটু complex

❌ JavaScript:
document.getElementById("btn").addEventListener("click", function() {
    alert("Clicked!");
});
✅ jQuery:
$("#btn").click(function() {
    alert("Clicked!");
});

👉 সুবিধা:
✔ simple syntax
✔ less boilerplate code

🔥 Multiple Events Example
$("#btn").on("click mouseover", function() {
    console.log("Event triggered");
});

👉 JavaScript এ এটা আলাদা আলাদা লিখতে হয়

3️⃣ AJAX Call সহজ করা

👉 server call JavaScript এ আগে খুব complex ছিল

❌ JavaScript (old way - XMLHttpRequest):
var xhr = new XMLHttpRequest();
xhr.open("GET", "/api/data");
xhr.onload = function() {
    console.log(xhr.responseText);
};
xhr.send();

👉 অনেক boilerplate 😓

✅ jQuery:
$.ajax({
    url: "/api/data",
    success: function(data) {
        console.log(data);
    }
});

👉 সুবিধা:
✔ clean
✔ easy to read
✔ less code

```
### TO used Jquery in type scripte project:
```
Step 1: Install (Real Project)
npm install jquery
npm install --save-dev @types/jquery

👉 Real life:

team project এ সবাই clean code চায়
TypeScript error avoid করতে @types must
🧩 Step 3: UI Example (HTML)
<button id="loadBtn">Load Students</button>
<ul id="list"></ul>
🚀 Step 4: TypeScript + jQuery (Real Work)
import $ from "jquery";

$("#loadBtn").click(() => {
    $.ajax({
        url: "/api/students",
        method: "GET",
        success: (students: any[]) => {

            $("#list").empty();

            students.forEach(s => {
                $("#list").append(`<li>${s.name}</li>`);
            });
        }
    });
});
🔥 What is happening here? (Real Understanding)

👉 User button click করলো
👉 jQuery event ধরলো
👉 API call করলো
👉 data পেলো
👉 UI update করলো

✔ সবকিছু very short code এ done ✅

🧠 যদি JavaScript দিয়ে করতে?
document.getElementById("loadBtn").addEventListener("click", function() {

    fetch("/api/students")
    .then(res => res.json())
    .then(students => {

        let list = document.getElementById("list");
        list.innerHTML = "";

        students.forEach(s => {
            let li = document.createElement("li");
            li.innerText = s.name;
            list.appendChild(li);
        });
    });

});

👉 কাজ same 😅
কিন্তু:
❌ code বেশি
❌ readable কম
```
### Use jQuery in TypeScript
```
import $ from "jquery";

$(document).ready(() => {
    $("#btn").click(() => {
        alert("Clicked!");
    });
});

👉 এখন:

$ properly কাজ করবে
TypeScript error দিবে না

3. tsconfig.json Configuration

যদি import এ সমস্যা হয়:

{
  "compilerOptions": {
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true
  }
}

👉 এটা না দিলে:
❌ import $ from 'jquery' error দিতে পারে
. Intermediate Usage
✅ Event Handling
$("#btn").on("click", (e: JQuery.ClickEvent) => {
    console.log("Clicked");
});
✅ DOM Manipulation
$("#text").text("Hello TS");
$("#box").css("color", "blue");
✅ AJAX Call
$.ajax({
    url: "/api/data",
    method: "GET",
    success: (res: any) => {
        console.log(res);
    }
});

Advanced Usage
✅ 6.1 Type-safe Data Handling
interface User {
    id: number;
    name: string;
}

$.ajax<User[]>({
    url: "/api/users",
    method: "GET",
    success: (users) => {
        users.forEach(u => console.log(u.name));
    }
});
.d.ts file কী?

👉 .d.ts = Declaration file
👉 এতে শুধু থাকে:

type
structure
function signature
👉 কিন্তু actual logic (code) থাকে না
🧠 সহজভাবে বুঝো

👉 ধরো তুমি একটা library ব্যবহার করছো (like jQuery)

JavaScript জানে:

$("#id").hide();

👉 কিন্তু TypeScript জানে না:

$ কী?
.hide() কী?

👉 তখন .d.ts file TypeScript কে শেখায়:

“এই function আছে, এই type আছে”

📦 Real Example (jQuery)
1️⃣ Without .d.ts (Problem)
$("#box").hide();

👉 Error:
❌ $ not found
❌ hide() unknown

2️⃣ With .d.ts (Solution)

👉 install:

npm install --save-dev @types/jquery

👉 এখন TypeScript জানে:

$("#box").hide(); // ✔ OK
```
## 🧩 .d.ts ভিতরে কী থাকে?
```
Example:

declare function $(selector: string): JQuery;

interface JQuery {
    hide(): JQuery;
    show(): JQuery;
    text(value: string): JQuery;
}

👉 মানে:

$ একটা function
.hide() valid method
return type defined
🚀 কেন .d.ts ব্যবহার করা হয়?
✔ 1. Type Safety
$("#box").hie(); // ❌ error (compile time)
✔ 2. Autocomplete

👉 IDE নিজে suggest করবে:

hide()
show()
text()
✔ 3. Library Support

👉 অনেক JavaScript library already আছে:

jQuery
Lodash
Axios

👉 এগুলোর জন্য .d.ts দরকার
```


###  তুমি যখন পুরোনো JavaScript code কে TypeScript এ convert করো, তখন TypeScript বুঝতে চায়:
```

function কী type?
variable কী type?
library কী type?

👉 এই gap fill করে:

TypeScript Definition Files (.d.ts)

🧠 2. Type Definition File কী?

👉 .d.ts file হলো:

JavaScript code-এর “type blueprint” (structure map)

👉 এটা বলে:

function কী return করবে
parameter কী type
object কী structure
⚙️ 3. Real Example (Without TypeScript)
JavaScript code:
function add(a, b) {
    return a + b;
}

👉 এখানে কোনো type নেই

🔥 4. TypeScript Version (Manual Translation)
function add(a: number, b: number): number {
    return a + b;
}

✔ এখন TypeScript বুঝে ফেলেছে

📦 5. But Problem in Real Life

👉 ধরো তুমি use করছো library:
jQuery

$("#id").hide();

👉 TypeScript জানে না:

$ কী?
.hide() কী?
🧩 6. Solution: Type Definition File

👉 আমরা install করি:

npm install --save-dev @types/jquery
🧠 7. Inside .d.ts (Concept Example)
interface JQuery {
    hide(): JQuery;
    show(): JQuery;
    text(content: string): JQuery;
}

declare function $(selector: string): JQuery;

👉 এটা TypeScript কে বলে:

$ একটা function
.hide() available method
🚀 8. Translating JavaScript to TypeScript (Real Flow)
Step 1: Old JavaScript
$("#btn").click(function() {
    alert("Hello");
});
Step 2: Add TypeScript understanding (via @types)

👉 install:

npm install --save-dev @types/jquery
Step 3: TypeScript version
import $ from "jquery";

$("#btn").click(() => {
    alert("Hello");
});

✔ এখন error নেই
✔ autocomplete আছে
✔ safe code

🔥 9. Why Definition Files Important?

👉 এগুলো ছাড়া TypeScript:

❌ library বুঝবে না
❌ error দিবে
❌ autocomplete কাজ করবে না

👉 এগুলোর সাথে:

✔ smart IDE support
✔ type safety
✔ bug reduction
```
