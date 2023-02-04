---
title: Testing
created: '2021-06-29T12:10:28.035Z'
modified: '2021-07-20T06:21:00.100Z'
---

# Testing

__Software testing__ is the process of assessing the completeness and quality of computer software. Usually this is done by running a part of a system (like a web application) and comparing the actual behavior to the expected behavior.

__Manual testing__ is a form of testing done by a human interacting with a system. With web apps, this might be clicking, dragging, and typing through a webpage. A list of actions and expected behaviors would be given. If the observed behavior doesn’t match the expected behavior, the application has an error.

__Automated testing__ is the use of software to control the execution of tests and the comparison of actual behavior to expected behavior. 

__Compared to manual testing, automated testing is__
* Faster: it tests more of your product in less time.
* More reliable: it’s less prone to error than a human is .
* Maintainable: you can review, edit, and extend a collection of tests.

A __bug__ is an error, fault, or flaw in software that makes a system behave in unexpected ways.


Rather than hire a testing team at the end of development, professional developers can run their automated tests after every change. The workflow might look like this:

1. Write code and corresponding tests
2. Enter a command into a terminal to run tests
3. If the app behaves as intended, all tests should pass. Development is complete.
4. If it does not behave as intended, at least one test should fail. Fix code and return to step 2.

## Test Suite

Tests are written with code, just like the rest of your web app. You can refer to the code defining your app as implementation code, and the code defining your tests as test code.

__A collection of tests for a web application is called a test suite.__

__Test code is included with and structured similarly to implementation code__. Often times changes to test code are associated with changes to implementation code and vice versa. Both are easier to maintain when they are stored in the same place.

__Documentation__ is any content separate from implementation code that explains how it works or how to use it. It may provide more concise summaries and explanation than the implementation code can.

Documentation can come in many forms, including plain text, diagrams…and tests! __Tests as documentation__ provide what many other forms cannot: both human-readable text to describe the application and machine-executable code to confirm the app works as described.

When adding a new feature to your product, it’s possible that something will break. __If that break occurs within a feature developed earlier, it is called regression__. When functionality previously developed and tested stops working, you may say the functionality regressed.


## Testing with Mocha

In Mocha we group tests using the `describe` function and define tests using the `it` function. These two functions can be used to make your test suite complete, maintainable, and expressive in the following ways:

* Structure your test suite: you can organize tests into nested groups that reflect the structure of your implementation code.

* Provide informative messages: you can define your tests using human-readable strings.

```
describe('Math', () => {
  describe('.max', () => {
    it('returns the argument with the highest value', () => {
      // Your test goes here
    });
    it('returns -Infinity when no arguments are provided', () => {
      // Your test goes here
    });
  });
});
```

`assert.ok()` allows you to compare values and throw errors as needed using one function call. The small, human-readable format of the functions will help you make a more expressive test suite. If an argument passed to assert.ok() evaluates to false, an AssertionError is thrown. The error communicates to Mocha that a test has failed, and Mocha logs the error message to the console.

### Steps in testing
__Each test is divided into setup, exercise, and verify phases__. This distinct and well-defined separation of steps makes your test more reliable, maintainable, and expressive.

The phases are defined as follows:
* Setup - create objects, variables, and set conditions that your test depends on

* Exercise - execute the functionality you are testing

* Verify - check your expectations against the result of the exercise phase. You can use the assert library here.

```
const assert = require('assert');

// Naive approach
describe('.pop', () => {
  it('returns the last element in the array [naive]', () => {
    assert.ok(['padawan', 'knight'].pop() === 'knight'); 
  });
});

// 3 phase approach
describe('.pop', () => {
  it('returns the last element in the array [3phase]', () => {
    // Setup
    const knightString = 'knight';
    const jediPath = ['padawan', knightString];

    // Exercise
    const popped = jediPath.pop();

    // Verify
    assert.ok(popped === knightString);
  });
});
```
Some tests require a fourth phase called __teardown__. It reset any conditions that were changed during test. A test, like the example in this exercise, can make changes to its environment that could affect other tests. The teardown phase is used to reset the environment before the next test runs.

Some common changes to an environment include
* altering files and directory structure
* changing read and write permissions on a file
* editing records in a database

Example for tearing down: With `fs` module, we tend to append a string to a file and then, read and verify if the file contains it. But everytime, it gets appended. So, at first it passes, but subsequently it always fails. So, on performing the test, the file must be deleted for reseting its environment.
```
const assert = require('assert');
const fs = require('fs');

describe('appendFileSync', () => {
  it('writes a string to text file at given path name', () => {

    // Setup
    const path = './message.txt';
    const str = 'Hello Node.js';
    
    // Exercise: write to file
    fs.appendFileSync(path, str);

    // Verify: compare file contents to string
    const contents = fs.readFileSync(path);
    assert.ok(contents.toString() === str);

    // Teardown: delete path
    fs.unlinkSync(path);
  });
});
```

