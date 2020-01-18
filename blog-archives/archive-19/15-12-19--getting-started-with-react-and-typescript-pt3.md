# Getting Started With React and TypeScript Pt.3 - Interfaces, Components & Hooks
Do you want to get started with React and TypeScript? This tutorial will help you learn about interfaces and how to use them with class and functional components. It will also help you learn how to annotate React hooks. Learn what you need to know to get started with React and TypeScript!<!--more-->
<!--
Table of Contents:
## Interfaces
### Optional properties
### Readonly properties
### Extending interfaces
### Exporting interfaces
### Interfaces and compilation
## Putting React and TypeScript together
### Class components
### Functional components
### Hooks
## Conclusion: Getting Started With React and TypeScript
-->

Getting Started With React and TypeScript [Part 1].

Getting Started With React and TypeScript [Part 2].

## Interfaces

In the [previous part], you've learned what types you can work with in React and TypeScript. You've also learned about [type inference] so you know when it is up to you to annotate your code and when TypeScript will do this work for you. One thing that can help you a lot are [interfaces].

Put simply, an `interface` is a object-like collection of types. It is used to describe the shape, or structure, of some data. This data can be anything, function parameters (objects and arrays), data inside data types, class props, state props and variables. Types in `interface` are structured in the form of key/value pairs.

In each pair, the `key` is the `property` that exists, or could exist, in the data you want to describe. The `value` is the data type of that `property`, specified as a `key`. The syntax of an `interface` will probably look familiar. It looks very similar to the syntax of [object literal]. There are few differences. First, `interface` has to start with `interface` keyword.

This keyword precedes the name of the `interface`. Second, there is no equal sign between the name of the `interface` and the collection of key/value pairs. Third, key/value pairs inside an `interface` can be separated either by commas (`,`) or by semicolons (`;`). Both will work. So, it depends on you which one you choose to use.

Fourth, in the terms of naming conventions, always start the name of the `interface` with capital letter, just like a class. Fifth, again some naming conventions, it is a good practice to end the name of the `interface` with "Interface" word.

Another practice is to start the name of the `interface` with "I" letter. This makes it clear what is interface and what is not. Let's take a look at some simple examples of interfaces.

```ts
///
// Create UserInterface
// interface is the keyword
// UserInterface is the name of the interface
interface UserInterface {
    name: string;
    age: number;
    isEmployed: boolean;
}

// Use UserInterface to annotate new 'user' object
const userOne: UserInterface = {
    name: 'Tony Smith',
    age: 23,
    isEmployed: false
}

const userTwo: UserInterface = {
    name: 'Bobby Stone',
    age: 28,
    isEmployed: true
}


///
// This will not work
// the 'age' property is required
const userThree: UserInterface = {
    name: 'Bobby Stone',
    // missing required age property here
    isEmployed: true
}
// Error: Property 'age' is missing in type '{ name: string; isEmployed: true; }' but required in type 'UserInterface'.


///
// Using interface with function
// Create interface for assingment
interface AssignentInterface {
    subject: string;
    lesson: string;
    chapter: number;
    time: string;
}

// Create function that accepts object as 'assignent' parameter
// Use AssignentInterface interface to annotate 'assignent' parameter
function study(assignent: AssignentInterface) {
    return `I will study ${assignent.subject}, lesson ${assignent.lesson}, chapter ${assignent.chapter} for ${assignent.time}.`
}

// Create some assignment data
const math = {
    subject: 'Mathematics',
    lesson: 'Trigonometry',
    chapter: 5,
    time: '45 minutes'
}

// Let's study
study(math)
// 'I will study Mathematics, chapter Trigonometry, exercise 5 for 45 minutes.'
```

### Optional properties

When you are not sure some `property` exist on the data you are describing you can also mark that `property` as optional. You can do this by adding `?` at the end of the property name (`property?: string`). This will tell TypeScript to expect this `property`, but it not require it.

So, if that optional property doesn't exist on the data, on which you used the `interface`, TypeScript will not complain and compile your code. Otherwise, it will show warning and will not let your code compile. So, remember, any `property` that is not optional is automatically required.

