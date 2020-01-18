# ES6, ES7, ES8 & Writing Modern JavaScript Pt5 - WeakMap, WeakSet and Export & Import

ES6 brought a lot of new features to JavaScript. In this part, you will learn, understand and master `WeakMap`, `WeakSet` and `export` and `import` statements, including dynamic imports. You will also learn a bit about weak and strong reference. Learn the nuts and bolts of ES6 and become a better JavaScript developer!<!--more-->

<!--
Table of Contents:
## WeakMap and WeakSet
### WeakMap
### WeakSet
### The differences between Map & WeakMap and Set & WeakSet
## Export, import and modules
### The import statement
### The export statement
### Dynamic imports
## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt5
-->

ES6, ES7, ES8 & Writing Modern JavaScript [Part 1] (Scope, let, const, var).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 2] (Template literals, Destructuring & Default Params).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 3] (Spread, Rest, Sets & Object Literal).

ES6, ES7, ES8 & Writing Modern JavaScript [Part 4] (Includes, Pads, Loops & Maps).

## WeakMap and WeakSet

In the third part, you've learned about [Sets]. Then, in the fourth part, you've also learned about [Maps]. Since the release of ES6, both these objects also have their "weaker" counterparts. These counterparts are called `WeakMap` and `WeakSet`. This raises a question. What is the difference between `Map` and `WeakMap` and `Set` and `WeakSet`?

In this situation, the word "weak" is used to specify a type of reference, or a type of pointer. In case of `WeakMap` it means that the key/value pairs inside the `WeakMap` are weakly referenced (weak pointers). In case of `WeakSet` they are the objects inside the `WeakSet` that are referenced weakly (weak pointers). Still, what does it mean when something is referenced weakly?

A weak reference means that when something is removed from the memory and all references to that thing are removed the thing itself can be [garbage collected]. So, when you try to access that thing, you will get `undefined` because there are no references to it. This is not true for things with strong reference. They will not be garbage collected if no other reference to it exists.

Another way to put it. A weakly referenced thing (a younger brother) is protected from garbage collection (a bully) only when some other reference to it (an older brother) exists (is close). When all references are gone (the older brother is elsewhere) the weakly referenced thing (the younger brother) is no longer protected from garbage collection (the bully) and it gets collected (gets bullied).

### WeakMap

Let's demonstrate this on one simple example. In the example below you initialize two variables, `mapExample` and `weakMapExample`, using `Map` and `WeakMap`. After that, you add another variable `objExample` and initialize it as object with some key and value. Then, you use the `objExample` to add new pair into `mapExample` and `weakMapExample`.

Next is a quick check to see that you can access this pair, or rather the value part, in `mapExample` as well as `weakMapExample`. Following this check, you set the `objExample` to `null` so garbage collection can remove it from memory. Finally, you will again do a quick check to see if you can still access the value part.

As you can see, accessing the value using `get()` it correctly returns `undefined` for both, the `Map` (`mapExample`) as well as the `WeakMap` (`weakMapExample`). However, what if you try to iterate over the `Map` (`mapExample`) using `for...of` loop? You will still get the value and even the `objExample` object even after garbage collection did its job!

```
///
// Map and WeakMap example:
// Create new Map and WeakMap.
let mapExample = new Map()
let weakMapExample = new WeakMap()

// Create the objExample.
let objExample = {age: 'foo'}

// Output the content of objExample
console.log(objExample)
// [object Object] {
//   age: 'foo'
// }

// Add the objExample to Map and WeakMap
mapExample.set(objExample, 'foo')
weakMapExample.set(objExample, 'foo')

// Output the content of map and weakMap
for (let [key, value] of mapExample) {
  console.log(key)
  console.log(value)
}
// Outputs:
// [object Object] {
//   age: 'foo'
// }
// 'foo'

// Output the content of Map
console.log(mapExample.get(objExample))
// Outputs: 'foo'

// Output the content of WeakMap
console.log(weakMapExample.get(objExample))
// Outputs: 'foo'

// Set the objExample to null so garbage collection can remove it from memory.
objExample = null

// Output the content of objExample
console.log(objExample)
// Outputs: null

// !
// PAY ATTENTION HERE!
// The map still contains the, now removed, objExample!
// Output the content of Map
for (let [key, value] of mapExample) {
  console.log(key)
  console.log(value)
}
// Outputs:
// [object Object] {
//   age: 'foo'
// }
// 'foo'

// Output the content of Map
console.log(mapExample.get(objExample))
// Outputs: undefined

// Output the content of WeakMap
console.log(weakMapExample.get(objExample))
// Outputs: undefined
```

### WeakSet

Now, let's take the example with `Map` and `WeakMap` and rewrite it using `Set` and `WeakSet`. What if you try to check if the object exists inside the `Set` (`setExample`) and `WeakSet` (`weakSetExample`), using  `has()`? Before the removal, you will get `true`. Both, the `Set` (`setExample`) and `WeakSet` (`weakSetExample`) contain the object. When you try to iterate over the `Set` (`setExample`) using `forEach`, you will get the object and its content.