Using teardown in the it block made your test isolated, but not reliable.

If the system encounters an error before it reaches the teardown, it will not execute that phase. In the previous example, an error may occur after the file is created but before it is deleted. The file would persist and may cause false negatives in future test runs.

Mocha provides hooks to solve that problem.

A __hook__ is a piece of code that is executed when a certain event happens. Hooks can be used to set and reset conditions like the setup and teardown phases do. In Mocha, a hook is written within a describe block.

```
describe('example', () => {
 
  afterEach(() => {
    // teardown goes here
  });
 
  it('.sample', () => {
    // test goes here
  });
});
```
In this example the function passed to afterEach is called after each it block is executed.

The other hooks in the Mocha library are `before()`, `beforeEach()`, and `after()`.

Using hook example,
```
const assert = require('assert');
const fs = require('fs');

describe('appendFileSync', () => {
  const path = './message.txt';

  afterEach(() => {
    // Teardown: delete path
    fs.unlinkSync(path);
  });
  
  it('writes a string to text file at given path name', () => {

    // Setup
    const str = 'Hello Node.js';
    
    // Exercise: write to file
    fs.appendFileSync(path, str);

    // Verify: compare file contents to string
    const contents = fs.readFileSync(path);
    assert.ok(contents.toString() === str);
  });
});
```

## Writing Expressive Tests

### Introduction
A good test framework is fast, complete, reliable, isolated, maintainable, and expressive.

An expressive test is easy to read and descriptive, making it useful as a form of documentation for your implementation code. One way to make a test more expressive is clarifying its verify phase — the step where expected outcome is compared to actual outcome.

Node.js provides a library called `assert` with methods that help you write more expressive verification code. You can use the methods in this library in place of conditional statements to write less code and use human-readable language. It can be used within the Mocha testing framework, and you will be using both throughout this lesson.

### assert.equal
You can use `assert.ok()` for most verifications, but sometimes it can be difficult to determine the condition you are evaluating.

Read the example code below. Will this assertion throw an error?
```
const landAnimals = ['giraffe', 'squirrel'];
const waterAnimals = ['shark', 'stingray'];
 
landAnimals.push('frog');
waterAnimals.push('frog');
 
assert.ok(landAnimals[2] == waterAnimals[2]);
```
The above assertion is checking for equality. In order to understand this you must evaluate the entire expression within the parentheses of .ok().

You can instead use assert.equal() which does the == comparison for us.

In the example below, the two methods achieve the same outcome.
```
assert.ok(landAnimals[2] == waterAnimals[2]);
assert.equal(landAnimals[2], waterAnimals[2]);
```
The second line is more expressive: instead of parsing the entire statement, a reader only needs to read the first two words to know the test is verifying equality!

### assert.strictEqual()
If you need to be strict in evaluating equality, you can use assert.strictEqual().

* `assert.equal()` performs a `==` comparison
* `assert.strictEqual()` performs a `===` comparison
Compare both section of code. This code performs the same verifications, but it is more expressive. Without parsing any logic, a reader would know the intention of your tests by reading the method names.
```
const a = 3;
const b = '3';
assert.ok(a == b);
assert.ok(a === b);

//more better
assert.equal(a, b);
assert.strictEqual(a, b);
```

### assert.deepEqual
```
const a = {relation: 'twin', age: '17'};
const b = {relation: 'twin', age: '17'};
assert.equal(a, b);
assert.strictEqual(a, b);
```
Both assertions will throw an error because distinct objects are not considered equal when using either loose or strict equality in JavaScript.

If you need to compare the values within two objects, you can use `assert.deepEqual()`. This method compares the values of each object using loose (==) equality.
```
assert.deepEqual(obj1, obj2);
assert.deepEqual(arr1, arr2);
```

Some other assert functions are also there
* `assert.notEqual()`
* `assert.notDeepEqual()`
* `assert.throws()` checks if it throws error


## TDD
Test-driven development (TDD) is a software development process relying on software requirements being converted to test cases before software is fully developed, and tracking all software development by repeatedly testing the software against all test cases. This is opposed to software being developed first and test cases created later.

