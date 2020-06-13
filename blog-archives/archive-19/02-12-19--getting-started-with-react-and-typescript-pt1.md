# Getting Started With React and TypeScript Pt.1 - The Setup
Have you ever wanted to try React and TypeScript together, but didn't know where to start? This tutorial will help you with it. It will show you how to implement TypeScript in existing React app. It will also show you how to create new React and TypeScript app from scratch.<!--more-->
<!--
Table of Contents:
## Benefits of TypeScript
### Optional static typing
### Intellisense, or IDE support
### Latest JavaScript features
### Browser compatibility
## Getting started with TypeScript
## Creating TypeScript config
### Note on strict option
### Most frequently used compiler options
## Setting up create-react-app project with TypeScript
## Adding TypeScript to existing create-react-app project
## Adding TypeScript to custom webpack configuration
## Creating React and TypeScript with custom webpack configuration
### Note on styles
## Conclusion: Getting Started With React and TypeScript
-->

## Benefits of TypeScript

Why is it a good idea to use React and TypeScript together? Or, why to use TypeScript in general? There are at least four benefits of using TypeScript. Mind you, these benefits are not tied to using it with React, but to using it in general.

### Optional static typing

First, there is, optional, static typing. JavaScript is dynamically typed language. This makes it easy to make mistakes. For example, you can initialize, or assign, variable with a wrong type of value. You can forget to declare that variable. You can also call a non-existing function.

It can also happen that you pass a number instead of string as a parameter to a function and it will break your code. TypeScript helps you prevent this by adding static types to your variables, functions, properties, etc. Then, when you accidentally use wrong type TypeScript will show warning.

TypeScript will tell you what the problem is and where to find it. In some cases it will also help you fix it. This will make debugging much easier. The best thing? TypeScript will show you these warnings before you even run your code. No more surprises.

### Intellisense, or IDE support

The majority of modern IDEs, including VS Code, Atom, WebStorm, Sublime Text and even VIM, have a very good support for TypeScript. As you write your code, your IDE will automatically provide you with active hints. This means less time spent trying to recall the name of some function, available parameters or existing variables.

### Latest JavaScript features

JavaScript is progressive language. There are constantly added some new features or the syntax is improved. Problem is that not all modern browsers understand your code if you use the last features. It is usually necessary to use tools such as Babel to transpile your code to make even the newer features work.

With TypeScript, you don't have to depend on babel, or other similar tools. The TypeScript compiler will do the hard work for you. As a result, you can freely use even the latest JavaScript features without having to wait for anything. You can even use features that are not officially implemented in JavaScript yet.

### Browser compatibility

This is probably the best thing on TypeScript. You don't have to worry about browser compatibility. When you write code in TypeScript it will, by default, compile your code into ES3 version of JavaScript, version all modern browsers understand.

_Note: You can change the JavaScript version to which TypeScript compiles your code by changing `target` compiler option in your `tsconfig.json`._

## Getting started with TypeScript

There are two ways you can start with TypeScript. You can either install it global, with npm, pnpm or yarn. Or, you can add it as a dependency to project you want to develop with React and TypeScript. You should know that installing TypeScript globally is not necessary. It will be sufficient to install it per project as a dependency.

Installing TypeScript globally:

```
npm i -g typescript
```

Installing TypeScript as a dependency:

```
npm i -D typescript
```

## Creating TypeScript config

When you install TypeScript the first thing to do is creating a config file for TypeScript called `tsconfig.json`. This config file is used to specify what files you want to include or exclude, or process by TypeScript. TypeScript will automatically include all files written in TypeScript. These are `.ts`, `.d.ts` (TypeScript definitions) and `.tsx` (TypeScript alternative to JSX).

This config file is also where you specify TypeScript configuration for your project. This is done with `compilerOptions` object. There are many [options] you can use. Mind you, you don't have to use all of these options. You don't actually use any of them because the `compilerOptions` is not required.

