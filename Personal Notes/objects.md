In JavaScript, the formal definition of an object is:

A collection of key-value pairs where keys (also called properties) are strings or Symbols, and values can be any valid JavaScript data type, including other objects or functions.

# What is a Symbol?

A Symbol is a unique and immutable primitive value used as an identifier for object properties.

Even if two symbols have the same description, they are always different:

```Example
const sym1 = Symbol("id");
const sym2 = Symbol("id");

console.log(sym1 === sym2); // false
```

Something to kep in mind. **Symbol** is not a type fo keyword like bool, int, string, or var in languages you see in C++ or Java.

Instead, **Symbol** in Javascript is a function that returns a primitive value of a new symbol type

```🔹 What is a primitive value ?

In JavaSript, a primitive value is a data type thats not an object and has no methods.

It is immutable and represents a single, raw value.

Primitive values are stored by value, not by reference.

There are 7 Primitive Data Types in JavaScript
1. string
2. number
3. bigint
4. boolean
5. undefined
6. null
7. symbol

⁉️ Characteristics of Primitives

*Feature                      *Description

Immutable                     You can not change the value (You can only replace it)
Not Objects                   No properties or methods(though they can
                              appear to  have  them temporarily)
Copied by value               When assigned or passed to a function,
                              a copy of the value is used

🔹 Primitives vs Objects

let a = 5;
let b = a;
b = 10;
console.log(a); // 5 — primitive copied by value

But with an object:

let obj1 = { x: 5 };
let obj2 = obj1;
obj2.x = 10;
console.log(obj1.x); // 10 — object copied by reference

👁 Keep in Mind

Objects don't pass copies of values in Javascript.

- In the example mentioned above obj1 holds a refernce to an objecct {x: 5}
- So when you assign obj2 = obj, you're not creating a new object. No what you're doing is copying a reference point
- Both obj1 and obj2 now point to the exact smae object in memory
- So when you change obj2.x = 10, you're modifying the object itself, and that change is visible in both values

🔹 Important Concept
- Objects, arrays, and functions in JavaScript are stored by reference.
- When you assign one to another variable, you're copying the reference, not cloning the data.
- Only primitive values (string, number, boolean, etc.) are stored by value (i.e., fully copied).

🔹 If You Want to Copy the Object Instead
To make a true copy, you need to clone the object:

let obj1 = { x: 5 };
let obj2 = { ...obj1 }; // spread syntax
obj2.x = 10;
console.log(obj1.x); // 5


```

```🔹 So what is Symbol exactly?

A Symbol is a unique and immutable( Remember a immutable value is a value that can only have its value replaced never changed. Reference the earlier lines for a deeper explnation.The quick summation of it is that the value must be directly reassigned) primative value used as an identifier for object properties.

Even if two symbols have the same description, they are always different

const sym1 = Symbol("id");
const sym2 = Symbol("id");

console.log(sym1 === sym2) // false

```

```🔹 Why Use Symbols?

Symbols are useful when:

1. You want to create hidden or internal object properties

2. You need unique keys that won’t accidentally collide with other keys

3. You’re working with well-known symbols that control object behavior (e.g. iteration, primitive coercion)

Example: Using a Symbol as a Key

const id = Symbol("userID");

const user = {
  name: "Alice",
  [id]: 1234 // note the square brackets to use a symbol as a key
};

console.log(user);         // { name: "Alice", [Symbol(userID)]: 1234 }
console.log(user[id]);     // 1234
console.log(Object.keys(user)); // ["name"] — symbol is hidden from typical key lookups

```

```🔹 Symbols Are Not Enumerated

Unlike string keys, symbol keys don’t appear in:

Object.keys(obj)

for...in loops

JSON.stringify(obj)

To get them, you use:

Object.getOwnPropertySymbols(user); // [Symbol(userID)]
```

```🔹 If you wish to copy a Object only by value

let obj1 = { x: 5 };
let obj2 = { ...obj1 }; // spread syntax
obj2.x = 10;
console.log(obj1.x); // 5

using the spread syntax will copy the value only to the object and separate the values.
As it stand the spread method is most common and readable.

Here's a key distinction :
    Destructuring pulls values out of an object.
    Spread Syntax copies the whole object into a new one.

Using Object.assign() (older method):
jconst obj1 = { a: 1, b: 2 };
const obj2 = Object.assign({}, obj1);

⚠️ Destructuring Doesn't Clone — But It Can Extract
const obj1 = { a: 1, b: 2 };
const { a, b } = obj1;

console.log(a); // 1
console.log(b); // 2

You're not creating a new object — you're extracting values into separate variables.
This doesn't clone the original object.

🔹 When You Actually Want to Clone
Goal                                Use

Copy entire object                  { ...obj } or Object.assign()
Copy nested objects	                Use deep copy (see below)
Extract values only	                Object destructuring


🔹 Shallow vs Deep Copy
Most methods (like spread or Object.assign) only make shallow copies:

const obj1 = { a: 1, nested: { x: 10 } };
const obj2 = { ...obj1 };

obj2.nested.x = 99;
console.log(obj1.nested.x); // 99 — still shared reference!


To make a deep copy, you need:

1. structuredClone() (modern and safe):
            const obj2 = structuredClone(obj1);

2. JSON.parse(JSON.stringify(obj)) (not recommended for all cases):
              const obj2 = JSON.parse(JSON.stringify(obj1));
              // fails on functions, Dates, Symbols, etc.

✅ Summary
    Method                   Clones?         Notes

const { a } = obj                 ❌          Destructures (extracts), not clones
{ ...obj }                        ✅          Shallow clone                              Object.assign({}, obj)`           ✅          Shallow clone                              structuredClone(obj)`             ✅✅        Deep clone (best for nested objects)
JSON.parse(JSON.stringify(obj))`  ✅          Deep clone, but lossy (no functions, etc.)





```
