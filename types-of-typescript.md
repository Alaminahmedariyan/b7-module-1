# Module 1 — TypeScript এর মূল ধারণাগুলো

> সব topic বাংলায় ব্যাখ্যা করা হয়েছে। Code example গুলো English-এ।

---

## 1-4 Primitive Types

### এটা কী?

TypeScript-এ সবচেয়ে basic data type গুলোকে **Primitive Type** বলে।
এগুলো হলো: `string`, `number`, `boolean`, `null`, `undefined`।

Variable declare করার সময় type বলে দিলে TypeScript ভুল ধরতে পারে।

### Use Case

কোনো user-এর নাম, বয়স, বা active কিনা — এই তথ্যগুলো store করতে primitive type ব্যবহার হয়।

### Example

```typescript
let name: string = "Rahim";
let age: number = 25;
let isActive: boolean = true;
let phone: null = null;
let address: undefined = undefined;

// ভুল করলে TypeScript সাথে সাথে error দেবে
let city: string = 100; // ❌ Error: number কে string-এ দেওয়া যাবে না
```

---

## 1-5 Non-Primitive Types

### এটা কী?

**Non-Primitive Type** মানে যেগুলো একাধিক value ধরতে পারে।
এগুলো হলো: `array`, `object`, `tuple`।

### Use Case

একজন student-এর marks list বা একটি product-এর তথ্য রাখতে non-primitive type ব্যবহার হয়।

### Example

```typescript
// Array — একই type-এর অনেক value
let marks: number[] = [80, 90, 75, 88];
let cities: string[] = ["Dhaka", "Chittagong", "Sylhet"];

// Object — key-value pair
let student: { name: string; age: number } = {
  name: "Karim",
  age: 20,
};

// Tuple — নির্দিষ্ট সংখ্যক এবং নির্দিষ্ট type-এর value
let coordinate: [number, number] = [23.8, 90.4]; // latitude, longitude
let profile: [string, number] = ["Rahim", 25];
```

---

## 1-6 Object, Literal & Optional Type

### এটা কী?

**Object Type** — object-এর shape বলে দেওয়া।
**Literal Type** — শুধু নির্দিষ্ট কিছু value allow করা।
**Optional Type** — কোনো property না দিলেও চলবে (? দিয়ে বোঝানো হয়)।

### Use Case

কোনো button-এর color শুধু নির্দিষ্ট কিছু হবে। অথবা user registration form-এ phone number optional রাখতে চাই।

### Example

```typescript
// Object Type
let user: { name: string; age: number } = {
  name: "Salam",
  age: 30,
};

// Literal Type — শুধু এই তিনটি value-ই দেওয়া যাবে
let direction: "left" | "right" | "center" = "left";
let status: "active" | "inactive" = "active";

direction = "up"; // ❌ Error: "up" allowed না

// Optional Type — phone দেওয়া না দেওয়া দুটোই চলবে
let person: { name: string; age: number; phone?: string } = {
  name: "Jamal",
  age: 22,
  // phone না দিলেও error হবে না
};

// Button size — literal type দিয়ে
type ButtonSize = "small" | "medium" | "large";
let btn: ButtonSize = "medium"; // ✅
```

---

## 1-7 Function in TypeScript

### এটা কী?

TypeScript-এ function লেখার সময় **parameter-এর type** এবং **return type** বলে দিতে হয়।
এতে function ভুল ভাবে call করলে আগেই error পাওয়া যায়।

### Use Case

দুটি সংখ্যা যোগ করার function, অথবা user-এর নাম থেকে greeting message বানানোর function।

### Example

```typescript
// Basic function — parameter এবং return type দেওয়া
function add(a: number, b: number): number {
  return a + b;
}

add(5, 10);   // ✅ returns 15
add(5, "10"); // ❌ Error: string দেওয়া যাবে না

// Return type void — কিছু return করে না
function greet(name: string): void {
  console.log("Hello, " + name);
}

// Arrow function
const multiply = (a: number, b: number): number => a * b;

// Optional parameter
function createUser(name: string, age?: number): string {
  if (age) {
    return `${name}, age ${age}`;
  }
  return name;
}

createUser("Rahim");       // ✅
createUser("Rahim", 25);   // ✅
```

---

## 1-8 Rest & Spread Operator

### এটা কী?

**Rest Operator (`...`)** — অনেকগুলো argument একটি array-তে নিয়ে নেয়।
**Spread Operator (`...`)** — array বা object-কে ছড়িয়ে দেয়।

দেখতে একই (`...`) কিন্তু কাজ আলাদা।

### Use Case

- Rest: কতগুলো সংখ্যা যোগ করতে হবে আগে থেকে জানা নেই।
- Spread: দুটো array মেলাতে বা object copy করতে।

