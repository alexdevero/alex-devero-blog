# Variable scope and Lexical Environment in JavaScript
<!--more-->
<!--
Table of Contents:
-->

## Variable scope

Every time you declare a variable or a function its visibility and accessibility is limited. There is one thing that determines this. It called a "scope", or "variable scope". This scope says where you can access specific variable and function and where you can't. In JavaScript, there are two types of scope, global and local scope.

### Global scope

When you declare variable outside any function or code block (`{ ... }`) it will be automatically in a global scope. For every JavaScript document, there is only one global scope. If you declare multiple variables or functions in a global scope, they will all end up at the same place.

Variable and functions declared in a global scope are usually called "global variables" and "global functions". When a variable or function is global it automatically becomes visible and accessible from anywhere. You can access it, reference it and modify.

```JavaScript
// Global variable:
var name = 'Jack'
let age = 37
const species = 'human'

// Global function:
function readName() {
  return name;
}

// Call the readName() function:
readName()
// Output:
// 'Jack'

// Global arrow function:
const readAge = () => age

// Call the readName() function:
readAge()
// Output:
// 37
```

### Local scope

Every function you declare creates its own local scope. Variables you declare inside this scope are local variables. These variables are visible and accessible only inside the scope, the function, at which you declared them. Trying to access them from the outside of the function, the local scope, will return an error.

Local variables exist only in their local scopes. They don't exist outside it. For this reason you can't access, reference or modify any local variable from the global scope. You can do so only inside the scope at which you declared them.

```JavaScript
// Declare a function to create a local scope:
function sayName() {
  // Local scope for this function.

  // Create local variable:
  const name = 'Dory'

  return name
}

// Call sayName() function:
sayName()
// Output:
// 'Dory'

// Try to access local "name" variable
// from a global scope.
console.log(name)
// Output:
// undefined
```

This also means that you can define multiple variables with the same name. These variables will not override each other as long as each is defined in a different local scope. Or, if one is declared in a global scope and the other in a local scope.

```JavaScript
// Create global variable:
let car = 'Tesla'

function createCar() {
  // Create local variable with the same name:
  let car = 'BMW'

  // Log the value of "car" variable:
  console.log(car)
}

// Call the createCar() function:
// This will read the "car" variable
// defined in a local scope (inside the function).
createCar()
// Output:
// 'BMW'

// Log the value of "car" variable:
// This will read the "car" variable
// defined in a global scope (outside the function).
console.log(car)
// Output:
// 'Tesla'
```


## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[]:

<!--
### Meta:
-
-->

<!--
### Keywords:
- Variable scope
-->

<!--
### Resources:
-
-->
