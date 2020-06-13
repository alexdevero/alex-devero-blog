# How to Build a [Todo List App] with React Hooks and TypeScript
The best way to learn something is by doing. This tutorial will help you learn how to build your own todo list app with React hooks and TypeScript. Try this easy tutorial, build your own todo list app, and get better in JavaScript, React and TypeScript.<!--more-->
<!--
Table of Contents:
## Briefing
## Project setup
## Interfaces
## Todo item component
## Todo list component
## Todo form component
## Main (index) component
### Imports
### Creating todo list app state
### Creating new todos
### Updating existing todos
### Removing existing todos
### Completing todos
### Ensuring every todo has title
### Returning all components
### Putting it all together
## Styles
## Conclusion: How to Build a Todo List App with React Hooks and TypeScript
-->

You can find the code on my [GitHub].

## Briefing

The goal for this tutorial is to build your own todo list app. About the app in general. This todo list app will have very simple interface and it will focus on the most important features, i.e. create, check off and delete todos. About code. You will use React and React hooks, mostly `useState` hook.

There will be one occasion where you will also use `useRef` hook. Since this todo list app will utilize React hooks for managing state there is no need to use class components. So, you will build this app only with [functional components]. When it comes to styling your todo list app, you will use external CSS stylesheets.

One last things. First every todo item will have a unique id. These ids will be generated when the todo item is created. You will use this id to mark the todo as complete or to remove it. To make this easier, while following good practices and avoiding using indexes, you will use [shortid] package.

## Project setup

As the first thing let's create the basic app for your todo list app. We can do this very fast with the help of [create-react-app]. You can use this package with `npm init react-app react-hooks-todo-list-app-ts --typescript`, `npx create-react-app react-hooks-todo-list-app-ts --typescript` or `yarn create react-app react-hooks-todo-list-app-ts --typescript`. If you don't want to use TypeScript, omit the `--typescript` flag at the end of the command.

These commands will create starting template for your todo list app, with workflow setup and almost all necessary dependencies. There is one dependency you will need to install manually, the `shortid` and types for this package. So, use `npm i shortid` and `npm i -D @types/shortid`, `yarn add shortid` and `yarn add -D @types/shortid` or `pnpm i shortid` and `pnpm i -D @types/shortid`.

There are some assets, such as React logo, that came with the app template. You can remove it because you will not need it. A very simple version of your `package.json` should look similar to this:

```json
{
  "name": "react-todo-list-hooks-ts",
  "version": "1.0.0",
  "description": "Simple Todo list app built with React hooks and TypeScript.",
  "browserslist": [
    ">0.2%",
    "not dead",
    "not ie <= 11",
    "not op_mini all"
  ],
  "main": "src/index.tsx",
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  },
  "dependencies": {
    "react": "16.11.0",
    "react-dom": "16.11.0",
    "shortid": "2.2.15"
  },
  "devDependencies": {
    "@types/react": "16.9.11",
    "@types/react-dom": "16.9.4",
    "@types/shortid": "^0.0.29",
    "react-scripts": "3.2.0",
    "typescript": "3.7.2"
  }
}
```

If you decide to use TypeScript, your `tsconfig` should look similar to this:

```json
{
    "include": [
        "./src/*"
    ],
    "compilerOptions": {
        "lib": [
            "dom",
            "es2015"
        ],
        "jsx": "react",
        "target": "es5",
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
        "noEmit": true
    }
}
```

As the last thing, below is the final structure of this todo list app project. You can use this as you work on this tutorial to orient yourself. With that, you are ready to start working on your todo list app.

```
react-meme-generator-ts/
├─node_modules
├─public
│ ├─favicon.ico
│ ├─index.html
│ ├─manifest.json
│ └─robots.txt
├─src
│ ├─components
│ │ ├─todo-form.tsx
│ │ ├─todo-item.tsx
│ │ └─todo-list.tsx
│ ├─styles
│ │ └─styles.css
│ ├─index.tsx
│ ├─interfaces.ts
│ └─react-app-env.d.ts
├─ package.json
└─ tsconfig.json
```

## Interfaces

The first thing to do is create [interfaces] for your todo list app. You will use them to define the shape of component `props` and the `todo` object, or to type them. If you decided to use pure JavaScript, instead of TypeScript, you can skip this step. You will need to create four interfaces.