What will happen after the removal? Well, you will again correctly get `false` for the `Set` (`setExample`) as well as the `WeakSet` (`weakSetExample`). However, you try the `forEach` loop again you will again get the object and its content, even though the object itself no longer exists.

```
///
// Set and WeakSet example:
// Create new Set and WeakSet
let setExample = new Set()
let weakSetExample = new WeakSet()

let objExample = {name: 'bar'}

// Output the content of objExample
console.log(objExample)
// [object Object] {
//   name: 'bar'
// }

// Add the objExample to Set and WeakSet
setExample.add(objExample)
weakSetExample.add(objExample)

// Output the content of Set and weakSet
setExample.forEach(item => console.log(item))
// Outputs:
// [object Object] {
//   name: 'bar
// }

// Output the content of Set
console.log(setExample.has(objExample))
// Outputs: true

// Output the content of WeakSet
console.log(weakSetExample.has(objExample))
// Outputs: true

// Set the objExample to null so garbage collection can remove it from memory.
objExample = null

// Output the content of objExample
console.log(objExample)
// Outputs: null

// !
// PAY ATTENTION HERE!
// Output the content of Set
setExample.forEach(item => console.log(item))
// Outputs:
// [object Object] {
//   name: 'bar'
// }

// Output the content of Set
console.log(setExample.has(objExample))
// Outputs: false

// Output the content of WeakSet
console.log(weakSetExample.has(objExample))
// Outputs: false
```

### The differences between Map & WeakMap and Set & WeakSet

The `Map`, `WeakMap`, `Set` and `WeakSet` are interesting features of ES6. Aside to the names and how they handle garbage collection, there are other differences between these features. `Map` and `WeakMap` and `Set` and `WeakSet` are very similar in their differences. First, `WeakMap` and `WeakSet` keys can't be primitive types (string, number, boolean, null, undefined, symbol). `WeakMap` and `WeakSet` can store only objects.

Second, `WeakMap` and `WeakSet` keys also can't be created by an array or another set. Third, `WeakMap` and `WeakSet` don't provide any methods or functions that would allow you to work with the whole set of keys. Meaning, there is no `size` or `length` property and no `keys()`, `values()`, `entries()`, `forEach()` or `for...of`.

This is also why in the example above you saw `forEach` used only with `Set`, not with `WeakSet` and `for...of` only with `Map` but not with `WeakMap`. Fourth, `WeakMap` and `WeakSet` are not iterable.

## Export, import and modules

The `export` and `import` statements are probably one of the most used ES6 features among JavaScript developers. What these statements do is that they allow you to split your code into modules you can then export and import whenever you want or need. As a result, it will be much easier for you to keep your code clear of redundant repetitions.

### The import statement

Before you get your hands on these ES6 features there is something you need to know. You can't use `import` statement in embedded scripts by default. If you want to do so, you need to set its `type` attribute to "module". Another interesting thing on the `import` is that you can change the name of the imported export, or multiple, when you import it.

You can do so using `as`(`import foo as bar from 'module'`). You can also import all exports, or code, from a module using `*`. When you want to import one some exports from the module, you can do so by separating these exports with comma and wrapping them with curly braces (`import { exportOne, exportTwo } from 'module'`).

When you export something pay attention, and remember, to how you export it. Meaning, remember whether you exported that thing as a `default` export or not (or as "named"). This determines the `import` syntax you will need to use to import that export. If you export something as `default` export you don't use curly braces (`import defaulExport from 'module'`).

If you export something as "named" export, you have to use curly braces (`import { namedExport } from 'module'`). Two last things about using `import` statement you need to know and remember. First, don't wrap the name of the export, default or named, in quotes. Second, always wrap the name of the module, the file, you are importing the export from in quotes.

```
///
// Import example no.1: Basic syntax and importing named export
import { someNamedExport } from '/exampleModule.js'


///
// Import example no.2: Importing multiple named exports
import { foo, bar, bazz, gazz } from '/exampleModule.js'


///
// Import example no.3: Basic syntax and importing default export
import someDefaultExport from '/exampleModule.js'


///
// Import example no.4: Importing default and named export
import someDefaultExport, { someNamedExport } from '/exampleModule.js'


///
// Import example no.5: Importing named export and renaming it
import { someBadlyNamedNamedExportThatIsJustImpossibleToRemember as calc }
  from '/exampleModule.js'


///
// Import example no.6: Importing default export and renaming it
import someBadlyNamedDefaultExportThatIsJustImpossibleToRemember as fuzzy
  from '/exampleModule.js'


///
// Import example no.7: Importing multiple exports and renaming them
import { foo as bar, bazz as fuzzy, zazz as zizzy } from '/exampleModule.js'
```

### The export statement

