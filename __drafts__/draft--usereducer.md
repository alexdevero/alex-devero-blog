# Blog post title [...]
The React useReducer hook is a very good alternative to useState when you need to manage complex states with multiple values. In this tutorial, you will learn about this React hook. You will learn about how useReducer hook works. You will also learn how to use it to manage state.
<!--more-->
<!--
Table of Contents:
-->

## A quick introduction to React useReducer hook

The useReducer hook is quite similar to [useState hook]. Like the useState hook, it also allows you to manage state of your React applications. The advantage of useReducer is that it makes it easier to work with complex states. By complex state I mean state with multiple sub-values, an object with key-value pairs.

The useReducer hook makes this easier by using more structural approach. That said, this doesn't mean that you should useReducer hook only to deal with such states. You can useReducer just as well with simple states that contain single primitive value. The way useReducer hook works is simple.

It uses two pieces of data, state and reducer function. The reducer is a pure function that takes a state and an action. The actions tells the reducer what you want it to do. What is the update you want to do to the state. For example, increment number, decrement number, push new value to array, etc.

Reducer function takes these inputs, applies the action you specified, and returns a new state value. This new state value is an updated version of the state you provided it with. Something to remember. Reducer should not change the old one directly. About the syntax.

### A note on pure functions

About "pure" functions. A function is pure when it follows two rules. First, the function always returns the same output if you pass in the same arguments. Second, the function does not produce any side-effects. This means that the function has no effect on its surroundings.

Put simply, the function doesn't work with the outside world. It works only with inputs you passed into it. A simple example of pure function can be a function that takes two numbers as parameters and returns their sum. If you pass in the same numbers, you will get the same result. This confirms the first rule.

The function doesn't do anything with the code outside it. It works solely with those two numbers it gets as input. This confirms the second rule. We can say that the function is pure. Now, let's say that the function stores the result in an outside variable. In this case, the function is not pure because it breaks the second rule.

When the function has an effect on outside world it is not pure. Changing variables outside it is such an effect. It would also not be pure if it logged the result or some message. These logs are also side-effects and thus break the second rule.

## The syntax of useReducer hook

The useReducer hook accepts three parameters. First two parameters are required. These two are the `reducer` and `state`. The `reducer` is the reducer function we discussed above. The `state` is any initial state value. This is the same initial state you know from working with `useState` hook.

Aside to these two, the useReducer hooks also accepts third, optional parameter. This parameter is `initializer`. This `initializer` allows you to initialize the state lazily with a function. The result returned by this function becomes the initial state value.

This can be useful when you want to create initial state but it involves some expensive operation, to generate the initial data. Just remember that React will invoke the initializer function only after the initial render, not after subsequent re-renders. That said, you will probably not need it as often.

The useReducer hook will return two things, or values. First is the current state. The second is a dispatch function. This function allows you to update the state you passed to the useReducer hook.

```jsx
// useReducer hook syntax:
const [state, dispatch] = useReducer(reducer, initialState, init)
```

## Initial state

Before you can start using the useReducer hook you need two things, initial state and reducer function. Let's start with the initial state. Initial state can be anything from primitive data type to object. Whatever fits you current situation. What you have to do is to create this state somewhere, and assign it to a variable.

```JavaScript
// A simple initial state object:
const initialState = {
  name: '',
  email: '',
  role: '',
  isActive: false,
}
```

## Reducer function

The second thing is the reducer function. The reducer function accepts two parameters: the state and action. It takes these two and updates the state, based on the action dispatched. It is very common to create the structure of reducer function, and handle each action, with [switch statement].

The main reason is that switch is usually more readable than `if...else` statement. Especially when you work with multiple actions. That said, if you prefer `if...else` statement go ahead and use that. About the structure. The reducer has to have a `case`, or if block, for each action you want to use to update the state.

Each of these actions should do two things. First, it should copy the current state. Reducer is a pure function. It is not supposed to change the existing state. What it does instead is it creates copies of it and works with them. It is common to create copies of old state by spread the old, using [spread].

The second thing reducer will do for each case, or block, is updating specific state value with the new value. Put together, it will basically copy the old state and overwrite only the values that should be updated. After that, it will return the new state. Aside to this there should be also a `default` case or else block.

This case or block can do two things. First, it can return the original state unchanged. Second, it can throw an error about non-existing action. Similarly to initial state, you define the reducer as a function somewhere in your code. Don't pass it to the reducer as a whole.

```JavaScript
// Create reducer function:
const reducer = (state, action) => {
  // Create switch to handle all actions:
  switch (action.type) {
    case 'SET_NAME':
      // Handle 'SET_NAME' action:
      return {
        ...state, // Copy the old state.
        name: action.payload // Update relevant value.
      }
    case 'SET_EMAIL':
      // Handle 'SET_EMAIL' action:
      return {
        ...state, // Copy the old state.
        email: action.payload // Update relevant value.
      }
    case 'SET_ROLE':
      // Handle 'SET_ROLE' action:
      return {
        ...state, // Copy the old state.
        role: action.payload // Update relevant value.
      }
    case 'SET_IS_ACTIVE':
      // Handle 'SET_IS_ACTIVE' action:
      return {
        ...state, // Copy the old state.
        isActive: action.payload // Update relevant value.
      }
    default:
      // Throw an error when none of cases matches the action.
      throw new Error('Unexpected action')
  }
}
```