One for todo (todo object), one for todo form one for todo list and one for todo item. The `todo` object will have three properties, `id`, `text`, `isCompleted`. The `TodoForm` props contain array of `todo` objects and `handleTodoCreate` method. The `TodoList` props will contain `handleTodoUpdate`, `handleTodoRemove`, `handleTodoComplete` and `handleTodoBlur` methods and array of `todo` objects.

The `TodoItem` props will contain `handleTodoUpdate`, `handleTodoRemove`, `handleTodoComplete`, `handleTodoBlur` and a single `todo` object.

```ts
// Todo interface
export interface TodoInterface {
  id: string;
  text: string;
  isCompleted: boolean;
}

// Todo form interface
export interface TodoFormInterface {
  todos: TodoInterface[];
  handleTodoCreate: (todo: TodoInterface) => void;
}

// Todo list interface
export interface TodoListInterface {
  handleTodoUpdate: (event: React.ChangeEvent<HTMLInputElement>, id: string) => void;
  handleTodoRemove: (id: string) => void;
  handleTodoComplete: (id: string) => void;
  handleTodoBlur: (event: React.ChangeEvent<HTMLInputElement>) => void;
  todos: TodoInterface[]
}

// Todo item interface
export interface TodoItemInterface {
  handleTodoUpdate: (event: React.ChangeEvent<HTMLInputElement>, id: string) => void;
  handleTodoRemove: (id: string) => void;
  handleTodoComplete: (id: string) => void;
  handleTodoBlur: (event: React.ChangeEvent<HTMLInputElement>) => void;
  todo: TodoInterface;
}
```

## Todo item component

The first component you will build will be todo item. When you add new todo on your todo list, this item component will represent it. This component will be composed of a couple of elements. First, there will be a `div` with `span` elements for checking off the todo. Unchecked item will contain empty span, styled into a transparent circle with border.

Checked off todo item will contain `span` with check mark HTML entity, inside a green circle. The wrapper `div` will have `onClick` handler to check/uncheck the todo. Next will be another `div` with `input`. You will use this `input` element to render the title, or the text, of the todo. This is the simplest way to make every todo item editable, through `input` elements.

You will pass the title be done through `value` attribute, from `todo` object passed through `props`. Aside to this, this `input` will have two handler methods, one for `onBlur` and one for `onChange`. The last element will be also a `div`, now with "x" entity/icon. You will use this element to remove the todo item.

This `div` will have one `onClick` handler. As all the previous data, and handler methods, this too will be passed thorough props.

If you use TypeScript, import the `TodoItemInterface` interface from `interfaces.ts` and to use it to type `props` of this component. After this, type the `onChange` handler on `input` element with `React.ChangeEvent<HTMLInputElement>` because we are attaching `onChange` handler to `input` element.

```tsx
// Import dependencies
import * as React from 'react'

// Import interfaces
import { TodoItemInterface } from './../interfaces'

// TodoItem component
const TodoItem = (props: TodoItemInterface) => {
  return (
    <div className='todo-item'>
      <div onClick={() => props.handleTodoComplete(props.todo.id)}>
        {props.todo.isCompleted ? (
          <span className="todo-item-checked">&#x2714;</span>
        ) : (
          <span className="todo-item-unchecked" />
        )}
      </div>

      <div className="todo-item-input-wrapper">
        <input
          value={props.todo.text}
          onBlur={props.handleTodoBlur}
          onChange={(event: React.ChangeEvent<HTMLInputElement>) => props.handleTodoUpdate(event, props.todo.id)}
        />
      </div>

      <div className="item-remove" onClick={() => props.handleTodoRemove(props.todo.id)}>
        &#x02A2F;
      </div>
    </div>
  )
}

export default TodoItem
```

## Todo list component

The todo list will be the second component you will create. This component will be very simple. This component will accept handler methods for the `TodoItem`, you've just created, and array of `todo` objects through `props`. The component itself will contain one `div` as a wrapper element.

Inside this `div` will be a list, one `ul` element. Inside this element, you will use `map()` to iterate over the array of `todo` objects, and create one `li` element with one `TodoItem` component for every `todo` object. You will then pass the individually `todo` objects to the `TodoItem` component, along with handler methods.

For TypeScript, remember to import `TodoListInterface` interface and use it to type the `props` of the `TodoList` component.

