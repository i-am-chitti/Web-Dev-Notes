---
tags: [JS]
title: Pure Javascript
created: '2021-05-21T08:28:00.038Z'
modified: '2021-07-30T08:49:44.141Z'
---

# Pure Javascript

Javascript: A single threaded, non-blocking, asynchronous, concurrent scripting language

JavaScript is case-sensitive and uses the Unicode character set. For example, the word Früh (which means "early" in German) could be used as a variable name.
```
const Früh = "foobar";
```

A semicolon is not necessary after a statement if it is written on its own line. But if more than one statement on a line is desired, then they must be separated by semicolons.

## Variables

A JavaScript identifier usually starts with a letter, underscore (_), or dollar sign ($). Subsequent characters can also be digits (0 – 9). Because JavaScript is case sensitive, letters include the characters A through Z (uppercase) as well as a through z (lowercase).

You can use most of ISO 8859-1 or Unicode letters such as å and ü in identifiers.

If a variable is declared without an initializer, it is assigned the value undefined.

### Variable Scope

A variable may belong to one of the following scopes:

- Global scope: The default scope for all code running in script mode.
- Module scope: The scope for code running in module mode.
- Function scope: The scope created with a function.

In addition, variables declared with let or const can belong to an additional scope:

- Block scope: The scope created with a pair of curly braces (a block).

When you declare a variable outside of any function, it is called a global variable, because it is available to any other code in the current document. When you declare a variable within a function, it is called a local variable, because it is available only within that function.

### Variable hoisting

`var`-declared variables are hoisted, meaning you can refer to the variable anywhere in its scope, even if its declaration isn't reached yet. You can see `var` declarations as being "lifted" to the top of its function or global scope. However, if you access a variable before it's declared, the value is always `undefined`, because only its declaration is hoisted, but not its initialization.

```
console.log(x === undefined); // true
var x = 3;

(function () {
  console.log(x); // undefined
  var x = "local value";
})();
```

The above example is interpreted the same as:-
```
var x;
console.log(x === undefined); // true
x = 3;

(function () {
  var x;
  console.log(x); // undefined
  x = "local value";
})();
```

Because of hoisting, all `var` statements in a function should be placed as near to the top of the function as possible. This best practice increases the clarity of the code.

Whether `let` and `const` are hoisted is a matter of definition debate. Referencing the variable in the block before the variable declaration always results in a `ReferenceError`, because the variable is in a "`temporal dead zone`" from the start of the block until the declaration is processed.
```
console.log(x); // ReferenceError
const x = 3;

console.log(y); // ReferenceError
let y = 3;
```

Unlike `var` declarations, which only hoist the declaration but not its value, function declarations are hoisted entirely — you can safely call the function anywhere in its scope. See the hoisting glossary entry for more discussion.

### Global Variables
In web pages, the global object is window, so you can set and access global variables using the window.variable syntax. In all environments, you can use the globalThis variable (which itself is a global variable) to access global variables.

Consequently, you can access global variables declared in one window or frame from another window or frame by specifying the window or frame name. For example, if a variable called `phoneNumber` is declared in a document, you can refer to this variable from an iframe as `parent.phoneNumber`.

### Constants
A constant cannot change value through assignment or be re-declared while the script is running. It must be initialized to a value.

You cannot declare a constant with the same name as a function or variable in the same scope. For example:

## Datatypes

* Number
* String
* Boolean
* Symbol
* Object
  * Function
  * Array
  * Data
  * RegExp
* null
* undefined

__NOTE__: A special value called NaN (short for "Not a Number") is returned if the string is non-numeric:

NaN is toxic: if you provide it as an operand to any mathematical operation, the result will also be NaN:

```NaN + 5; //NaN```

There are 7 datatypes -
Primitive - number, string, boolean, null, undefined, symbol
Object - Array, Functions, object