## Action, type and payload

In the reducer function example you could see `action.type` and `action.payload`. This is because when you update the state with dispatch function returned by the useReducer hook you pass in an object. This object contains two keys, `type` and `payload`. The `type` tell reducer function what action you want to make.

Reducer function then uses this information, the `type`, to use one of the `switch` cases, or if blocks. The `payload` is where you put the new value for the state. These two names are not mandatory. They are just a common practice among React developers. You can use any names you want. Just make sure to use correct names in your reducer.

```JavaScript
// Dispatched object example to set name:
dispatch({
  type: 'SET_NAME',
  payload: 'Victor'
})

// Dispatched object example to set role:
dispatch({
  type: 'SET_ROLE',
  payload: 'Admin'
})

// Dispatched object example to set isActive:
dispatch({
  type: 'SET_IS_ACTIVE',
  payload: true
})
```

## Putting it all together

You have the initial state and reducer function. Now, you can use them with the useReducer hook and let the hook handle state management for you. The process is simple. Call the useReducer hook and pass in the reducer function and initial state, in this order. This will return the `state` and `dispatch` function.

When you want to update specific state value you use the `dispatch` function. You call this function passing an object as an argument. This is the `action`. This object will contain two keys, `type` and `payload` (or any names you chose). The `type` must match one of the `switch` cases in your reducer function.

The value of payload is the value you want to update the state with. It is the new value you want to store in the state. The `state` value returned by the useReducer hook will always give you the latest values of the state. This is just like when you use useState hook. In this case, the `state` is still the same. The state updater function is the `dispatch`.

```jsx
// Import useReducer hook from React:
import { useReducer } from 'react'

// Create initial state:
const initialState = {
  name: '',
  email: '',
  role: '',
  isActive: false,
}

// Create reducer function:
const reducer = (state, action) => {
  // Create switch to handle all actions:
  switch (action.type) {
    case 'SET_NAME':
      // Handle 'SET_NAME' action:
      return {
        ...state, // Copy the old state.
        name: action.payload // Update relevant value.
      }
    case 'SET_EMAIL':
      // Handle 'SET_EMAIL' action:
      return {
        ...state, // Copy the old state.
        email: action.payload // Update relevant value.
      }
    case 'SET_ROLE':
      // Handle 'SET_ROLE' action:
      return {
        ...state, // Copy the old state.
        role: action.payload // Update relevant value.
      }
    case 'SET_IS_ACTIVE':
      // Handle 'SET_IS_ACTIVE' action:
      return {
        ...state, // Copy the old state.
        isActive: action.payload // Update relevant value.
      }
    default:
      // Throw an error when none of cases matches the action.
      throw new Error('Unexpected action')
  }
}

// Create simple component:
export default function App() {
  // Call useReducer hook, passing in
  // previously created reducer function
  // and initial state:
  const [state, dispatch] = useReducer(reducer, initialState)

  return (
    <div className="App">
      {/*
        Create input for "name" and use dispatch
        to update "name" state value on input change.
      */}
      <input
        type="text"
        name="name"
        value={state.name}
        onChange={(event) => dispatch({
          type: 'SET_NAME', // Dispatch 'SET_NAME' action.
          payload: event.target.value // Set input value as payload.
        })}
      />

      {/*
        Create input for "email" and use dispatch
        to update "email" state value on input change.
      */}
      <input
        type="email"
        name="email"
        value={state.email}
        onChange={(event) => dispatch({
          type: 'SET_EMAIL', // Dispatch 'SET_EMAIL' action.
          payload: event.target.value // Set input value as payload.
        })}
      />

      {/*
        Create select for selecting "role" and use dispatch
        to update "role" state value on select change.
      */}
      <select
        onChange={(event) => dispatch({
          type: 'SET_ROLE', // Dispatch 'SET_ROLE' action.
          payload: event.target.value // Set input value as payload.
        })}
      >
        <option value="" selected></option>
        <option value="Admin">Admin</option>
        <option value="User">User</option>
        <option value="guest">Guest</option>
      </select>

      {/*
        Create checkbox for isActive and use dispatch
        to update "isActive" state value on checkbox change.
      */}
      <label>
        <input
          type="checkbox"
          checked={state.isActive}
          onChange={(event, checked) => dispatch({
            type: 'SET_IS_ACTIVE', // Dispatch 'SET_IS_ACTIVE' action.
            payload: checked // Set checkbox checked value as payload.
          })}
        />
        Is active?
      </label>
    </div>
  )
}
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
-
-->

<!--
### Resources:
-
-->