```tsx
// Import dependencies
import * as React from 'react'

// Import TodoItem
import TodoItem from './todo-item'

// Import interfaces
import { TodoListInterface } from './../interfaces'

// TodoList component
const TodoList = (props: TodoListInterface) => {
  return (
    <div className="todo-list">
      <ul>
        {props.todos.map((todo) => (
          <li key={todo.id}>
            <TodoItem
              todo={todo}
              handleTodoUpdate={props.handleTodoUpdate}
              handleTodoRemove={props.handleTodoRemove}
              handleTodoComplete={props.handleTodoComplete}
              handleTodoBlur={props.handleTodoBlur}
            />
          </li>
        ))}
      </ul>
    </div>
  )
}

export default TodoList
```

## Todo form component

The todo "form" will is the first component where you will use `useState` React hook. It is also here where you will use the `useRef` React hook. You will use the `useState` hook to store the text passed to the `input` element, text for the todo title before you will create new todo item.

You will use the `useRef` hook to store reference to this input. The way you create new todo is by pressing "Enter" key, while you type some text inside that input. So, when you press "Enter" key you will use this reference to reset the input, by setting the value to empty string. This input will also have two handler methods for `onChange` and `onKeyPress`.

These two handler methods will be `handleInputChange` and `handleInputEnter`. The first, for `onChange`, will update the form state when you write something into the input, some todo title/text. The second, for `onKeyPress`, will create new todo object and reset the input field when it detect pressing "Enter" key.

Do you remember the `shortid` package? It is here where you are going to use this dependency. Inside the `handleInputEnter` function, inside the new `todo` object, you will use `shortid` to generate unique `id` for every new todo. Don't worry. This will be simple. All you need is to call `generate()` on `shortid` and your new `id` is ready.

Lastly, few things for TypeScript. First, import `TodoInterface` and `TodoFormInterface` interfaces. Then, use the `TodoInterface` interface to type the new `todo` object inside `handleInputEnter`, and `TodoFormInterface` interface to type the `props` of `TodoForm`. Then, type the `useRef` hook, using `<HTMLInputElement>` and set it to `null`.

After that, there are also two events. For the first one, you can type it with `React.ChangeEvent<HTMLInputElement>` because we are attaching `onChange` handler to `input` element. For the second, you can type it with `React.KeyboardEvent` because we are "listening" for key press.

```tsx
// Import dependencies
import * as React from 'react'
import shortid from 'shortid'

// Import interfaces
import {TodoInterface, TodoFormInterface} from './../interfaces'

// Todo form component
const TodoForm = (props: TodoFormInterface) => {
  // Create ref for form input
  const inputRef = React.useRef<HTMLInputElement>(null)

  // Create form state
  const [formState, setFormState] = React.useState('')

  // Handle todo input change
  function handleInputChange(event: React.ChangeEvent<HTMLInputElement>) {
    // Update form state with the text from input
    setFormState(event.target.value)
  }

  // Handle 'Enter' in todo input
  function handleInputEnter(event: React.KeyboardEvent) {
    // Check for 'Enter' key
    if (event.key === 'Enter') {
      // Prepare new todo object
      const newTodo: TodoInterface = {
        id: shortid.generate(),
        text: formState,
        isCompleted: false
      }

      // Create new todo item
      props.handleTodoCreate(newTodo)

      // Reset the input field
      if (inputRef && inputRef.current) {
        inputRef.current.value = ''
      }
    }
  }

  return (
    <div className="todo-form">
      <input
        ref={inputRef}
        type="text"
        placeholder='Enter new todo'
        onChange={event => handleInputChange(event)}
        onKeyPress={event => handleInputEnter(event)}
      />
    </div>
  )
}

export default TodoForm
```

## Main (index) component

You are almost done. There is just one component you need to build. This is the main `TodoListApp` component. This component will implement methods for creating, updating, removing and completing your todos. This will be done via `handleTodoCreate`, `handleTodoUpdate`, `handleTodoRemove` and `handleTodoComplete` methods.

It is also this component where you will store all existing todos, using the `useState` React hook. So, let's build this component, step by step.

### Imports

First, as usually, you will need to import dependencies for `react`. Now, you will also need to import `render` method from `react-dom`. This is because you will render the `TodoListApp` component, your todo list app, in the DOM.

