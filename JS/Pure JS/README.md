---
tags: [JS]
title: Pure Javascript
created: '2021-05-21T08:28:00.038Z'
modified: '2021-07-30T08:49:44.141Z'
---

# Pure Javascript

Javascript: A single threaded, non-blocking, asynchronous, concurrent scripting language

## Datatypes

* Number
* BigInt
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

__Revise Javascript__ [Here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#other_types)

## Functions

### Higher order functions

Every JS function is actually a function object. Thus, like objects, functions also have properties and methods.

For example:

```
const myFun = () => { console.log('I am a function'); }
console.log(myFun.name);  // myFun
const auxName = myFun;
console.log(auxName.name);  // myFun
```

Other properties are _.length_, and methods are _.toString()_ etc

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
1. SyntaxError: This error will be thrown when a typo creates invalid code ??? code that cannot be interpreted by the compiler.
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