### TDD Lifecycle
1. Add a test
2. Run all tests and these should fail for expected reasons
3. Write simplest code that passes the new test
4. All tests should pass now
5. Refactor as needed, using tests after each refactor to ensure the functionality is preserved
6. Repeat

### Development Style
1. KISS: Keep it Simple, Stupid!
2. YAGNI: You ain't gonna need it.
3. Fake it till you make it

### Limitations
1. doesn't perform sufficient testing in situations where full functional tests are required to determine success or failure, due to extensive use of unit tests. Examples of these are user interfaces, programs that work with databases, and some that depend on specific network configurations.
2. Unit tests created in a test-driven development environment are typically created by the developer who is writing the code being tested. Therefore, the tests may share blind spots with the code: if, for example, a developer does not realize that certain input parameters must be checked, most likely neither the test nor the code will verify those parameters.
3. A high number of passing unit tests may bring a false sense of security, resulting in fewer additional software testing activities, such as integration testing and compliance testing.

## TDD with Mocha
One of the driving forces of TDD is the red-green-refactor cycle. “Red” and “green” correspond to the color of the text that our test framework produces in the terminal while running the tests in our suite. Red signifies failing tests and green corresponds to passing tests.
![red-green-refactor-tdd](./red-green-refactor-tdd.webp)
Use this red, green, refactor diagram to help you as you read the steps below:

* Red — Write tests that describe the intended behavior of implementation code, and then compare developer expectations with the actual results of implementation code. The tests should always fail at first because the implementation code for the desired behavior will be written in response to the failing test.
* Green — Write just enough implementation code to make the test pass. The tests return green because the implementation code executes the intended behavior described by the test in the red phase.
* Refactor — Clean up and optimize code following the characteristics of a good test. Refactoring involves actively considering test and implementation code and making revisions to the code base. The tests are passing and should continue to pass throughout this phase of the cycle.  The purpose of the refactor phase is to think critically about the code you have and decide whether there is anything unnecessary, redundant, or that could be done more clearly or efficiently.

An __edge case__ is a problem or situation that occurs only at an extreme (maximum or minimum) operating parameter — you can think of these as special cases that you need to account for. Like for wishing function, if instead of a wishing string, a number is provided as string, it must throw an error which can be tested with `assert.throws()` and can be handled with `typeof` operator.

### Review of TDD with Mocha
At a high-level the process is:

1. Write The Test — Start with a test describing the functionality we’d like to see.
2. Fail The Test — Write code in response to the test that fails.
3. Pass The Test — The tests fail and communicate feedback to developers through error messages. It’s our responsibility to read those messages, then respond by writing the minimum amount of code to address those messages.
4. Refactor Your Code — See below.
The development process is guided by the red-green-refactor cycle.

#### Red
Write a test that covers the functionality you would like to see implemented. You don’t have to know what your code looks like at this point, you just have to know what it will do.

Run the test. You should see it fail. Most test runners will output red for failure and green for success. While we say “failure” do not take this negatively. It’s a good sign! By seeing the test fail first, we know that once we make it pass, our code works.

#### Green
Read the error message from the failing test, and write as little code as possible to fix the current error message. By only writing enough code to see our test pass, we tend to write less code as a whole. Continue this process until the test passes.

This may involve writing intermediary features covering lower level functionality which require their own Red, Green, Refactor cycle. The edge-case was an example of this.

Do not focus on code quality at this point. Be shameless! We simply want to get our new test passing.

#### Refactor
Clean up your code, reducing any duplication you may have introduced. This includes your code as well as your tests.

Treat your test suite with as much respect as you would your live code, as it can quickly become difficult to maintain if not handled with care. You should feel confident enough in the tests you’ve written that you can make your changes without breaking anything.


## Testing in React

__Jest is a javascript testing framework__. It provides some of the unique features bundled in a single framework like, zero config, snapshots, isolated testing and its well documented api. 

While, __Enzyme is a JavaScript Testing utility for React__ that makes it easier to test your React Components' output. You can also manipulate, traverse, and in some ways simulate runtime given the output.

Some useful resources:-

Jest Tutorial for Beginners: Getting Started With JavaScript Testing [Click Here](https://www.valentinog.com/blog/jest/)

How to unit test React applications with Jest and Enzyme [Click Here](https://pusher.com/tutorials/react-jest-enzyme)

Advanced Testing with React and Jest [Click Here](https://ericdcobb.medium.com/advanced-react-component-mocks-with-jest-and-react-testing-library-f1ae8838400b)

Testing in React: Best Practices, Tips, and Tricks [Click here](https://techblog.commercetools.com/testing-in-react-best-practices-tips-and-tricks-577bb98845cd)