You will also import `TodoForm` and `TodoList` components so you can later return, and render, them. When you import these components you should also import the main external CSS stylesheet, so you can later style your todo list app.

For TypeScript, you will need to import the `TodoInterface` interface. You will use this interface a couple of times, to type `todos` state and some method parameters.

```tsx
// Import dependencies
import * as React from 'react'
import { render } from 'react-dom'

// Import components
import TodoForm from './components/todo-form'
import TodoList from './components/todo-list'

// Import interfaces
import { TodoInterface } from './interfaces'

// Import styles
import './styles/styles.css'
```

### Creating todo list app state

The state fo your todo list app will be simple. It will be an array of objects. One object will represent one existing todo. In the beginning, you will initialize the `todos` state as an empty array.

For TypeScript, make sure to use the `TodoInterface` interface along with `[]`. This will tell TypeScript you are "talking" about an array of todos objects, not just one todo object.

```tsx
// TodoListApp component
// ....
const TodoListApp = () => {
  const [todos, setTodos] = React.useState<TodoInterface[]>([])
  // ...
}
```

### Creating new todos

The first method for your todo list app will be method to create new todos, `handleTodoCreate` method. This method will accept one parameter, a `todo` object. The way it will work is simple. First, it will create new todo list app state, the `newTodosState`, by copying the current todo list app state.

Next, it will take the `todo` object, you pass as parameter when you call this method, and add that `todo` to the new todo list app state, the `newTodosState`, using `push()` method. After that, it will update the todo list app state, using `setTodos()` method.

About TypeScript. You will use the `TodoInterface` interface to type the `todo` parameter. You will also use this interface to type the `newTodosState` variable. In this case, you will again have specify you want an array of `todo` objects, adding `[]` after the `TodoInterface`.

```tsx
  // ....
  // Creating new todo item
  function handleTodoCreate(todo: TodoInterface) {
    // Prepare new todos state
    const newTodosState: TodoInterface[] = [...todos]

    // Update new todos state
    newTodosState.push(todo)

    // Update todos state
    setTodos(newTodosState)
  }
  // ....
```

### Updating existing todos

Next, you will need method to update existing todos, `handleTodoUpdate` method. This method will accept two parameters, `event` and `id`. The `id` will be unique `id` generated for every todo item/object. Similarly to `handleTodoCreate`, this method will also start by creating new todo list app state, `newTodosState`, by copying the current todo list app state.

Next, it will use `find()` method to iterate over the `newTodosState` variable and find the correct todo item to update, using the `id` passed as argument. When it finds the correct `todo` item/object, it will change the value of its `text` key. New `value` will come from the value of the input inside specific todo item.

The last step is updating the todo list app state, using `newTodosState` and `setTodos()` method.

For TypeScript, use the `TodoInterface` interface to type the `todo` parameter passed to `find()` method. Use it also for the `newTodosState` variable, along with `[]` after the `TodoInterface`. Lastly, type the `id` parameter as a `string`.

```tsx
  // ....
  // Update existing todo item
  function handleTodoUpdate(event: React.ChangeEvent<HTMLInputElement>, id: string) {
    // Prepare new todos state
    const newTodosState: TodoInterface[] = [...todos]

    // Find correct todo item to update
    newTodosState.find((todo: TodoInterface) => todo.id === id)!.text = event.target.value

    // Update todos state
    setTodos(newTodosState)
  }
  // ....
```

### Removing existing todos

Removing todos will be done using `filter()` method. First, you will create new todo list app state, `newTodosState`, by copying the current todo list app state. During this, you will use the `filter()` method to remove the todo you want to remove. This will be done by comparing `id` of all todos with the `id` of todo you want to remove.

When this is done, you will use this new, filtered, state to update the `todos` state with the `setTodos()` method.

For TypeScript, use the `TodoInterface` interface to type the `todo` parameter passed to `filter()` method. Then, use it also for the `newTodosState` variable, along with `[]` after the `TodoInterface`. Finally, type the `id` parameter as a `string`.

```tsx
  // ....
  // Remove existing todo item
  function handleTodoRemove(id: string) {
    // Prepare new todos state
    const newTodosState: TodoInterface[] = todos.filter((todo: TodoInterface) => todo.id !== id)

    // Update todos state
    setTodos(newTodosState)
  }
  // ....
```