```ts
///
// Create CustomUserInterface interface
// with optional 'age' property
interface CustomUserInterface {
  username: string;
  age?: number; // this is optional (the '?' at the end of the property name)
}

// This will work because 'age' is optional, not required
const userOne: CustomUserInterface = {
  username: 'tomtom'
  // missing age property
}

// This will naturally work as well
const userTwo: CustomUserInterface = {
  username: 'tomtom'
  age: 23
}
```

### Readonly properties

In some cases, you might want to prevent change some properties after they are set for the first time. Interfaces allow this as well. All you have to do is add `readonly` word before the name of the property. Then, when you try to overwrite this property, after you assign it, TypeScript will warn you that the property is read-only.

```ts
///
// Create UserInterface with read-only property 'password'
interface UserInterface {
    username: string;
    readonly password: string; // This is read-only property ('readonly')
    // it can be modified only when the object is first created.
    age?: number; // This is optional property ('?')
}

// Create new user using UserInterface interface
let userOne: UserInterface = {
    username: 'tomtom',
    password: 'some very secret thing'
}

// Log userOne's username
console.log(userOne.username) 'tomtom'

// This will work:
// Try to change username property
userOne.username = 'buggy'
console.log(userOne.username) // 'buggy'

// ! This will not work
// Try to change read-only password property
userOne.password = 'another very secrert thing'
// Error: Cannot assign to 'password' because it is a read-only property.
```

### Extending interfaces

Interesting thing about `interface` is that you can also extend one `interface` with another, or more (separated by commas). This is similar to [JavaScript classes]. So, when one `interface` extends another that `interface` will inherit its shape. It will contain all key/value pairs and you can then add some more if you want.

```ts
///
// Create HumanInterface interface
interface HumanInterface {
    name: string;
    age: number;
    isAlive: boolean;
}

// Create MaleInterface interface that extends HumanInterface (inherits from it)
interface MaleInterface extends HumanInterface {
    gender: string;
}

// MaleInterface now looks like this:
// interface HumanInterface {
//     name: string; // inherited from HumanInterface
//     age: number; // inherited from HumanInterface
//     isAlive: boolean; // inherited from HumanInterface
//     gender: string; // Newly added
// }


///
// Extending multiple interfaces
interface FirstInterface {
    name: boolean;
}

interface SecondInterface {
    age: number;
}

interface ThirdInterface extends FirstInterface, SecondInterface {
    gender: string;
}

// ThirdInterface now looks like this:
// interface ThirdInterface {
//     name: boolean;
//     age: number;
//     gender: string;
// }
```

### Exporting interfaces

In ES6 and above, there is the option to use [export] and [import] statement to export and import snippets of your code. These two statements can be quite handy when you work with interfaces. You can put all interfaces in one file, export them and import them where you need them. This can help you keep your code organized.

It can also help you reduce the size of your codebase. You don't have to re-declare some interface over and over again just because some objects, or data, have the same shape. Instead, you can declare that interface once, export it, and import it any time, and at any place, you need it.

When you want to export some interface put the `export` keyword before the `interface` keyword during the declaration. When you want to import it somewhere and use it, use the `import` statement and correct name of the `interface`.

```ts
///
// ./interfaces/interfaces.ts

// Create AdminInterface and export it
export interface AdminInterface {}

// Create UserInterface and export it
export interface UserInterface {}


///
// ./index.ts
// Import AdminInterface and UserInterface interfaces
import { AdminInterface, UserInterface } from './interfaces/interfaces'

// use AdminInterface interface
let newAdmin: AdminInterface

// use UserInterface interface
let newUser: UserInterface
```

### Interfaces and compilation

One important thing about interfaces. Interfaces will not show when you compile your React and TypeScript, or just TypeScript, code to JavaScript. TypeScript uses interfaces only for type checking during the runtime and compilation. However, TypeScript will not compile them. So, you don't have to worry your JavaScript will get bloated. It will not.

```ts
///
// TypeScript
// Create FirstInterface interface
interface FirstInterface {
    name: string;
    age: number;
    isEmployed: boolean;
}

// Create SecondInterface interface
interface SecondInterface {
    subject: string;
    points: number;
}

// Create ThirdInterface interface
interface ThirdInterface {
    title: string;
    pubDate: Date;
    author: string;
}

// Declare variable using FirstInterface interface
let userData: FirstInterface

// Declare variable using SecondInterface interface
let boardData: SecondInterface

// Declare variable using ThirdInterface interface
let blogData: ThirdInterface
```

