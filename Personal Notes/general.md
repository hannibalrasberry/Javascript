# This

In JavaScript, the this keyword refers to the object that is executing the current function. Its value depends on where and how the function is called.

The value of this changes based on how a function is invoked.

## 1. Global Context (this in the Global Scope)

In the global execution context (outside of any function), this refers to:

    - window object in browsers.
    - global This or global in Node.js.

```Example:

console.log(this);
// In a browser: Window {...}
// In Node.js: global {...}
```

## 2. this Inside an Object Method

When this is used inside an object's method, it refers to the object that owns the method.

```Example: javascript

const person = {
  name: 'Alice',
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
  };
```

person.greet(); // Output: Hello, my name is Alice //Ouput: Hello, my name is Alice

✅ Here, this.name refers to person.name because this refers to the person object.

## 3. this in a Regular Function (Default Behavior)

When a regular function (not an object method) is called, this defaults to:

    - undefined in strict mode ('use strict')
    - window in brosers (non-strict mode)
    - global in Node.js (non-strict mode)

```
Example:

function showThis(){
    console.log(this);
}

showThis(); //In strict mode: undefined | in non strict mode: Window {...}
```

common mistake: If a function inside an object is not called as a method, this is not bound to the object !

```
Example :
const person = {
    name: 'Alice',
    greet(){
        function sayHi(){
            console.log(this.name); //this is NOT bound to 'person'
        }
        sayHi();
    }
};

```

The this inside sayHi() refers to the global object (window/globalThis), not person.

Solution: Use an arrow function (explained in rule #5 ) or .bind()(explained in rule #7)

## 4. this in Constructor Functions

When using a constructor function (with new), this refers to the newly created object.

```
Example :

function Person (name){
    this.name = name;
}

const user = new Person ('Bob');
console.log(user.name); //Output: Bob
```

Here, this.name = name assigns the value to the new user object.

## 5. this in Arrow Functions

Arrow functions do NOT have their ownthis. Instead, they inherit this from their surrounding scopt.

```
const person = {
    name: 'Alice',
    greet: function(){
        const sayHi = () => {
            console.log('Hello, my name is ${this.name});
        };
        sayHi();
    }
};

person.greet(); //Output: Helo, my name is Alice
```

Here, this.name works because arrow functions inherit this from their parent scope (greet), which refers to person.

Use arrow functions to avoid this confusion!

## 6. this in Event Listeners

In an event listener, this refers to the element that received the event.

```
document.querySelector('button').addEventListener('click', function({
    console.log(this); //Refers to the clicked button element
}));
```

If you use an arrow function, this will refer to the surrounding scope, not the element:

```
document.querySelector('button').addEventListener('click', ( => {
    console.log(this); //Likely 'window' (not the button!)
}));
```

Use refular functions if you need this to refer to the clicked element.

## 7. Manually Controlling this with .bind(), .call(), and .apply()

Sometimes, you need to explicitly set the value of this.

Using .bind()

    - Permanently binds this to a specific object.

```
const person = {
    name: 'Alice',
};

function greet(){
    console.log('Hello, name is ${this.name}');
}

const boundGreet = greet.bind(person);
boundGreet(); //Output: Hello, my name is Alice
```

Using .call() and .apply() - Calls the function immediately, setting this to the provided object

```
greet.call(person); //Output: Hello, my name is Alice
greet.apply(person); //Output: Hello, my name is Alice
```

Difference between call and apply :

    - .call(thisArg, arg1, arg2, ...) -> Pass arguments separately
    - .apply(thisArg, [arg1, arg2, ...]) -> Pass argument as an array

    Quick Summary of this Behavior

    - Context               - this refers to....
    Global Scope                Window (browser) or globalThis (Node.js)
    Inside Object Method        The object thatwns the method
    Regular Function            undefined in strict mode. window/globalThis otherwise
    Constructor Function        The newly ceated object (new keyword)
    Arrow Function              this from surrounding scope (lexical this)
    Event Listener              The element that received the event (this is the clicked element)
    .bind(), .call(),           Alows manual setting of this
    .apply()

    Final Tips

    - Use arrow functions when you want this to inherit from the surrounding scope.
    - Use .bind() wehn you need to ensure this refers to a specific object
    - Use call() or apply() when you need to invoke function immediately with a specific this value
    - In event listeners, use a regular function if you need this to refer to the target element