### Completing todos

The method for completing todos will look very similar to `handleTodoUpdate` method. First, it will copy the current todo list app state and store it in `newTodosState` variable. Then, it will use `find()` method to find specific todo item/object in `todos` state.

This time, it will negate the value of `isCompleted` key of the specific todo item/object. After this, it will use the `setTodos` method to update `todos` state.

Now, about TypeScript. First, use the `TodoInterface` interface to type the `todo` parameter passed to `find()` method. Next, use this interface also for the `newTodosState` variable, again with `[]` after the `TodoInterface`. The last type will be for the `id`. This will be a `string`.

```tsx
  // ....
  // Check existing todo item as completed
  function handleTodoComplete(id: string) {
    // Copy current todos state
    const newTodosState: TodoInterface[] = [...todos]

    // Find the correct todo item and update its 'isCompleted' key
    newTodosState.find((todo: TodoInterface) => todo.id === id)!.isCompleted = !newTodosState.find((todo: TodoInterface) => todo.id === id)!.isCompleted

    // Update todos state
    setTodos(newTodosState)
  }
  // ....
```

### Ensuring every todo has title

The last thing. When you edit existing todo there should be some warning if you leave the text/title empty. To get this done you can watch change on `input` element inside every todo. Then, you can check its `value` is not an empty string, the `length` of the `value` is bigger than "0".

If there is an empty string, you will add specific CSS class. When you input some text, you will remove that CSS class. This CSS class will mark the input with red border. You will define this class in your CSS stylesheet later.

As usually, the TypeScript. This will be quick. All there is to type is the `event` passed as parameter. Since you are attaching a `onChange` event handler on `input` element, you can use `React.ChangeEvent<HTMLInputElement>`.

```tsx
  // ....
  // Check if todo item has title
  function handleTodoBlur(event: React.ChangeEvent<HTMLInputElement>) {
    if (event.target.value.length === 0) {
      event.target.classList.add('todo-input-error')
    } else {
      event.target.classList.remove('todo-input-error')
    }
  }
  // ....
```

### Returning all components

Your todo list app is almost finished. Now, you now need to take all the components you've built so far, and imported in component, and return them. Make sure to provide all components with necessary `props`. After that, you can use the `render()` method and render the `TodoListApp` in the DOM.

```tsx
  // ...
  return (
    <div className="todo-list-app">
      {/* Todo form component */}
      <TodoForm
        todos={todos}
        handleTodoCreate={handleTodoCreate}
      />

      {/* Todo list component */}
      <TodoList
        todos={todos}
        handleTodoUpdate={handleTodoUpdate}
        handleTodoRemove={handleTodoRemove}
        handleTodoComplete={handleTodoComplete}
        handleTodoBlur={handleTodoBlur}
      />
    </div>
  )
}

// Render the App in the DOM
const rootElement = document.getElementById('root')
render(<TodoListApp />, rootElement)
```

### Putting it all together

You wrote a lot code in this main component. Let's put it all together to make it more clear.

```tsx
// Import dependencies
import * as React from 'react'
import { render } from 'react-dom'

// Import components
import TodoForm from './components/todo-form'
import TodoList from './components/todo-list'

// Import interfaces
import { TodoInterface } from './interfaces'

// Import styles
import './styles/styles.css'

// TodoListApp component
const TodoListApp = () => {
  const [todos, setTodos] = React.useState<TodoInterface[]>([])

  // Creating new todo item
  function handleTodoCreate(todo: TodoInterface) {
    // Prepare new todos state
    const newTodosState: TodoInterface[] = [...todos]

    // Update new todos state
    newTodosState.push(todo)

    // Update todos state
    setTodos(newTodosState)
  }

  // Update existing todo item
  function handleTodoUpdate(event: React.ChangeEvent<HTMLInputElement>, id: string) {
    // Prepare new todos state
    const newTodosState: TodoInterface[] = [...todos]

    // Find correct todo item to update
    newTodosState.find((todo: TodoInterface) => todo.id === id)!.text = event.target.value

    // Update todos state
    setTodos(newTodosState)
  }

  // Remove existing todo item
  function handleTodoRemove(id: string) {
    // Prepare new todos state
    const newTodosState: TodoInterface[] = todos.filter((todo: TodoInterface) => todo.id !== id)

    // Update todos state
    setTodos(newTodosState)
  }

  // Check existing todo item as completed
  function handleTodoComplete(id: string) {
    // Copy current todos state
    const newTodosState: TodoInterface[] = [...todos]

    // Find the correct todo item and update its 'isCompleted' key
    newTodosState.find((todo: TodoInterface) => todo.id === id)!.isCompleted = !newTodosState.find((todo: TodoInterface) => todo.id === id)!.isCompleted

    // Update todos state
    setTodos(newTodosState)
  }

  // Check if todo item has title
  function handleTodoBlur(event: React.ChangeEvent<HTMLInputElement>) {
    if (event.target.value.length === 0) {
      event.target.classList.add('todo-input-error')
    } else {
      event.target.classList.remove('todo-input-error')
    }
  }

  return (
    <div className="todo-list-app">
      <TodoForm
        todos={todos}
        handleTodoCreate={handleTodoCreate}
      />

      <TodoList
        todos={todos}
        handleTodoUpdate={handleTodoUpdate}
        handleTodoRemove={handleTodoRemove}
        handleTodoComplete={handleTodoComplete}
        handleTodoBlur={handleTodoBlur}
      />
    </div>
  )
}

const rootElement = document.getElementById('root')
render(<TodoListApp />, rootElement)
```

