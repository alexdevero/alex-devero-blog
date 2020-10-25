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

### Two types of export

There are also two types of exports you can use. One is called named export and the other default export. When it comes to named exports, you can create as many of them as you want. There is no limit. This doesn't apply to default exports. In JavaScript, you can have only one default export per module.

The first type, named export, is what you saw on the examples above. In these examples, you were using the `export` keyword along with the name of the thing you wanted to export. All these exports were named. When you want to export something as `default` you have to add `default` between the `export` statement and what you want to export.

```JavaScript
// Named export
export const LANG = 'English'

// or
const favoriteFantasy = 'Discworld'
export favoriteFantasy


// Default export
export default const LANG = 'English'

// or
const favoriteFantasy = 'Discworld'
export default favoriteFantasy
```

There is another way to export something as `default`. You can wrap the name of the thing you want to export with curly braces. Next, you add `as` keyword, followed by the `default` keyword. This will also export that thing as default.

```JavaScript
// Another way to create default export
const FAVORITE_SEASON = 'Summer'

// Export FAVORITE_SEASON as default
export { FAVORITE_SEASON as default }
```

### Renaming exports

When you export something, and you don't want to use the variable, function or class name, you can rename it. To do that, you have to wrap the name with curly braces and add `as` keyword followed by new name, under which you want to export it. If you export multiple things, you can use this to rename all of them or just some.

```JavaScript
// Declare a variable
let sillyJoke = 'Knock, knock.'

// Export the variable and rename it
export { sillyJoke as classicJoke }


// Declare multiple variables
const petOne = 'Dog'
const petTwo = 'Cat'
const petThree = 'Alligator'
const petFour = 'Dragon'

// Export all variables and rename some
// Note: line breaks are just for readability
export {
  petOne,
  petTwo as pet2, // rename export only for petTwo
  petThree as pet3, // rename export only for petThree
  petFour
}
```

## The import statement

When you want to import some code you have to use the `import` statement. Remember that this will work only with code you exported with the `export` statement. You can't import something you didn't export. When you want to import something, there are two options from which you can choose.

In both cases, you have to start the line with the `import` keyword. Next, you specify the name of the exported module you want to import. This part of syntax will differ according to which of the two options you choose. After that follows `from` keyword, followed by the name of the file from which you want to import those modules.

```JavaScript
// Example of import syntax
import { someModule } from 'file.js'
import someModule from 'file.js'
```

### Importing individual modules

The first option is to import modules, those things you've exported, individually. If you choose this, you have to consider how you exported those modules. If you exported those modules with named exports you have to use exactly the names you used. If you used renaming, then, you have to use those new names.

When importing named exports, you have to wrap those names with curly braces. This is required when you import named exports. Similarly to exporting, you can also import all exports individually with multiple `import` statements. You can also import them all with single `import` statement. In that case, you have to separate those exported modules with commas.

```JavaScript
// File 1: file-one.js
// Declare and export some stuff
// Use named export
export const age = 29

function sayHi() {
  return 'Hello'
}

// Use named export with renaming
export { sayHi as greeting }


// File 2: file-two.js
// Import only the "age" variable
import { age } from 'file-one.js'

// Try to read imported "age" variable
console.log(age)
// Output:
// 29


// Import only the "greeting" function
// Note: you exported the sayHi as greeting
// so you have to import it as greeting, not as sayHi
import { age } from 'file-one.js'

// Import both, "age" and "greeting"
import { age, greeting } from 'file-one.js'

// Try to read imported "age" variable
console.log(age)
// Output:
// 29

// Try to call imported "greeting" function
console.log(greeting())
// Output:
// 'Hello'
```

If you exported some module as `default`, you can choose whatever name to import that module you want. And, don't wrap the module name with curly braces if you want to import default export. Otherwise, JavaScript will throw en error.

```JavaScript
// File 1: file-one.js
// Declare and export some stuff as default
export default const surname = 'Joe'


// File 2: file-two.js
// Import only default export "name"
// Note: no curly braces around the name
import surname from 'file-one.js'

// Try to read imported "age" variable
console.log(surname)
// Output:
// 'Joe'
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