As said, it is up to you what options will you use and what not. If you are just starting out, it might be better to start with a blank slate. Outside the `compilerOptions` object, you can specify only what files to include and exclude (usually `node_modules`). Then, inside it, you can specify `target` and `module` options.

The `target` tells TypeScript to which ECMAScript version you want to compile your code. The `module` tells TypeScript what module should it use for code generation. You can find all available options in the [documentation] for compiler options. When you have these two covered, you can start experimenting adding more options.

This is probably one of the best approaches to getting started with React and TypeScript at least based on my experience. It is also one of the best approaches to getting started with TypeScript in general. Using all options right from the beginning could be overwhelming. TypeScript would complain about even the smallest problem.

You would spend hours trying to figure where the problem is and how to solve it. You would also probably had to rewrite the majority of your code base, if you decide to try to implement TypeScript in an existing project. If you create new project to try React and TypeScript everything will be easier. I suggest going this way.

When you decide to try React and TypeScript, and use TypeScript to create the default `tsconfig.json`, you will get something similar to the example below. Notice that the majority of options are commented out. As I mentioned this is a good place to start if you decide to try React and TypeScript together.

```json
{
  "compilerOptions": {
    /* Basic Options */
    // "incremental": true,                   /* Enable incremental compilation */
    "target": "es5",                          /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019' or 'ESNEXT'. */
    "module": "esnext",                       /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */
    // "lib": [],                             /* Specify library files to be included in the compilation. */
    // "allowJs": true,                       /* Allow javascript files to be compiled. */
    // "checkJs": true,                       /* Report errors in .js files. */
    // "jsx": "preserve",                     /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */
    // "declaration": true,                   /* Generates corresponding '.d.ts' file. */
    // "declarationMap": true,                /* Generates a sourcemap for each corresponding '.d.ts' file. */
    // "sourceMap": true,                     /* Generates corresponding '.map' file. */
    // "outFile": "./",                       /* Concatenate and emit output to single file. */
    // "outDir": "./",                        /* Redirect output structure to the directory. */
    // "rootDir": "./",                       /* Specify the root directory of input files. Use to control the output directory structure with --outDir. */
    // "composite": true,                     /* Enable project compilation */
    // "tsBuildInfoFile": "./",               /* Specify file to store incremental compilation information */
    // "removeComments": true,                /* Do not emit comments to output. */
    // "noEmit": true,                        /* Do not emit outputs. */
    // "importHelpers": true,                 /* Import emit helpers from 'tslib'. */
    // "downlevelIteration": true,            /* Provide full support for iterables in 'for-of', spread, and destructuring when targeting 'ES5' or 'ES3'. */
    // "isolatedModules": true,               /* Transpile each file as a separate module (similar to 'ts.transpileModule'). */

    /* Strict Type-Checking Options */
    "strict": true,                           /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                 /* Raise error on expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,              /* Enable strict null checks. */
    // "strictFunctionTypes": true,           /* Enable strict checking of function types. */
    // "strictBindCallApply": true,           /* Enable strict 'bind', 'call', and 'apply' methods on functions. */
    // "strictPropertyInitialization": true,  /* Enable strict checking of property initialization in classes. */
    // "noImplicitThis": true,                /* Raise error on 'this' expressions with an implied 'any' type. */
    // "alwaysStrict": true,                  /* Parse in strict mode and emit "use strict" for each source file. */

    /* Additional Checks */
    // "noUnusedLocals": true,                /* Report errors on unused locals. */
    // "noUnusedParameters": true,            /* Report errors on unused parameters. */
    // "noImplicitReturns": true,             /* Report error when not all code paths in function return a value. */
    // "noFallthroughCasesInSwitch": true,    /* Report errors for fallthrough cases in switch statement. */

    /* Module Resolution Options */
    // "moduleResolution": "node",            /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */
    // "baseUrl": "./",                       /* Base directory to resolve non-absolute module names. */
    // "paths": {},                           /* A series of entries which re-map imports to lookup locations relative to the 'baseUrl'. */
    // "rootDirs": [],                        /* List of root folders whose combined content represents the structure of the project at runtime. */
    // "typeRoots": [],                       /* List of folders to include type definitions from. */
    // "types": [],                           /* Type declaration files to be included in compilation. */
    // "allowSyntheticDefaultImports": true,  /* Allow default imports from modules with no default export. This does not affect code emit, just typechecking. */
    "esModuleInterop": true,                  /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    // "preserveSymlinks": true,              /* Do not resolve the real path of symlinks. */
    // "allowUmdGlobalAccess": true,          /* Allow accessing UMD globals from modules. */

    /* Source Map Options */
    // "sourceRoot": "",                      /* Specify the location where debugger should locate TypeScript files instead of source locations. */
    // "mapRoot": "",                         /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSourceMap": true,               /* Emit a single file with source maps instead of having a separate file. */
    // "inlineSources": true,                 /* Emit the source alongside the sourcemaps within a single file; requires '--inlineSourceMap' or '--sourceMap' to be set. */

    /* Experimental Options */
    // "experimentalDecorators": true,        /* Enables experimental support for ES7 decorators. */
    // "emitDecoratorMetadata": true,         /* Enables experimental support for emitting type metadata for decorators. */

    /* Advanced Options */
    "forceConsistentCasingInFileNames": true  /* Disallow inconsistently-cased references to the same file. */
  }
}
```