## Styles

Your todo list app is ready to go. Well, almost. There is a lot of space for some styling. Here are some styles you can use to make your todo list app look better.

```css
/* Default styles*/
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

#root,
body {
  min-height: 100vh;
}

body {
  margin: 0;
}

#root,
.todo-list-app {
  display: flex;
  flex-flow: column nowrap;
}

#root {
  align-items: center;
  width: 100%;
}

/* Todo list app styles  */
.todo-list-app {
  padding-top: 32px;
  width: 100%;
  max-width: 480px;
}

/* Todo form styles */
.todo-form input,
.todo-item {
  border: 1px solid #ececec;
}

.todo-form input {
  padding: 0 14px;
  width: 100%;
  height: 48px;
  transition: .25s border ease-in-out;
}

.todo-form input:focus {
  outline: 0;
  border: 1px solid #3498db;
}

/* Todo list styles */
.todo-list ul {
  padding: 0;
  margin: 0;
}

.todo-list li {
  list-style-type: none;
}

/* Todo item styles */
.todo-item {
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  padding: 8px;
}

.todo-form + .todo-list ul .todo-item {
  border-top: 0;
}

.todo-item-input-wrapper {
  flex-grow: 1;
  padding: 0 16px;
}

.todo-item input {
  width: 100%;
  border: 0;
  border-bottom: 1px solid transparent;
  transition: .25s border-bottom ease-in-out;
}

.todo-item input:focus {
  outline: 0;
  border-bottom: 1px solid #3498db;
}

.todo-item .todo-input-error {
  border-bottom: 1px solid #e74c3c;
}

.todo-item span {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  border: 1px solid #ececec;
  transition: .25s all ease-in-out;
}

.todo-item-unchecked:hover {
  background: hsla(168, 76%, 42%, .25);
  border: 1px solid hsl(168, 76%, 42%, .25);
}

.todo-item-checked {
  color: #fff;
  background: #1abc9c;
  border: 1px solid #1abc9c;
}

.item-remove {
  display: flex;
  padding-left: 8px;
  padding-right: 8px;
  font-size: 28px;
  cursor: pointer;
  line-height: 1;
  color: #ececec;
  transition: .25s color ease-in-out;
}

.item-remove:hover {
  color: #111;
}
```

## Conclusion: How to Build a Todo List App with React Hooks and TypeScript

Congratulations, you've just built your own todo list app using React hooks and TypeScript! However, you don't have to stop here. So, go ahead. Take this todo list app and make it better. Think about what features you would like it to have. Then, don't wait for anything. Try to implement them by yourself. Have fun!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[GitHub]: https://github.com/alexdevero/react-hooks-todo-list-app-ts
[functional components]: https://reactjs.org/docs/components-and-props.html#function-and-class-components
[shortid]: https://www.npmjs.com/package/shortid
[TypeScript]: https://www.typescriptlang.org
[create-react-app]: https://github.com/facebook/create-react-app
[interfaces]: https://www.typescriptlang.org/docs/handbook/interfaces.html

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
