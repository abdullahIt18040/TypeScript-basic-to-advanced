
TypeScript এ Decorator হলো এমন একটি special function, যা class, method, property বা parameter-এর behavior পরিবর্তন বা অতিরিক্ত functionality যোগ করতে ব্যবহার করা হয়।

Decorator ব্যবহার করার সময় @ symbol ব্যবহার করা হয়।
```
১. Decorator কী?

সহজভাবে বললে:

Decorator হলো এমন একটি function যা কোনো class বা তার member-এ extra behavior যোগ করে।

উদাহরণ:

function Logger(constructor: Function) {
  console.log("Class created:", constructor.name);
}

@Logger
class Person {
  name = "Mamun";
}

এখানে @Logger হলো একটি Decorator।
যখন Person class তৈরি হবে তখন Logger function execute হবে।

২. TypeScript এ Decorator Enable করা

Decorator ব্যবহার করতে হলে tsconfig.json ফাইলে enable করতে হয়।

{
  "compilerOptions": {
    "experimentalDecorators": true
  }
}
৩. TypeScript এ Decorator এর ধরন

Decorator সাধারণত ৫ ধরনের হয়।

Class Decorator

Method Decorator

Property Decorator

Accessor Decorator

Parameter Decorator

৪. Class Decorator

যখন কোনো class এর উপর decorator ব্যবহার করা হয়, তখন তাকে Class Decorator বলে।

function ClassInfo(constructor: Function) {
  console.log("This is a class decorator");
}

@ClassInfo
class Student {
  name = "Rahim";
}

এখানে @ClassInfo class-এর উপর কাজ করছে।

৫. Method Decorator

যখন class এর method-এর উপর decorator ব্যবহার করা হয় তখন তাকে Method Decorator বলে।

function Log(target: any, methodName: string) {
  console.log("Method name:", methodName);
}

class Calculator {
  @Log
  add(a: number, b: number) {
    return a + b;
  }
}

এখানে @Log method-এর নাম log করবে।

৬. Property Decorator

যখন class এর property-এর উপর decorator ব্যবহার করা হয় তখন তাকে Property Decorator বলে।

function PropertyLog(target: any, propertyName: string) {
  console.log("Property:", propertyName);
}

class User {
  @PropertyLog
  username: string;
}

এখানে username property detect করবে।

৭. Parameter Decorator

যখন method এর parameter-এ decorator ব্যবহার করা হয় তখন তাকে Parameter Decorator বলে।

function ParamLog(target: any, methodName: string, index: number) {
  console.log("Parameter index:", index);
}

class Test {
  print(@ParamLog message: string) {
    console.log(message);
  }
}
৮. বাস্তব ব্যবহার (Real Life Use)

Decorator অনেক framework-এ ব্যবহার হয়, যেমন:

Angular

NestJS

উদাহরণ (Angular):

@Component({
  selector: 'app-root'
})
export class AppComponent {}

এখানে @Component একটি Decorator।

৯. Decorator কেন ব্যবহার করা হয়

Decorator ব্যবহার করা হয়:

Logging করার জন্য

Validation করার জন্য

Metadata যোগ করার জন্য

Dependency Injection করার জন্য
```

Framework configuration করার জন্য
### Decorator Factory কী?

সহজভাবে:

Decorator Factory হলো এমন একটি function যা parameter নিয়ে একটি decorator return করে।
```
Structure:

function DecoratorFactory(parameter) {
  return function(target) {
    // decorator logic
  };
}

ব্যবহার:

@DecoratorFactory("Hello")
class Test {}
২. Simple Example
function Logger(message: string) {
  return function (constructor: Function) {
    console.log(message);
    console.log(constructor.name);
  };
}

@Logger("This is a decorator factory")
class Person {
  name = "Mamun";
}

Output

This is a decorator factory
Person

এখানে:

Logger() হলো Decorator Factory

ভিতরের function হলো actual decorator

৩. Method Decorator Factory Example
function LogMethod(prefix: string) {
  return function (
    target: any,
    methodName: string,
    descriptor: PropertyDescriptor
  ) {
    console.log(prefix + methodName);
  };
}

class Calculator {
  @LogMethod("Executing method: ")
  add(a: number, b: number) {
    return a + b;
  }
}

Output

Executing method: add
```
## TypeScript এ Useful Decorator তৈরি করা মানে এমন decorator বানানো যা বাস্তবে logging, validation, caching, authorization ইত্যাদি কাজে লাগে।

নিচে কয়েকটি practical example দেখানো হলো।
```
১. Logging Decorator (Method Call Track করা)

এই decorator method call হলে log দেখাবে।

function LogExecution(
  target: any,
  methodName: string,
  descriptor: PropertyDescriptor
) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Method ${methodName} called with`, args);
    const result = originalMethod.apply(this, args);
    console.log(`Method ${methodName} returned`, result);
    return result;
  };
}