### Note on strict option

One thing you may disable, only at the beginning, is the `strict` option. This option enables all strict type checking options. These options are `--noImplicitAny`, `--noImplicitThis`, `--alwaysStrict`, `--strictBindCallApply`, `--strictNullChecks`, `--strictFunctionTypes` and `--strictPropertyInitialization`.

If you are just starting out with React and TypeScript there will be some new things and practices to learn. These are neither difficult nor bad. They will help you write cleaner and better code. The problem is that you may not be used to them, or some of them. It is often better to start slowly and adopt new practice one by one.

So, in the beginning, disable the `strict` option. Next, add all those strict type checking options explicitly and disable them as well. After that, learn about them and one-by-one enable them. This will help you get used to working with React and TypeScript. When you are done with them, you can replace them with `strict`.

### Most frequently used compiler options

Some of the most frequently used options in project built with React and TypeScript are `module`, `moduleResolution`, `target`, `allowJs`, `jsx` and `strict`. You already know about `module` and `target`. The `moduleResolution` specifies how modules get [resolved]. The `allowJs` tells TypeScript to include `.js` and `.jsx` files in processing.

The `jsx`, adds support for JSX in `.tsx` files. The last one is `strict`, the option we discussed above. This option is often better to disable in the beginning, before you get used to working with React and TypeScript. Otherwise, you may end up in type checking hell, losing your enthusiasm and throwing TypeScript out the window.

However, when you get used to it, and learn the nuts and bolts of `strict`, enable it by default. If there is any way TypeScript can help you write cleaner and more stable and predictable code it is thanks to the `strict` option.

## Setting up create-react-app project with TypeScript

If you are used to working with app generators such as [create-react-app] getting started with React and TypeScript will be very easy. Let's say you want to start a new project, and you want to use React and TypeScript together. Instead of using `npx create-react-app my-app` command use `npx create-react-app my-app --typescript`.

The `--typescript` flag at the end of the command will automatically create app with necessary configuration for TypeScript. It will also generate `tsconfig.json`. So, you don't have to worry about creating any configuration. The `create-react-app` create it for you and make it even easier for you to start with React and TypeScript.

The `tsconfig.json` provided by `create-react-app` will look like the example below.

```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react"
  },
  "include": [
    "src"
  ]
}
```

## Adding TypeScript to existing create-react-app project

Let's say you want to start using React and TypeScript together in existing project, based on `create-react-app`. In this case, you will need to add these dependencies: `typescript`, `@types/node`, `@types/react` and `@types/react-dom`. Next, you will need to rename all your `.jsx` files to `.tsx`, and `.js` files to `.ts`.

