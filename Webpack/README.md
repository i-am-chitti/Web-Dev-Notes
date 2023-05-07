# Webpack

## Intro

At its core, webpack is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph from one or more entry points and then combines every module your project needs into one or more bundles, which are static assets to serve your content from.

Core concepts -
- Entry
- Output
- Loaders
- Plugins
- Mode
- Browser Compatibility

### Dependency Graph

Any time one file depends on another, webpack treats this as a dependency. This allows webpack to take non-code assets, such as images or web fonts, and also provide them as dependencies for your application.

When webpack processes your application, it starts from a list of modules defined on the command line or in its configuration file. Starting from these entry points, webpack recursively builds a dependency graph that includes every module your application needs, then bundles all of those modules into a small number of bundles - often, only one - to be loaded by the browser.

### Entry

Usage: `entry: string | [string] | { <entryChunkName> string }`

An entry point indicates which module webpack should use to begin building out its internal dependency graph. Webpack will figure out which other modules and libraries that entry point depends on (directly and indirectly).

By default its value is `./src/index.js`, but you can specify a different (or multiple) entry points by setting an entry property in the webpack configuration.

Example -

```
module.exports = {
  entry: ['./src/file_1.js', './src/file_2.js'],
  output: {
    filename: 'bundle.js',
  },
};
```

```
module.exports = {
  entry: {
    app: './src/app.js',
    adminApp: './src/adminApp.js',
  },
};
```

### Output

The output property tells webpack where to emit the bundles it creates and how to name these files. It defaults to `./dist/main.js` for the main output file and to the `./dist` folder for any other generated file.

You can configure this part of the process by specifying an output field in your configuration:

```
module.exports = {
  output: {
    filename: 'bundle.js',
  },
};
```
#### multiple entry points

```
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js',
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist',
  },
};

// writes to disk: ./dist/app.js, ./dist/search.js
```

### Loaders

Out of the box, webpack only understands JavaScript and JSON files. Loaders allow webpack to process other types of files and convert them into valid modules that can be consumed by your application and added to the dependency graph.

#### Example -

For example, you can use loaders to tell webpack to load a CSS file or to convert TypeScript to JavaScript. To do this, you would start by installing the loaders you need:

```
npm install --save-dev css-loader ts-loader
```

And then instruct webpack to use the `css-loader` for every `.css` file and the `ts-loader` for all `.ts` files:

```
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' },
    ],
  },
};
```

#### Using Loaders

There are two ways to use loaders in your application:

1. Configuration (recommended): Specify them in your webpack.config.js file.
2. Inline: Specify them explicitly in each import statement.

##### Configuration

`module.rules` allows you to specify several loaders within your webpack configuration. This is a concise way to display loaders, and helps to maintain clean code. It also offers you a full overview of each respective loader..

At a high level, loaders have two properties in your webpack configuration:

- The `test` property identifies which file or files should be transformed.
- The `use` property indicates which loader should be used to do the transforming.

Loaders are evaluated/executed from right to left (or from bottom to top). In the example below execution starts with sass-loader, continues with css-loader and finally ends with style-loader. See "Loader Features" for more information about loaders order

```
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          {
            loader: 'css-loader',
            options: {
              modules: true,
            },
          },
          { loader: 'sass-loader' },
        ],
      },
    ],
  },
};
```

#### Loader Features

- Loaders can be chained. Each loader in the chain applies transformations to the processed resource. A chain is executed in reverse order. The first loader passes its result (resource with applied transformations) to the next one, and so forth. Finally, webpack expects JavaScript to be returned by the last loader in the chain.
- Loaders can be synchronous or asynchronous.
- Loaders run in Node.js and can do everything that’s possible there.
- Loaders can be configured with an options object (using query parameters to set options is still supported but has been deprecated).
- Normal modules can export a loader in addition to the normal main via package.json with the loader field.
- Plugins can give loaders more features.
- Loaders can emit additional arbitrary files


### Plugins

While loaders are used to transform certain types of modules, plugins can be leveraged to perform a wider range of tasks like bundle optimization, asset management and injection of environment variables.

#### Anatomy

A webpack plugin is a JavaScript object that has an `apply` method. This `apply` method is called by the webpack compiler, giving access to the entire compilation lifecycle.

```
const pluginName = 'ConsoleLogOnBuildWebpackPlugin';

class ConsoleLogOnBuildWebpackPlugin {
  apply(compiler) {
    compiler.hooks.run.tap(pluginName, (compilation) => {
      console.log('The webpack build process is starting!');
    });
  }
}

module.exports = ConsoleLogOnBuildWebpackPlugin;
```