### Example

```typescript
// Rest Operator — যত খুশি argument দেওয়া যাবে
function sumAll(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

sumAll(1, 2, 3);          // 6
sumAll(10, 20, 30, 40);   // 100

// Spread Operator — array মেলানো
const fruits = ["apple", "banana"];
const veggies = ["carrot", "potato"];
const allFood = [...fruits, ...veggies];
// ["apple", "banana", "carrot", "potato"]

// Spread Operator — object copy এবং নতুন property যোগ
const user = { name: "Rahim", age: 25 };
const updatedUser = { ...user, city: "Dhaka" };
// { name: "Rahim", age: 25, city: "Dhaka" }

// Original object পরিবর্তন হয় না
console.log(user); // { name: "Rahim", age: 25 }
```

---

## 1-9 Destructuring in TypeScript

### এটা কী?

**Destructuring** মানে object বা array থেকে সরাসরি নির্দিষ্ট value বের করে নেওয়া।
বারবার `user.name`, `user.age` লেখার বদলে একবারেই বের করা যায়।

### Use Case

API থেকে data আসলে সেখান থেকে দরকারি field গুলো সরাসরি বের করে নেওয়া।

### Example

```typescript
// Object Destructuring
const user = { name: "Salam", age: 28, city: "Dhaka" };

// আগের পদ্ধতি (পুরনো)
const name1 = user.name;
const age1 = user.age;

// Destructuring (নতুন পদ্ধতি)
const { name, age, city } = user;
console.log(name); // "Salam"
console.log(age);  // 28

// Default value সহ destructuring
const { name: userName, role = "user" } = user;
// role না থাকলে "user" হবে

// Array Destructuring
const colors = ["red", "green", "blue"];
const [first, second] = colors;
console.log(first);  // "red"
console.log(second); // "green"

// Function parameter-এ destructuring
function showUser({ name, age }: { name: string; age: number }): void {
  console.log(`${name} is ${age} years old`);
}

showUser(user); // "Salam is 28 years old"
```

---

## 1-10 Type Alias

### এটা কী?

**Type Alias** মানে কোনো type-কে একটা নাম দেওয়া যাতে বারবার একই জিনিস লিখতে না হয়।
`type` keyword দিয়ে এটা করা হয়।

### Use Case

`{ name: string; age: number; email: string }` বারবার লেখার বদলে একবার `User` নামে define করে রাখা।

### Example

```typescript
// Type Alias ছাড়া — বারবার লিখতে হচ্ছে
function getUser(): { name: string; age: number } {
  return { name: "Rahim", age: 25 };
}

function saveUser(user: { name: string; age: number }): void {
  console.log(user);
}

// Type Alias দিয়ে — একবার লিখলেই হয়
type User = {
  name: string;
  age: number;
  email: string;
};

function getUser2(): User {
  return { name: "Rahim", age: 25, email: "rahim@gmail.com" };
}

function saveUser2(user: User): void {
  console.log(user);
}

// Simple type-এও alias ব্যবহার হয়
type ID = string | number;
type Status = "active" | "inactive" | "pending";

let userId: ID = 101;
let userStatus: Status = "active";
```

---

## 1-11 Union & Intersection Types

### এটা কী?

**Union Type (`|`)** — দুটির মধ্যে যেকোনো একটি type হতে পারে।
**Intersection Type (`&`)** — দুটি type একসাথে মিলিয়ে নতুন type বানানো।

### Use Case

- Union: ID হয় string অথবা number হতে পারে।
- Intersection: Employee হলো একই সাথে Person এবং Worker।

### Example

```typescript
// Union Type — string অথবা number
type ID = string | number;

let userId: ID = 101;      // ✅
let userId2: ID = "U-101"; // ✅
let userId3: ID = true;    // ❌ Error

// Union Type — function-এ
function printId(id: string | number): void {
  if (typeof id === "string") {
    console.log("String ID: " + id.toUpperCase());
  } else {
    console.log("Number ID: " + id);
  }
}

// Intersection Type — দুটো type একসাথে
type Person = {
  name: string;
  age: number;
};

type Worker = {
  company: string;
  salary: number;
};

// Employee-কে Person এবং Worker দুটোই হতে হবে
type Employee = Person & Worker;

const emp: Employee = {
  name: "Karim",
  age: 30,
  company: "TechBD",
  salary: 50000,
};
// সব property দিতে হবে, একটাও বাদ দেওয়া যাবে না
```

---

## 1-12 Ternary, Nullish Coalescing & Optional Chaining

### এটা কী?

তিনটি আলাদা shortcut operator:

