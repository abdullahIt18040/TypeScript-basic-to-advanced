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
