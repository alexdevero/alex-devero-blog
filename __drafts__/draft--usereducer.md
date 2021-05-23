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
