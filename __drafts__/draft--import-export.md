# Import and Export in JavaScript and How to Use It

Import and export statements are two great features introduced ES6 (ES2015). These two statement allows you to export and import your code and use it whenever you need. This tutorial will show you what import and export statements are, how they work and how to use them.<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

In the past, when JavaScript developers wanted to split their code into modules they had to use one of the three options. These options were [AMD], [CommonJS] and [UMD]. There was built-in support for modules in JavaScript. Things changed when the ES2015 (ES6) specification was released.

One feature this specification brought to JavaScript was also a support for modules on a language-level. JavaScript developers were now able to work with native modules with the help of newly introduced statements `import` and `export`. Now, you as a JavaScript developer can split your code into multiple files.

Each of these files is a module. These modules can contain anything, from variables and functions to classes. In order to this code available to the outside you have to simply exporting it. When you want to use some of that exported code, you simply import it where you need. Now, let's take a look at both those new statements.

## The export statement

When you want to export some variable, function or class you have to place the `export` keyword before it. This tells JavaScript two things. First, you want that "thing" to be available from the outside of the current file. Second, other parts of the program should be able to import that "thing" with the `import` statement.

When you export some code you can still change it and update it. However, you can that only at the place where you exported it. You can't do that when you import that exported code somewhere else. When you import some exported code you can only read it and use it, but not change it.

### Two ways to export

When you want to export some code with `export` statement, there are two ways to do it. The first one is by exporting at the moment of declaration. In this case, you put the `export` statement on the same line right before the variable, function or class you are about to declare.

```JavaScript
// Declare and export variables
export const MY_PASS = 'Some very important secret.'
export let name = 'Jack'
export var stack = 'JS'

// Declare and export functions
export function sayHi() {
  return 'Hi.'
}

export const sayBye = function() {
  return 'Bye.'
}

export const sayGoodBye = () => {
  return 'Good bye.'
}

// Declare and export class
export class Person {
  name = this.name
  age = this.age
  #my_secret = this.secret
}
```

The second way to export code is by declaring it first and exporting it after that. In this case you use the `export` statement followed by the "thing" you want to export.

```JavaScript
// Declare variables
const MY_PASS = 'Some very important secret.'
let name = 'Jack'
var stack = 'JS'

// Export variables
export MY_PASS
export name
export stack

// Declare functions
function sayHi() {
  return 'Hi.'
}

const sayBye = function() {
  return 'Bye.'
}

const sayGoodBye = () => {
  return 'Good bye.'
}

// Declare and export functions
export sayHi
export sayBye
export sayGoodBye

// Declare class
class Person {
  name = this.name
  age = this.age
  #my_secret = this.secret
}

// Export class
export Person
```

When you decide to use the second way there is another thing to do. Instead of export all those things individually, you can export them at once with a single `export` statement. For example, at the end of the file. To do this, you have to wrap everything you want to export with curly braces, separated by commas.

```JavaScript
// Declare some stuff
const MY_PASS = 'Some very important secret.'

let name = 'Jack'

function sayHi() {
  return 'Hi.'
}

class Car {
  numOfWheels = this.numOfWheels
  typeOfFuel = this.typeOfFuel
}

// Export all the stuff at once
export { MY_PASS, sayHi, Car }
```

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[AMD]: https://en.wikipedia.org/wiki/Asynchronous_module_definition
[CommonJS]: http://wiki.commonjs.org/wiki/Modules/1.1
[UMD]: https://github.com/umdjs/umd

<!--
### Meta:
-
-->

<!--
### Keywords:
-
-->

<!--
### Resources:
- https://www.taniarascia.com/javascript-modules-import-export/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export
-->