__Revise Javascript__ [Here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#other_types)

Javascript does implicit conversion.

```
const num1 = 'Joh';
const num2 = 'Hello';
console.log(num1 - num2); // NaN

const num3 = '10';
const num4 = '20';
console.log(num3-num4) // '-10'

console.log(num3+num4) // '1020'

console.log(20+'23') // 2023
```

For input of type number, in JS, its value will be string. From HTML, it comes as string. We need to do explicit conversion with `parseInt`.

```
console.log(typeof null); //object
```

## Functions

Every JS function is actually a function object. Thus, like objects, functions also have properties and methods.

For example:

```
const myFun = () => { console.log('I am a function'); }
console.log(myFun.name);  // myFun
const auxName = myFun;
console.log(auxName.name);  // myFun
```

Other properties are _.length_, and methods are _.toString()_ etc

### Higher order functions

**Higher order Function** are those function which either accepts a function as argument or returns a function or both.

```
const timeFuncRuntime = funcParameter => {
   let t1 = Date.now();
   funcParameter();
   let t2 = Date.now();
   return t2 - t1;
}

const addOneToOne = () => 1 + 1;

timeFuncRuntime(addOneToOne);
```
* Anonymous functions can also be argument

___

## Iterators

1. ```.forEach()```
    * It accepts a callback function as argument.
    * It loops through the array and executes the callback function for each element.
    * The return value will always be ```undefined```

    ```
    const fruits = ['mango', 'papaya', 'pineapple', 'apple'];

    // Iterate over fruits below
    fruits.forEach((fruit) => {
      console.log(`I want to eat a ${fruit}`);
    });
    ```

2. ```.map()```
    * works similar to ```.forEach()``` but it returns a new array

    ```
    const bigNumbers = [100, 200, 300, 400, 500];
    const smallNumbers = bigNumbers.map((bigNumber) => bigNumber/100);
    console.log(smallNumbers);
    ```

3. ```.filter()```
    * similar to ```.map()``` but return a new array filtering it based on callback function.
    * accepts a callback function that must return either true or false for each value

    ```
    const randomNumbers = [375, 200, 3.14, 7, 13, 852];
    const smallNumbers = randomNumbers.filter((number) => number<250);
    ```

4. ```.findIndex()```
    * It will return the index of the first element that evaluates to true in the callback function

    ```
    const jumbledNums = [123, 25, 78, 5, 9];
    const lessThanTen = jumbledNums.findIndex(num => {
      return num < 10;
    });
    ```

5. ```.reduce()```
    * returns a single value after iterating through the array. Thus, reducing the array
    * Its callback function takes two arguments, one ```accumulator``` and other ```currentValue```
    * The value of accumulator starts off as the value of the first element in the array and the currentValue starts as the second element.
    * Finally it returns the accumulator value.
    - Apart from a callback function, It also takes an optional second parameter to set an initial value for accumulator.

    ```
    const numbers = [1, 2, 4, 10];
    const summedNums = numbers.reduce((accumulator, currentValue) => {
      return accumulator + currentValue
    }, 100)  // <- Second argument for .reduce(), if not provided accumulator will be the first value in array

    console.log(summedNums); // Output: 117
    ```

6. ```.some()```
    * It tests whether at least one element is present in array that passes the callback function.
    ```
    const array = [1, 2, 3, 4, 5];
    // checks whether an element is even
    const even = (element) => element % 2 === 0;
    console.log(array.some(even));
    // expected output: true

    ```

7. ```.every()```
    * Like ```.some()```, it checks the condition for every element. It evaluates true if and only if all element passed the callback test, else false.

    ```
    console.log(interestingWords.every((word) => word.length>5 ));
    // if interesting words are of greater than 5 character length
    ```

    [MDN's Iterator Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Iteration_methods)


___

## Errors & Debugging

* Here are three common types of errors:
1. SyntaxError: This error will be thrown when a typo creates invalid code — code that cannot be interpreted by the compiler.
2. Reference Error: This error will be thrown if you try to use a variable that does not exist.
3. TypeError: This error will be thrown if you attempt to perform an operation on a value of the wrong type.

* Handling Errors
There are two important parts of an error that are name and its message.
```
console.log(Error('User name invalid));
console.log(new Error('User name invalid));
// both are correct with and without new keyword
console.log("This will be executed as program execution doesn't halts");
```
Creating new error doesn't halts our program but once any error is thrown, our program is halted.

Throwing an error
```
throw Error('Something wrong happened');
// Error: Something wrong happened

console.log('This will never run');
```

If an error was thrown and caught, then program execution will continue.
```
try {
  throw Error('This error will get caught');
} catch (e) {
  console.log(e);
}
// Prints: This error will get caught

console.log('The thrown error that was caught in the try...catch statement!');
// Prints: 'The thrown error that was caught in the try...catch statement!'
```

### Destructuring arrays and objects

Destructuring array
```
// lenthy code
let cars = ['ferrari', 'tesla', 'cadillac'];
let car1 = cars[0];
let car2 = cars[1];
let car3 = cars[2];
console.log(car1, car2, car3); // Prints: ferrari tesla cadillac

// more easy to understand and write
let cars = ['ferrari', 'tesla', 'cadillac'];
let [car1, car2, car3] = cars;
console.log(car1, car2, car3); // Prints: ferrari tesla cadillac
```

Destructuring objects
```
let destinations = { x: 'LA', y: 'NYC', z: 'MIA' };
let x = destinations.x;
let y = destinations.y;
let z = destinations.z;
console.log(x, y, z); // Prints LA NYC MIA

// more easy to understand
let destinations = { x: 'LA', y: 'NYC', z: 'MIA' };
let { x, y, z } = destinations;
console.log(x, y, z); // Prints LA NYC MIA
```


## `this` keyword

The value of `this` depends on in which context it appears: function, class, or global.


## Closure

A closure is the combination of a function and the lexical environment within which that function was declared. This environment consists of any local variables that were in-scope at the time the closure was created. In this case, `myFunc` is a reference to the instance of the function displayName that is created when `makeFunc` is run. The instance of `displayName` maintains a reference to its lexical environment, within which the variable name exists. For this reason, when `myFunc` is invoked, the variable `name` remains available for use, and "Mozilla" is passed to `console.log`.

```
function makeFunc() {
  const name = "Mozilla";
  function displayName() {
    console.log(name);
  }
  return displayName;
}

const myFunc = makeFunc();
myFunc();
```

Every closure has three scopes:

- Local scope (Own scope)
- Enclosing scope (can be block, function, or module scope)
- Global scope


### Value vs Reference

When assigning primitive data type value to a variable, any changes are made directly to that value without affecting the original value.

When assigning non-primitive data type ot a variable value to a variable, it is done by reference so any changes will affect all the references.

### Truthy vs falsy

"", '', ``, 0 ,-0, null, undefined, NaN, false are evaluated as falsy.


### Variable Lookup

A variable is first looked up in the local scope (`{}`), then, in global scope.


### Math
 It is a standard built-in object always available.

 ```
 const number = 93.1938;
 console.log(Math.floor(number)); // 93
 console.log(Math.ceil(number)); // 94
 ```

### currentTarget vs target

`currentTarget` - always refers to the element to which event listener has been attached to

`target` - identifies the element on which the event has occurred.
