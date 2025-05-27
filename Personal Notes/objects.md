In JavaScript, the formal definition of an object is:

A collection of key-value pairs where keys (also called properties) are strings or Symbols, and values can be any valid JavaScript data type, including other objects or functions.

What is a Symbol?

A Symbol is a unique and immutable primitive value used as an identifier for object properties.

Even if two symbols have the same description, they are always different:

```Example
const sym1 = Symbol("id");
const sym2 = Symbol("id");

console.log(sym1 === sym2); // false
```

Why Use Symbols?

Symbols are useful when:

You want to create hidden or internal object properties

You need unique keys that won’t accidentally collide with other keys

You’re working with well-known symbols that control object behavior (e.g. iteration, primitive coercion)

```Example: Using a Symbol as a Key
const id = Symbol("userID");

const user = {
  name: "Alice",
  [id]: 1234 // note the square brackets to use a symbol as a key
};

console.log(user);         // { name: "Alice", [Symbol(userID)]: 1234 }
console.log(user[id]);     // 1234
console.log(Object.keys(user)); // ["name"] — symbol is hidden from typical key lookups

```

## Syntax

A simple assigment can be done.

```Sample Code
const restaurant = {
  name: 'Classico Italiano',
  location: 'Via Angelo Tavanti 23, Firenze, Italy',
  categories: ['Italian', 'Pizzeria', 'Vegetarian', 'Organic'],
  starterMenu: ['Focaccia', 'Bruschetta', 'Garlic Bread', 'Caprese Salad'],
  mainMenu: ['Pizza', 'Pasta', 'Risotto'],
  };
```

```Example 1
In the method below, we show you ways to assign the values to a varible or constant. A tick that can be applied to skip a value, is to simply provide a blank space as shown below.

const [first, second] = restaurant.categories;
const [firstBeta, , secondBeta] = restaurant.categories;
```

```Example 2
Keep in mind that when it comes to objects, there are ways to assign those using functions.

let spaceship = {
  'Fuel Type': 'Turbo Fuel',
  'Active Duty': true,
  homePlanet: 'Earth',
  numCrew: 5
};


let returnAnyProp = (objectName, propName) => objectName[propName];

returnAnyProp(spaceship, 'homePlanet'); // Returns 'Earth'
```

## Deconstucting

```Notes

To descturcture objects you have to use the curly braces


```