When you are done with that, all you need is to start your app. The app will automatically detect TypeScript, generate `tsconfig.json`, with default configuration, and you will be able to use React and TypeScript together right away.

## Adding TypeScript to custom webpack configuration

If you don't want to use `create-react-app` generator you don't have to. Using React and TypeScript with custom configuration is also very easy. First, let's assume you have existing React project where you want to implement TypeScript. In this case, the process will be very similar to adding TypeScript to `create-react-app` project.

You will add `typescript`, `@types/react` and `@types/react-dom` dependencies. You will also need `awesome-typescript-loader`. This will allow webpack handle TypeScript files. Next, you will need to change your webpack config files. You will add `.tsx` and `.ts` to the `extensions` array, under `resolve`.

```js
  // ...
  resolve: {
    // Add .ts and .tsx to extensions
    extensions: [
      '.js',
      '.jsx',
      '.tsx',
      '.ts'
    ]
  // ...
```

Next, you will add new rule for `.tsx` and `.ts`. This rule will use the `awesome-typescript-loader` to handle `.tsx` and `.ts` files. It will also exclude `node_modules`. Lastly, in the `entry`, you will need to change the `./src/index.js` to `./src/index.tsx`, or any other file you use as an entry point.

```js
  // ...
  entry: [
    './src/index.tsx' // Change entry point
  ],
  module: {
    rules: [
      // Add rule for .ts and .tsx
      {
        test: /\.ts(x)?$/,
        use: [
          'awesome-typescript-loader'
        ],
        exclude: /node_modules/
      }
      // ...
```

## Creating React and TypeScript with custom webpack configuration

What if you are starting from scratch and want to create webpack config for React and TypeScript app? First, add `react`, `react-dom`, `typescript`, `@types/node`, `@types/react`,  `@types/react-dom`, `webpack`, `webpack-cli`, `@types/react`, `@types/react-dom`, `@babel/preset-react`, `babel-loader`, `@babel/core`, `@babel/preset-env`, `webpack-dev-server`, `typescript`, `awesome-typescript-loader`.

Next, add three new npm scripts to your `package.json`. These will be `"build-dev": "webpack -d --mode development"`, `"build-prod": "webpack -p --mode production"` and `"start": "webpack-dev-server --hot --mode development"`. Your `package.json` will look similar to the example below.

```json
{
  "name": "react-typescript-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.tsx",
  "keywords": [],
  "author": "",
  "license": "ISC",
  "scripts": {
    "build-dev": "webpack -d --mode development",
    "build-prod": "webpack -p --mode production",
    "start": "webpack-dev-server --hot --mode development"
  },
  "dependencies": {
    "react": "^16.12.0",
    "react-dom": "^16.12.0"
  },
  "devDependencies": {
    "@babel/core": "^7.7.4",
    "@babel/preset-env": "^7.7.4",
    "@babel/preset-react": "^7.7.4",
    "@types/react": "^16.9.13",
    "@types/react-dom": "^16.9.4",
    "awesome-typescript-loader": "^5.2.1",
    "babel-loader": "^8.0.6",
    "typescript": "^3.7.2",
    "webpack": "^4.41.2",
    "webpack-cli": "^3.3.10",
    "webpack-dev-server": "^3.9.0"
  }
}
```

The next step is creating config file for webpack. The process will be similar to "Adding TypeScript to custom webpack configuration". The files to be resolved will be `.jsx`, `.js`, `.tsx` and `.ts`. There will be two rule sets, one for `.jsx` and `.js` files and one for `.tsx` and `.ts` files.

The first set will be handled by `babel-loader`, the second by `awesome-typescript-loader`. In both rule sets, remember to exclude `node_modules`. The entry will also point to `./src/index.tsx`. Output directory, and also `contentBase` for `devServer`, can be "dist". This will give you a simple webpack config you can start with.

