
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