- **Ternary (`? :`)** — if-else কে এক লাইনে লেখা।
- **Nullish Coalescing (`??`)** — `null` বা `undefined` হলে default value দেওয়া।
- **Optional Chaining (`?.`)** — object-এর property access করার সময় crash না করা।

### Use Case

- Ternary: user logged in কিনা দেখে message দেখানো।
- `??`: user-এর nickname না থাকলে নাম দেখানো।
- `?.`: API response-এ কোনো nested data না থাকলে error না হওয়া।

### Example

```typescript
// Ternary Operator
const age = 20;
const message = age >= 18 ? "Adult" : "Minor";
console.log(message); // "Adult"

// if-else দিয়ে একই কাজ (লম্বা পদ্ধতি)
let msg;
if (age >= 18) {
  msg = "Adult";
} else {
  msg = "Minor";
}

// Nullish Coalescing (??)
// null বা undefined হলে ডান পাশেরটা নেবে
const nickname = null;
const displayName = nickname ?? "Anonymous";
console.log(displayName); // "Anonymous"

const score = 0;
const finalScore = score ?? 10;
console.log(finalScore); // 0 — কারণ 0 null/undefined না

// Optional Chaining (?.)
const user = {
  name: "Rahim",
  address: {
    city: "Dhaka",
  },
};

// address না থাকলে crash করবে না, undefined দেবে
console.log(user?.address?.city);    // "Dhaka"
console.log(user?.phone?.number);    // undefined (error না)

// Array-তেও optional chaining
const users = null;
console.log(users?.[0]?.name); // undefined (error না)
```

---

## 1-13 Nullable, Unknown & Never Type

### এটা কী?

- **Nullable** — কোনো variable-এ `null` বা `undefined` allow করা।
- **Unknown** — type জানা নেই, ব্যবহার করার আগে check করতে হবে।
- **Never** — এই type-এর কোনো value হতেই পারে না (function কখনো শেষ হয় না বা সবসময় error দেয়)।

### Use Case

- Nullable: database থেকে data না পেলে null।
- Unknown: বাইরে থেকে আসা data যার type নিশ্চিত না।
- Never: এমন function যেটা সবসময় error throw করে।

### Example

```typescript
// Nullable — null বা undefined allow করা
let username: string | null = "Rahim";
username = null; // ✅ এখন null দেওয়া যাবে

// strictNullChecks on থাকলে এটা error হবে:
let name: string = null; // ❌

// Unknown — any-এর নিরাপদ বিকল্প
let input: unknown = "Hello";
input = 42;    // ✅
input = true;  // ✅

// Unknown ব্যবহার করার আগে type check করতে হবে
if (typeof input === "string") {
  console.log(input.toUpperCase()); // ✅ নিরাপদ
}

// any দিলে check ছাড়াই চলত — কিন্তু সেটা বিপজ্জনক
let data: any = "test";
data.toUpperCase(); // ✅ কিন্তু runtime-এ crash করতে পারে

// Never — কখনো return করে না
function throwError(message: string): never {
  throw new Error(message);
}

// Infinite loop — কখনো শেষ হয় না
function runForever(): never {
  while (true) {
    // চলতেই থাকবে
  }
}

// Exhaustive check-এ never ব্যবহার
type Shape = "circle" | "square";

function getArea(shape: Shape): number {
  if (shape === "circle") return 3.14;
  if (shape === "square") return 1;
  
  // এখানে পৌঁছানো কখনো সম্ভব না
  const _check: never = shape;
  return _check;
}
```

---

## সব topic এক নজরে

| Topic | Keyword | কাজ |
|---|---|---|
| Primitive Types | `string`, `number`, `boolean` | Basic একক value |
| Non-Primitive Types | `array`, `object`, `tuple` | একাধিক value |
| Literal Type | `"left" \| "right"` | নির্দিষ্ট value-ই শুধু |
| Optional Type | `?` | না দিলেও চলবে |
| Function | `param: type): returnType` | Input-output নিশ্চিত |
| Rest | `...args` | অনেক argument একসাথে |
| Spread | `...array` | ছড়িয়ে দেওয়া |
| Destructuring | `const { name } = user` | সরাসরি বের করা |
| Type Alias | `type User = {...}` | Type-কে নাম দেওয়া |
| Union | `string \| number` | যেকোনো একটি |
| Intersection | `Person & Worker` | দুটো একসাথে |
| Ternary | `condition ? a : b` | এক লাইনে if-else |
| Nullish Coalescing | `??` | null হলে default |
| Optional Chaining | `?.` | crash ছাড়া access |
| Nullable | `string \| null` | null allow করা |
| Unknown | `unknown` | নিরাপদ any |
| Never | `never` | কখনো return করে না |