The whole code above will compile to these few lines:

```js
///
// Compiled JavaScript
"use strict";
let userData;
let boardData;
let blogData;
```


## Putting React and TypeScript together

You know about what types are available in TypeScript. You also know about interfaces and how to use them annotate your code. Now, let's take a look at how to use React and TypeScript together. Let's take a look at how to properly annotate class and functional components and hooks.

### Class components

Class components are no longer used as often as they once were. However, they are still used in React. So, it is still good to know how to write them in projects built with React and TypeScript. With classes, there are two options for types. You can provide the class with types for `props` and for `state`.

When you declare new class, types for `props` and for `state` go between the brackets that follow after the `extends React.Component` and before opening curly bracket. Remember that it is in this exact order. Types for `props` are always first and types for `state` second. You can also, optionally, annotate the class `state` itself.

When you want to leave one of the types empty, you can add empty object inside the curly brackets instead of the interface object. If you don't want to use interfaces, you can also provide the types for `prop` and `state` directly, through the objects inside brackets.

```tsx
///
// Create interface for class component props
interface PropsInterface {
  heading: string;
}

// Create interface for class component state
interface StateInterface {
  firstName: string;
  lastName: string;
}

// Create new class
// use PropsInterface and StateInterface interfaces (<Props, State>)
class MyApp extends React.Component<PropsInterface, StateInterface> {
  // This state annotation is optional
  // it is for better type inference
  state: StateInterface = {
    firstName: 'Andrew',
    lastName: 'Coboll'
  }

  render() {
    return (
      <div>
        {this.props.heading} {this.state.firstName} {this.state.lastName}
      </div>
    )
  }
}


///
// Or, class with constructor
class MyApp extends React.Component<PropsInterface, StateInterface> {
  // Declare state property and annotate it with StateInterface
  state: StateInterface

  // Add constructor and annotate props with PropsInterface
  constructor(props: PropsInterface) {
    super(props)
      this.state = {
        firstName: 'Andrew',
        lastName: 'Coboll'
    }
  }

  render() {
    return (
      <div>
        {this.props.heading} {this.state.firstName} {this.state.lastName}
      </div>
    )
  }
}


///
// Class with types only for props
// Replace the interface for state with empty object
class MyApp extends React.Component<PropsInterface, {}> { ... }


///
// Class with types only for state
// Replace the interface for props with empty object
class MyApp extends React.Component<{}, StateInterface> { ... }


///
// Class with types, without interface - one prop, one state prop
class MyApp extends React.Component<{ classProp: string }, { stateProp: boolean }> {}


// Class with types, without interface - multiple props, multiple state props
class MyApp extends React.Component<{
  propOne: number; // Props types
  propTwo: string; // Props types
}, {
  statePropOne: boolean; // State types
  statePropTwo: number; // State types
}> { ... }
```

### Functional components

Annotating functions is even easier than classes since there is no state and, as is in older JS, no constructor. You declare your functional component as you would normally. If it accepts some `props`, you use interface to annotate these `props`. Or, you can also annotate `props` directly.

```tsx
///
// Create interface for functional component
interface PropsInterface {
  propOne: string;
  propTwo: string;
}

// Create functional component
// and use PropsInterface interface
// to annotate its props
function MyComponent(props: PropsInterface) {
  return (
    <div>{props.propOne} {props.propTwo}</div>
  )
}

// Arrow function version
const MyComponent = (props: PropsInterface) => {
  return (
    <div>{props.propOne} {props.propTwo}</div>
  )
}


///
// Annotate props directly - one prop
function MyComponent(props: string) {
    return (
        <div>{props.propOne} {props.propTwo}</div>
    )
}

// Arrow function version
const MyComponent = (props: string) => {
    return (
        <div>{props.propOne} {props.propTwo}</div>
    )
}


///
// Annotate props directly - multiple props
function MyComponent(props: {
    propOne: string;
    propTwo: string;
}) {
    return (
        <div>{props.propOne} {props.propTwo}</div>
    )
}

// Arrow function version
const MyComponent = (props: {
    propOne: string;
    propTwo: string;
}) => {
    return (
        <div>{props.propOne} {props.propTwo}</div>
    )
}
```

### Hooks