#### Usage

Since plugins can take arguments/options, you must pass a new instance to the plugins property in your webpack configuration.

```
const HtmlWebpackPlugin = require('html-webpack-plugin');
const webpack = require('webpack'); //to access built-in plugins
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
      },
    ],
  },
  plugins: [
    new webpack.ProgressPlugin(),
    new HtmlWebpackPlugin({ template: './src/index.html' }),
  ],
};
```


### Mode

By setting the mode parameter to either `development`, `production` or `none`, you can enable webpack's built-in optimizations that correspond to each environment. The default value is `production`.

```
module.exports = {
  mode: 'production',
};
```

We can pass it as a CLI argument as well like
```
webpack --mode=development
```

### Browser Compatibility

Webpack supports all browsers that are ES5-compliant (IE8 and below are not supported). Webpack needs Promise for import() and require.ensure(). If you want to support older browsers, you will need to load a polyfill before using these expressions.

### Targets

Because JavaScript can be written for both server and browser, webpack offers multiple deployment targets that you can set in your webpack configuration.

#### Usage

To set the target property, you set the target value in your webpack config:

```
module.exports = {
  target: 'node',
};
```


### Modules

In contrast to Node.js modules, webpack modules can express their dependencies in a variety of ways. A few examples are:

- An ES2015 `import` statement
- A CommonJS `require()` statement
- An AMD `define` and `require` statement
- An `@import` statement inside of a css/sass/less file.
- An image url in a stylesheet `url(...)` or HTML `<img src=...>` file.

#### Supported Modules

- ECMAScript Modules
- CommonJS Module
- AMD Modules
- Assets
- WebAssembly Modules


## Hot Module Replacement

Hot Module Replacement (HMR) exchanges, adds, or removes modules while an application is running, without a full reload. This can significantly speed up development in a few ways:

- Retain application state which is lost during a full reload.
- Save valuable development time by only updating what's changed.
- Instantly update the browser when modifications are made to CSS/JS in the source code, which is almost comparable to changing styles directly in the browser's dev tools.

### How it works

#### In the application

The following steps allow modules to be swapped in and out of an application:

- The application asks the HMR runtime to check for updates.
- The runtime asynchronously downloads the updates and notifies the application.
- The application then asks the runtime to apply the updates.
- The runtime synchronously applies the updates.

#### In compiler

In addition to normal assets, the compiler needs to emit an "update" to allow updating from the previous version to the new version. The "update" consists of two parts:

- The updated manifest (JSON)
- One or more updated chunks (JavaScript)

The manifest contains the new compilation hash and a list of all updated chunks. Each of these chunks contains the new code for all updated modules (or a flag indicating that the module was removed).

#### In runtime

For the module system runtime, additional code is emitted to track module parents and children. On the management side, the runtime supports two methods: `check` and `apply`.

A `check` makes an HTTP request to the update manifest. If this request fails, there is no update available. If it succeeds, the list of updated chunks is compared to the list of currently loaded chunks. For each loaded chunk, the corresponding update chunk is downloaded. All module updates are stored in the runtime. When all update chunks have been downloaded and are ready to be applied, the runtime switches into the `ready` state.

The `apply` method flags all updated modules as invalid. For each invalid module, there needs to be an update handler in the module or in its parent(s). Otherwise, the invalid flag bubbles up and invalidates parent(s) as well. Each bubble continues until the app's entry point or a module with an update handler is reached (whichever comes first). If it bubbles up from an entry point, the process fails.

Afterwards, all invalid modules are disposed (via the dispose handler) and unloaded. The current hash is then updated and all `accept` handlers are called. The runtime switches back to the `idle` state and everything continues as normal.

### Code Splitting

Code splitting is one of the most compelling features of webpack. This feature allows you to split your code into various bundles which can then be loaded on demand or in parallel. It can be used to achieve smaller bundles and control resource load prioritization which, if used correctly, can have a major impact on load time.

There are three general approaches to code splitting available:

1. Entry Points: Manually split code using `entry` configuration.
2. Prevent Duplication: Use Entry dependencies or SplitChunksPlugin to dedupe and split chunks.
3. Dynamic Imports: Split code via inline function calls within modules.

There are some pitfalls to this approach:

- If there are any duplicated modules between entry chunks they will be included in both bundles.
- It isn't as flexible and can't be used to dynamically split code with the core application logic.


### Tree Shaking

Tree shaking is a term commonly used in the JavaScript context for dead-code elimination. It relies on the static structure of ES2015 module syntax, i.e. `import` and `export`.