You know how all you need about `import` statements. Now, let's briefly talk about the `export`. As I mentioned above, there are two types of exports, "default" and "named". As you now know, the type of export determines what syntax you use for import. Import with curly braces with "named" export and without curly braces with "default" export.

The rules about curly braces you learned about in the part about "named" and "default" `import` statements also apply to exports. When you want to export something as "default" you don't use curly braces. When you want to export it as "named" export you use curly braces.

Another important thing that distinguishes "default" and "named" is that you can have only one "default" export per module (file). You can't use "default" export to export multiple things. This limit doesn't apply to "named" exports. You can have as many "named" exports per module (file) as you want. Multiple exports must be separated by commas.

Next, when you want to export multiple things you can do it either individually or all at once. One last thing. What can you export? Basically anything. You can export variables, functions, classes, objects. The only limitation are probably primitives. Meaning, you can't import things such as string, number, booleans, etc. directly.

If you want to export some primitive data type, you have to declare it as a variable first. Then, you can export that variable. Finally, you can also rename the thing you want to export when you export it. This works similarly to importing. You again use `as` (`export foo as bar`).

```
///
// Export example no.1: Default export
const foo = 'Export me'

export default foo

// or
export default const foo = 'Export me'


///
// Export example no.2: Named export
const foo = 'Export me'

export { foo }

// or
export const foo = 'Export me'


///
// Export example no.3: Multiple individual exports
export const foo = 13
export const fizz = 'Another export'
export const bazzy = true


///
// Export example no.4: Multiple exports at once
const foo = 13
const fizz = 'Another export'
const bazzy = true

export { foo, fizz, bazzy }


///
// Export example no.5: Named and default exports
const foo = 'Default export'
const fizz = 'named export'
export foo, { fizz }

// or
export default const foo = 'Default export'

export const fizz = 'named export'
```

### Dynamic imports

The `import` and `export` statements introduced in ES6 are great features. However, there is already a small upgrade in the making. This currently exists only as a [stage 3 proposal]. You may be able to import modules dynamically, only and right at the time when you need them. You will basically import module on-demand and not by default. This will be allowed using "dynamic import", or `import()`.

For example, you can import a module only when user clicks on a specific button or link. Or, you can import whole page only when user clicks on specific navigation link. Otherwise, the module will not be loaded by the browser or app. This can help you significantly reduce the amount of resources the page or needs to load. And, as a result it can load much faster.

The best thing about dynamic import is that you can use it anywhere. You can use it in global scope, inside function or even inside statements such as `if else` or loops. How it works? Dynamic import always returns a `promise`. And, this promise always resolves to the module you want to import.

What's more, if you work with asynchronous code, or `async` functions, you can also combine dynamic imports with `await` operator. You will learn about `promise` and `async/await` in the next part of this series.

```
///
// Dynamic import example no.1:
const button = document.querySelector('.cta-btn')
const navLinkAbout = document.querySelector('.link-about')

// Attach eventListener to the button
button.addEventListener(() => {
  // import specific module when it is needed
  import('/some-module.js').then((module) => {
    // do something
  }).catch((error) => console.log(error))
})

// Attach eventListener to the navigation link
navLinkAbout.addEventListener(() => {
  // import About page module when user clicks on the navigation link
  import('/pages/page-about.js').then((module) => {
    // Load the page
  }).catch((error) => console.log(error))
})


///
// Dynamic import example no.2: Dynamic import and async/await
async function someCoolModuleLoader() {
  // Load module combining import with await
  let coolModule = await import('/cool-module.js')

  coolModule.greet() // Use greet() function from coolModule
  coolModule.default() // Use the default export
}
```

## Epilogue: ES6, ES7, ES8 & Writing Modern JavaScript Pt5

Congratulations! You've just finished another part of ES6, ES7, ES8 & Writing Modern JavaScript series! Today, you've learned everything you need about features `WeakMap`, `WeakSet` and `export` and `import` statements. Lastly, you've also learned about dynamic imports. Now, you can start using all these exciting features with absolute confidence.

In the next part learn about probably the most powerful and advanced ES6 features you can find. This includes features such as arrow functions, `classes`, `promises`, `async/await` and `generators`. So, get ready to take your knowledge of JavaScript to the highest level.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt1/
[Part 2]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt2/
[Part 3]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/
[Part 4]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt4/
[Sets]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt3/#sets
[Maps]: https://blog.alexdevero.com/es6-es7-es8-modern-javascript-pt4/#map-2
[garbage collected]: https://dzone.com/articles/memory-management-and-garbage-collection-in-javasc
[stage 3 proposal]: https://github.com/tc39/proposal-dynamic-import/#import

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
- https://webapplog.com/es6/
- https://zellwk.com/blog/es6/
- https://markpollmann.com/ES6/
- https://www.lifewire.com/best-javascript-es6-features-4579821
- https://github.com/lukehoban/es6features
- http://elliot.land/post/strong-vs-weak-references
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol
- https://stackoverflow.com/questions/43319924/whats-the-difference-between-es6-set-and-weakset
-->
