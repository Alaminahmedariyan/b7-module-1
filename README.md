# Module 1 — TypeScript এর মূল ধারণাগুলো

এই রিপোজিটরিতে TypeScript-এর মৌলিক বিষয়গুলো বাংলায় ব্যাখ্যা করা হয়েছে। প্রতিটি topic-এ real-life use case এবং code example দেওয়া আছে।

---

## সব topic এক নজরে

| Topic | Keyword | কাজ |
|---|---|---|
| Primitive Types | `string`, `number`, `boolean` | Basic একক value রাখা |
| Non-Primitive Types | `array`, `object`, `tuple` | একাধিক value রাখা |
| Literal Type | `"left" \| "right"` | শুধু নির্দিষ্ট value allow করা |
| Optional Type | `?` | না দিলেও চলবে এমন property |
| Function | `param: type): returnType` | Input-output নিশ্চিত করা |
| Rest Operator | `...args` | অনেক argument একসাথে নেওয়া |
| Spread Operator | `...array` | array বা object ছড়িয়ে দেওয়া |
| Destructuring | `const { name } = user` | সরাসরি value বের করা |
| Type Alias | `type User = {...}` | Type-কে একটা নাম দেওয়া |
| Union Type | `string \| number` | যেকোনো একটি type হতে পারে |
| Intersection Type | `Person & Worker` | দুটো type একসাথে মেলানো |
| Ternary | `condition ? a : b` | এক লাইনে if-else |
| Nullish Coalescing | `??` | null হলে default value দেওয়া |
| Optional Chaining | `?.` | crash ছাড়া nested property access |
| Nullable | `string \| null` | null allow করা |
| Unknown | `unknown` | নিরাপদ any বিকল্প |
| Never | `never` | কখনো return করে না এমন function |

---

## Topic গুলো বিস্তারিত

### 1-4 Primitive Types
TypeScript-এর সবচেয়ে basic type গুলো — `string`, `number`, `boolean`, `null`, `undefined`।

```typescript
let name: string = "Rahim";
let age: number = 25;
let isActive: boolean = true;
```

---

### 1-5 Non-Primitive Types
একাধিক value ধরতে পারে এমন type — `array`, `object`, `tuple`।

```typescript
let marks: number[] = [80, 90, 75];
let student: { name: string; age: number } = { name: "Karim", age: 20 };
let profile: [string, number] = ["Rahim", 25];
```

---

### 1-6 Object, Literal & Optional Type
Object-এর shape নির্ধারণ, শুধু নির্দিষ্ট value allow করা এবং optional property রাখা।

```typescript
let direction: "left" | "right" | "center" = "left";
let person: { name: string; phone?: string } = { name: "Jamal" };
```

---

### 1-7 Function
Parameter-এর type এবং return type বলে দিলে ভুল call করলে আগেই error পাওয়া যায়।

```typescript
function add(a: number, b: number): number {
  return a + b;
}
```

---

### 1-8 Rest & Spread Operator
Rest দিয়ে অনেক argument একটি array-তে নেওয়া যায়। Spread দিয়ে array বা object ছড়িয়ে দেওয়া যায়।

```typescript
function sumAll(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

const allFood = [...fruits, ...veggies];
```

---

### 1-9 Destructuring
Object বা array থেকে সরাসরি নির্দিষ্ট value বের করে নেওয়া।

```typescript
const { name, age } = user;
const [first, second] = colors;
```

---

### 1-10 Type Alias
বারবার একই type না লিখে একবার নাম দিয়ে রাখা।

```typescript
type User = { name: string; age: number; email: string };
type Status = "active" | "inactive" | "pending";
```

---

### 1-11 Union & Intersection Types
Union — দুটির মধ্যে যেকোনো একটি। Intersection — দুটো type একসাথে।

```typescript
type ID = string | number;
type Employee = Person & Worker;
```

---

### 1-12 Ternary, Nullish Coalescing & Optional Chaining
তিনটি shortcut operator যা কোড ছোট এবং নিরাপদ রাখে।

```typescript
const message = age >= 18 ? "Adult" : "Minor";
const displayName = nickname ?? "Anonymous";
const city = user?.address?.city;
```

---

### 1-13 Nullable, Unknown & Never Type
- **Nullable** — `null` বা `undefined` allow করা  
- **Unknown** — ব্যবহারের আগে type check করতে হয়  
- **Never** — কখনো return করে না এমন function  

```typescript
let username: string | null = null;
let input: unknown = "Hello";
function throwError(msg: string): never { throw new Error(msg); }
```

---

## কোড চালানোর নিয়ম

```bash
npx ts-node index.ts
```