ব্যবহার:

class Calculator {

  @LogExecution
  add(a: number, b: number) {
    return a + b;
  }

}

const calc = new Calculator();
calc.add(5, 3);

Output:

Method add called with [5,3]
Method add returned 8

👉 এটি debugging এবং monitoring এর জন্য খুব useful।

২. Execution Time Decorator (Performance Measure)

এই decorator method কত সময় নেয় তা মাপবে।

function MeasureTime(
  target: any,
  methodName: string,
  descriptor: PropertyDescriptor
) {
  const original = descriptor.value;

  descriptor.value = function (...args: any[]) {
    const start = Date.now();

    const result = original.apply(this, args);

    const end = Date.now();
    console.log(`${methodName} took ${end - start} ms`);

    return result;
  };
}

ব্যবহার:

class DataService {

  @MeasureTime
  loadData() {
    for (let i = 0; i < 100000000; i++) {}
  }

}

new DataService().loadData();
৩. Validation Decorator

Parameter check করার জন্য decorator ব্যবহার করা যায়।

function MinLength(length: number) {
  return function (target: any, propertyKey: string) {

    let value: string;

    const getter = () => value;

    const setter = (newVal: string) => {
      if (newVal.length < length) {
        throw new Error(`${propertyKey} must be at least ${length} characters`);
      }
      value = newVal;
    };

    Object.defineProperty(target, propertyKey, {
      get: getter,
      set: setter
    });

  };
}

ব্যবহার:

class User {

  @MinLength(5)
  password: string;

}

const user = new User();
user.password = "12345"; // OK
user.password = "123";   // Error
৪. Authorization Decorator

User login আছে কিনা check করতে পারে।

function RequireLogin(
  target: any,
  methodName: string,
  descriptor: PropertyDescriptor
) {

  const original = descriptor.value;

  descriptor.value = function (...args: any[]) {

    const isLoggedIn = true;

    if (!isLoggedIn) {
      console.log("User not authorized");
      return;
    }

    return original.apply(this, args);
  };
}

ব্যবহার:

class BankService {

  @RequireLogin
  transferMoney() {
    console.log("Money transferred");
  }

}
৫. Decorators কোথায় বেশি ব্যবহার হয়

Real-world এ decorators অনেক framework-এ ব্যবহার হয়:

Angular

NestJS

TypeORM

উদাহরণ (Angular):

@Component({
  selector: 'app-user'
})

এখানে @Component একটি useful decorator।
```
## TypeScript এ Multiple Decorators মানে হলো একই class, method, property বা parameter-এর উপর একাধিক decorator ব্যবহার করা।

এতে একটি decorator অন্যটির সাথে combine হয়ে কাজ করতে পারে।

## ১. Multiple Decorator কী?
```
যখন একটি element-এর উপর একাধিক @decorator ব্যবহার করা হয়, তখন তাকে Multiple Decorators বলে।

Example:

@Decorator1
@Decorator2
class Example {}

এখানে Decorator1 এবং Decorator2 দুইটিই একই class-এর উপর কাজ করবে।

২. Simple Example
function First() {
  console.log("First decorator");
}

function Second() {
  console.log("Second decorator");
}

@First
@Second
class Test {}

Output:

Second decorator
First decorator

👉 কারণ decorators bottom → up order এ execute হয়।

৩. Method-এ Multiple Decorator
function Log(target: any, method: string) {
  console.log("Log decorator:", method);
}

function Auth(target: any, method: string) {
  console.log("Auth decorator:", method);
}

class UserService {

  @Auth
  @Log
  getUser() {
    console.log("User data");
  }

}

Output:

Log decorator: getUser
Auth decorator: getUser
৪. Decorator Factory সহ Multiple Decorator
function Logger(message: string) {
  return function (constructor: Function) {
    console.log(message);
  };
}

function Version(version: string) {
  return function (constructor: Function) {
    console.log("Version:", version);
  };
}

@Logger("Application Started")
@Version("1.0")
class App {}

Output:

Version: 1.0
Application Started
৫. Execution Order (খুব গুরুত্বপূর্ণ)

Multiple decorator থাকলে execution order দুইভাবে ঘটে।

১️⃣ Decorator Expression Evaluation

উপর থেকে নিচে

২️⃣ Decorator Function Execution

নিচ থেকে উপরে

Example:

function A() {
  console.log("A evaluated");
  return function () {
    console.log("A executed");
  };
}

function B() {
  console.log("B evaluated");
  return function () {
    console.log("B executed");
  };
}

@A()
@B()
class Demo {}

Output:

A evaluated
B evaluated
B executed
A executed
৬. বাস্তব ব্যবহার (Real Use Case)

Multiple decorators সাধারণত ব্যবহৃত হয়:

Authentication

Logging

Validation

Caching

Example:

class OrderService {

  @Auth
  @Log
  @Cache
  placeOrder() {}

}
```