```js
const webpack = require('webpack');
const path = require('path');

const config = {
  entry: [
    './src/index.tsx'
  ],
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader',
        exclude: /node_modules/
      },
      {
        test: /\.ts(x)?$/,
        use: [
          'awesome-typescript-loader'
        ],
        exclude: /node_modules/
      }
    ]
  },
  resolve: {
    extensions: [
      '.js',
      '.jsx',
      '.tsx',
      '.ts'
    ]
  },
  devServer: {
    contentBase: './dist'
  }
};

module.exports = config;
```

Now, you will create `.babelrc`. Here, you will configure `@babel/preset-env` and `@babel/preset-react` presets. This will allow webpack work with React code, thanks to babel. It will also allow you to use the latest JavaScript, or TypeScript syntax.

```
{
  presets: [
    [
      '@babel/preset-env',
      {
        modules: false
      }
    ],
    '@babel/preset-react'
  ]
}
```

The last step. You will need to create `tsconfig.json`. It is up to you what compiler options will you use. So, take the example below as that, an example. What should stay are `module`, `moduleResolution`, `target`, `jsx`, `include` and `outDir`. Other than that, add or remove any options you want.

```json
{
  "compilerOptions": {
    "outDir": "./dist/",
    "sourceMap": true,
    "strict": true,
    "noImplicitReturns": true,
    "noImplicitAny": true,
    "module": "es6",
    "moduleResolution": "node",
    "target": "es5",
    "allowJs": true,
    "jsx": "react",
  },
  "include": [
    "./src/**/*"
  ]
}
```

Now, add `index.html` in the "dist" directory. There are two necessary elements. The first one is the `div` element where you want to render your React app. The second one is `script` for adding `bundle.js` created by webpack. The rest of content of this file is up to you.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>React and TypeScript</title>
    <meta charset="utf-8">
  </head>

  <body>
    <div id="root"></div>
    <script src="bundle.js"></script>
  </body>
</html>
```

Now, the `index.tsx`. This will be the main file for your React app. It will be, probably, in "src" directory. Here, you will either create or import the main React component and render it in the `div` element you created in `index.html`. With that, you are ready to build your next app with React and TypeScript.

```tsx
// Import React and render
import * as React from 'react'
import { render } from 'react-dom'

// Create simple component
const App = () => <div>Hello!</div>

// Render the component in DOM
const rootElement = document.getElementById('root')
render(<App />, rootElement)
```

### Note on styles

One thing about the custom webpack configuration for starting from scratch. It is not configured to handle any CSS, Sass, less or PostCSS files. This will not be a problem if you want to build your app with React and TypeScript with one of the [CSS-in-JS libraries]. Then, can use your library of choice right away.

If you want to use CSS, or some CSS pre- or post-processor, make sure you install appropriate loaders. Then, add rules for files with CSS styles to your webpack config. In case of `create-react-app`, for basic support of CSS and [CSS modules], you don't have to add anything. The `create-react-app` project [supports] both these options.

If you want to use Sass, you will need to add `node-sass`, as is mentioned in the [installation instructions]. That's it. In `create-react-app`, there is no need to add any webpack loaders.

## Conclusion: Getting Started With React and TypeScript

In this tutorial, you have learned how to implement TypeScript in your existing React projects so you can use React and TypeScript together. You have also learned how to create React and TypeScript project from scratch, with `create-react-app` or custom webpack configuration.

What's coming next? In the next part, you will learn about types and interfaces and how to use React and TypeScript together the right way. Until then, practice what you have learned today.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[options]: https://www.typescriptlang.org/docs/handbook/compiler-options.html
[documentation]: https://www.typescriptlang.org/docs/handbook/compiler-options.html
[resolved]: https://www.typescriptlang.org/docs/handbook/module-resolution.html
[create-react-app]: https://github.com/facebook/create-react-app
[CSS-in-JS libraries]: https://blog.alexdevero.com/style-react-components-pt2/#no5-css-in-js
[CSS modules]: https://github.com/css-modules/css-modules
[supports]: https://create-react-app.dev/docs/adding-a-css-modules-stylesheet
[installation instructions]: https://create-react-app.dev/docs/adding-a-sass-stylesheet

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