Annotating hooks is very easy. If you initialize a hook with some default value TypeScript will infer its type for you. So, you don't have to anything. If you initialize without a value you can add its type inside brackets right after the name of the hook and before the parenthesis (i.e. `React.useState<type>()`).

Let's take a look at examples of the three most popular hooks, `useState`, `useRef` and `useReducer`.

Example of `useState` hook:

```tsx
///
// Initialize useState hook with default value
const MyComponent = () => {
  const [name, setName] = React.useState('') // Will be inferred as string

  // or
  const [name, setName] = React.useState('Tom') // Will be inferred as string

  const [age, setAge] = React.useState(15) // Will be inferred as number

  const [isHappy, setIsHappy] = React.useState(true) // Will be inferred as boolean

  const [skills, setSkills] = React.useState(['Programming', 'Drawing']) // Will be inferred as an array

  // or
  const [skills, setSkills] = React.useState([]) // Will be inferred as an array

  const [customerData, setCustomerData] = React.useState({ firstName: 'Tom', lastName: 'Smith' }) // Will be inferred as an object

  // or
  const [customerData, setCustomerData] = React.useState({}) // Will be inferred as an object
}


///
// Initialize useState hook without default value
const MyComponent = () => {
  const [name, setName] = React.useState<string>() // set type to string

  const [age, setAge] = React.useState<number>() // set type to number

  const [isHappy, setIsHappy] = React.useState<boolean>() // set type to boolean

  const [skills, setSkills] = React.useState<[]>() // set type to array

  const [skills, setSkills] = React.useState<{}>() // set type to object
}
```

Example of `useRef` hook:

```tsx
const MyComponent = () => {
  // Initialize ref with null value
  // and tell TypeScript the type of the HTML element
  let textInputRef = React.useRef<HTMLInputElement>(null)

  // Initialize ref for form element
  let formRef = React.useRef<HTMLFormElement>(null)

  const handleTextSave = () => {
    // Make sure textInputRef input exists
    if (textInputRef & textInputRef.current) {
      // Get value of textInputRef input
      const inputValue = textInputRef.current.value
    }
  }

  return (
    {/* Use ref for form initialized above */}
    <form ref={formRef}>
      <label>Your name:</label>

      <input
        type="text"
        defaultValue=""
        ref={textInputRef}{/* Use textInputRef ref initialized above */}
      />

      <button onClick={handleTextSave}>Save</button>
    </form>
  )
}
```

Example of `useReducer` hook:

```tsx
// Create interface for app state
interface AppStateInterface {}

// Create interface for reducer actions
interface ActionInterface {
  type: 'ACTION_ONE' | 'ACTION_TWO';
  payload: string | boolean;
}

// Create reducer function
// use AppStateInterface and ActionInterface
// to annotate state and action parameters
// and set return type to AppStateInterface (reducer( ... ): AppStateInterface) { ... })
export function reducer(state: AppStateInterface, action: ActionInterface): AppStateInterface {
  switch (action.type) {
    case 'ACTION_ONE':
      return {
        ...state,
        one: action.payload // payload is string
      }
    case 'ACTION_TWO':
      return {
        ...state,
        two: action.payload // payload is boolean
      }
    default:
      return state
  }
}
```

## Conclusion: Getting Started With React and TypeScript

Congratulations! You've just finished the third part of getting started with React and TypeScript tutorial. Today you've learned what are interfaces and how to use them. You've also learned how to annotate class and functional components and the three most popular hooks properly.

Now,take what you've learned today and apply it. For example, give it a try and build your first app with React and TypeScript from scratch. Or, take existing React project and rewrite it using React and TypeScript. Whatever you choose, just make sure to do something with what you've learned. Otherwise, you will forget most of it.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/react-and-typescript-pt1/
[Part 2]: https://blog.alexdevero.com/react-and-typescript-pt2/
[previous part]: https://blog.alexdevero.com/react-and-typescript-pt2/#types
[type inference]: https://blog.alexdevero.com/react-and-typescript-pt2/#type-inference
[interfaces]: https://www.typescriptlang.org/docs/handbook/interfaces.html
[object literal]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Object_literals
[JavaScript classes]: https://blog.alexdevero.com/javascript-classes-pt1/#class-inheritance-extends
[export]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export
[import]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import

<!--
#### Meta:
-
-->
