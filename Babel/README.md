# Babel

## Babel is a JavaScript compiler

Babel is a toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments. Here are the main things Babel can do for you:

- Transform syntax
- Polyfill features that are missing in your target environment (through a third-party polyfill such as core-js)
- Source code transformations (codemods)
- and many more

```
// Babel Input: ES2015 arrow function
[1, 2, 3].map(n => n + 1);

// Babel Output: ES5 equivalent
[1, 2, 3].map(function(n) {
  return n + 1;
});
```

By default, babel converts ES2015-ES2020 to the oldest JS ie ES5. In ES2015, some concepts are -
- Arrow functions
- classes
- block scoping
- literals


## Usage Guide

### Overview

1. Run these -

```
npm install --save-dev @babel/core @babel/cli @babel/preset-env
```

2. Creating a config file named `babel.config.json` (requires v7.8.0 and above) in the root of your project with this content:

```
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          "edge": "17",
          "firefox": "60",
          "chrome": "67",
          "safari": "11.1"
        },
        "useBuiltIns": "usage",
        "corejs": "3.6.5"
      }
    ]
  ]
}
```

3. And running this command to compile all your code from the `src` directory to `lib`:

```shell
./node_modules/.bin/babel src --out-dir lib
```

### Basic usage with CLI

All the Babel modules you'll need are published as separate npm packages scoped under `@babel`

#### Core Library

The core functionality of Babel resides at the `@babel/core` module.

#### CLI tool

`@babel/cli` is a tool that allows you to use babel from the terminal. Here's the installation command and a basic usage example
```
npm install --save-dev @babel/core @babel/cli

./node_modules/.bin/babel src --out-dir lib
```

### Plugins and Presets

Transformations come in the form of plugins, which are small JavaScript programs that instruct Babel on how to carry out transformations to the code. You can even write your own plugins to apply any transformations you want to your code. To transform ES2015+ syntax into ES5 we can rely on official plugins like `@babel/plugin-transform-arrow-functions`:

```
npm install --save-dev @babel/plugin-transform-arrow-functions

./node_modules/.bin/babel src --out-dir lib --plugins=@babel/plugin-transform-arrow-functions
```

Now any arrow functions in our code will be transformed into ES5 compatible function expressions:

```
const fn = () => 1;

// converted to

var fn = function fn() {
  return 1;
};
```

That's a good start! But we also have other ES2015+ features in our code that we want transformed. **Instead of adding all the plugins we want one by one, we can use a "preset" which is just a pre-determined set of plugins**.

Some presets are -

- `@babel/preset-env`
- `@babel/preset-react` - transforms JSX to JS
- `@babel/preset-typescript` - transforms TSX to JS
- `@babel/preset-flow` - use with [Flow](https://flow.org/en/docs/getting-started/)


### @babel/env

`@babel/preset-env` is a smart preset that allows you to use the latest JavaScript without needing to micromanage which syntax transforms (and optionally, browser polyfills) are needed by your target environment(s). This both makes your life easier and JavaScript bundles smaller.

It uses `browserlist`, `compat-table` and `electron-to-chromium`
