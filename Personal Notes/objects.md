When you are Deconstructing an array, or object. It is rather easy to pull the data from it.

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
