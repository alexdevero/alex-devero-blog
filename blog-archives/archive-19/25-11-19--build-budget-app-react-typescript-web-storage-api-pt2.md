# How to Build a [Budget App] With React, Typescript & Web Storage API Pt.2
Learning React and TypeScript doesn't have to be hard or boring. It can be fun. This tutorial will show you how to build your own simple budget app using React and TypeScript. It will also show you how to use Web Storage API to make data in your web app persistent.<!--more-->
<!--
Table of Contents:
## BudgetItemAdd component
## BudgetTotal component
## Settings page
## Homepage
### Handling recalculation of paid budget
### Handling local/session storage
### Changing items
### Adding new item
### Removing existing items
### Returning the HomePage component
### Putting it all together
## Setting up app router
### Handling initial render
### Updating items when storage method changes
### Updating settings
### Creating app router
### Putting it all together
## Rendering budget app
## Styles
## Conclusion: How to build a budget app with React, TypeScript & Web Storage API
-->

How to Build a Budget App With React, Typescript & Web Storage API [Part 1].

You can find the code on my [GitHub] (_make sure you are on "blog-tutorial" branch_).

## BudgetItemAdd component

The `BudgetItemAdd` component will allow to add new item on the list in your budget app. This component will be a modal dialog accessible from the main screen. At the top will be component states for `date`, `title`, `price` and `isPaid`, created with `useReact` React hook. These states will get value from `input` elements.

These inputs will be wrapped inside `form` element. Your budget app will use a `handleFormSubmit` function to handle this form. This function will take the values of `date`, `title`, `price` and `isPaid` states, generate unique `id` using `shortid` and call `handleAddItem` function, passed via `props`, passing all previous data as an argument.

After this function is called the budget app will automatically reset all local states. It will do so by setting them to their initial values. Then, it will use `handleShowAddItem` function, passed via `props`, to automatically close the modal dialog.

```tsx
// components/budget-item-add

// Import react & shortid
import * as React from 'react'
import shortid from 'shortid'

// Import interface
import { BudgetItemAddInterface } from './../interfaces'

// BudgetItemAdd component
const BudgetItemAdd = (props: BudgetItemAddInterface) => {
  // Prepare BudgetItemAdd states
  const [date, setDate] = React.useState('')
  const [title, setTitle] = React.useState('')
  const [price, setPrice] = React.useState(0)
  const [isPaid, setIsPaid] = React.useState(false)

  function handleFormSubmit(event: React.FormEvent<HTMLFormElement>) {
    // Prevent form from submitting
    event.preventDefault()

    // Create new item
    props.handleAddItem({
      date: date,
      title: title,
      price: price,
      isPaid: isPaid,
      id: shortid.generate()
    })

    // Reset form state
    setDate('')
    setTitle('')
    setPrice(0)
    setIsPaid(false)

    // Close modal window
    props.handleShowAddItem(!props.showAddItem)
  }

  return (
    <div className="modal-wrapper">
      <div className="modal-dialog">
        <button className="btn btn-cross" onClick={() => props.handleShowAddItem(!props.showAddItem)}>&#x02A2F;</button>

        <form onSubmit={handleFormSubmit}>
          <fieldset>
            {/* Date the item was added */}
            <label htmlFor="date">Date of payment:</label>

            <input
              type="date"
              id="date"
              value={date}
              onChange={(event) => setDate(event.target.value)}
              required={true}
            />
          </fieldset>

          <fieldset>
            {/* Title of the item */}
            <label htmlFor="title">Item name:</label>

            <input
              type="text"
              id="title"
              value={title}
              onChange={(event) => setTitle(event.target.value)}
              required={true}
            />
          </fieldset>

          <fieldset>
            {/* Price of the item */}
            <label htmlFor="price">Item price:</label>

            <input
              type="number"
              id="price"
              value={price}
              onChange={(event) => setPrice(parseInt(event.target.value, 10))}
              min="0"
              step="1"
              required={true}
            />
          </fieldset>

          <fieldset>
            {/* Mark as paid */}
            <input
              className="custom-checkbox-checkbox"
              type="checkbox"
              id="isPaid"
              checked={isPaid}
              onChange={() => setIsPaid(!isPaid)}
            />

            <label className="custom-checkbox-label" htmlFor="isPaid"> Item is already paid</label>
          </fieldset>

          <fieldset>
            <input
              className="btn btn-add"
              type="submit"
              value="+ Add item"
            />
          </fieldset>
        </form>
      </div>
    </div>
  )
}

export default BudgetItemAdd
```

## BudgetTotal component

The `BudgetTotal` component will display the budget period, budget amount and budget currency, all selected in app settings. The budget will be shown either as positive (green colored) or negative (red colored). We will determine which one to show by subtracting the currently paid budget from the total budget amount.

If currently paid budget, the sum of the price of all items checked as paid, is bigger than the total budget amount it means we've already spent our whole budget. Otherwise, we are still within the budget. The `BudgetTotal` component will get all these data from `props`.

```tsx
// components/budget-total

// Import react
import * as React from 'react'

// Import interface
import { BudgetTotalInterface } from './../interfaces'

// BudgetTotal component
const BudgetTotal = (props: BudgetTotalInterface) => {
  return (
    <div className="budget-total">
      <h2>
        <span className="budget-period">Your {props.budgetPeriod}</span>
        {' '}
        <span className="budget-label">budget:</span>
        {' '}
        <span
          className={`budget-total ${props.budgetAmount - props.budgetPaid > 0 ? 'budget-total-positive' : 'budget-total-negative'}`}>
          {props.budgetAmount - props.budgetPaid}
        </span>
        {' '}
        <span className="budget-currency">{props.budgetCurrency}</span>
      </h2>
    </div>
  )
}

export default BudgetTotal
```

## Settings page

The settings is the place where you will be able to set or change budget period, currency and size. Change of any of these settings will automatically propagate through the whole budget app. All necessary logic, functions and data, will be passed via `props`. This will make this component very simple.

There will be only `input` or `select` elements for every settings option, along with `label` and wrapped inside a `fieldset`. The budget period will have three options, "Daily", "Monthly" and "Yearly". You will use `select` element to render this element. The size will be represented in the form of `input` type `number`.

The option for preferred storage method will be also represented by `select` element. This `select` will also have three options, "None", "Local storage" and "Session storage". For the currency option, you will use `input` with `datalist`. The `datalist` will be generated by from `currencyCodes` array stored `in data/currency-codes.ts`.

You will take this array, iterate over it with `map()` and return `option` element for every currency code. This will create `datalist` with around 167 options of currency code you can choose from. All form elements will have handler functions, listening for `onChange` event, that will pass values to the main app state, in `AppRouter` component.

Every `input` elements will use current settings data from main app store as values for `defaultValue` attribute. These data will be passed to the `SettingsPage` component via `props`. This will ensure all `input` elements will always reflect the current settings.

Last thing. Since all changes are applied automatically there is no need for saving button. You can add a note about automatic saving.

```tsx
// pages/settings.tsx

// Import react & Link from react-router-dom
import * as React from 'react'
import { Link } from 'react-router-dom'

// Import interface
import { SettingsPageInterface } from './../interfaces'

// Import data for currency codes
import currencyCodes from './../data/currency-codes'

// SettingsPage component
const SettingsPage = (props: SettingsPageInterface) => (
  <div>
    <header>
      <h2>Settings</h2>

      <Link className="btn btn-cross btn-unstyled" to="/">&#x02A2F;</Link>
    </header>

    <fieldset>
      <label htmlFor="period">Budget period:</label>

      <select
        onChange={(event) => props.setBudgetPeriod(event.target.value)}
        name="period"
        id="period"
        defaultValue={props.budgetPeriod}
      >
        <option value="daily">Daily</option>
        <option value="monthly">Monthly</option>
        <option value="yearly">Yearly</option>
      </select>
    </fieldset>

    <fieldset>
      <label htmlFor="currency">Budget currency:</label>

      <input
        onChange={(event) => props.setBudgetCurrency(event.target.value)}
        name="currency"
        id="currency"
        defaultValue={props.budgetCurrency}
        list="currencyCodes"
      />

      <datalist id="currencyCodes">
        {currencyCodes.map(code => <option key={code} value={code} />)}
      </datalist>
    </fieldset>

    <fieldset>
      <label htmlFor="budget">Budget size:</label>

      <input
        onChange={(event) => props.setBudgetAmount(parseInt(event.target.value, 10))}
        type="number"
        name="budget"
        id="budget"
        defaultValue={props.budgetAmount}
      />
    </fieldset>

    <fieldset>
      <label htmlFor="storage">Preferred storage method:</label>

      <select
        onChange={(event) => props.setStorageMethod(event.target.value)}
        name="storage"
        id="storage"
        defaultValue={props.storageMethod}
      >
        <option value="none">None</option>
        <option value="local">Local storage</option>
        <option value="session">Session storage</option>
      </select>
    </fieldset>

    <p><small><em>* All changes are saved automatically.</em></small></p>
  </div>
)

export default SettingsPage
```

## Homepage

In the case of homepage, you will start with importing almost all component you have created so far, the `BudgetTotal`, `BudgetList`, `BudgetItemAdd` and `IconSettings`. Next, as usually, you will also import interfaces used in `HomePage` component `BudgetItemObjInterface` and `HomePageInterface`.

The next thing to do is creating states, with the help of `useState` React hook. You will need two, one for paid budget (`budgetPaid`, a number) and one for showing the add item (`showAddItem`, a boolean). When `showAddItem` is set to `true` the `BudgetItemAdd` modal window will be shown.

```tsx
// pages/home.tsx

// Import react & Link
import * as React from 'react'
import { Link } from 'react-router-dom'

// Import components
import BudgetTotal from './../components/budget-total'
import BudgetList from './../components/budget-list'
import BudgetItemAdd from './../components/budget-item-add'
import IconSettings from './../components/icon-settings'

// Import interfaces
import { BudgetItemObjInterface, HomePageInterface } from './../interfaces'

const HomePage = (props: HomePageInterface) => {
  // Prepare homepage states
  const [budgetPaid, setBudgetPaid] = React.useState(0)
  const [showAddItem, setShowAddItem] = React.useState(false)
  // ...
}
```

### Handling recalculation of paid budget

Next, let's use `useEffect` hook to calculate the paid budget. Inside this hook, you will iterate over all items on the list, stored in `budgetItems` state. It will take the price of each item and add it to the total costs, or money spent. Then, it will update `budgetPaid` state with the value of total costs.

Two things to explain. First, I suggest you use `forEach()` loop to iterate over `budgetItems` state, instead of `map()`. The way `map()` [works] is that it builds a new array and returns it. Or, it can return something for each item in the array. You don't want, or need, to return anything.

All you need is just doing a simple calculation. Adding the price of the item to the total costs. What's more, you need to do this calculation only when item has been paid, it is checked off. Otherwise, you want the `forEach()` to ignore the item. So, not only there is nothing to return. In some cases, there will be nothing to do at all.

The second thing is the `[props.budgetItems]` dependency array, at the end of the `useEffect` hook. This will cause two things. First, this hook will be triggered when the `HomePage` component mounts, on the initial render. Second, this hook will be also triggered when the `budgetItems` prop, passed via `props`, changes.

So, every time you add, update or remove an item from `budgetItems` budget app will recalculate the total budget.

```tsx
  // ...
  // Recalculate total budget
  React.useEffect(() => {
    // Prepare total costs
    let costs = 0

    // Iterate over items and add their prices to total costs
    props.budgetItems.forEach((item: BudgetItemObjInterface) => {
      // Add prices only of item that have been paid
      if (item.isPaid) {
        costs += item.price
      }
    })

    // Update budgetPaid state
    setBudgetPaid(costs)
  }, [props.budgetItems]) // Watch 'budgetItems' state for changes
  // ...
```

### Handling local/session storage

Next, you will create function to handle local, or session, storage. This function will have two parameters. One will be `task`. This will be either "get" or "update". "get" will load data from storage and "update" will save data, and overwrite any existing. The second parameter will be `newState`, this is the array of items on the list.

This function will always first check the current settings for preferred storage method, if it is "local" or "session". If it is "none" it will do nothing. Next, it will check the value passed as first argument, type of the task to do. If it is "update" and preferred storage method is "local" it will take the data passed as second argument and create new item in `localStorage`.

If there are any existing data stored in the same item, it will update them, overwrite them. If the type of task is "get" and preferred storage method is "local" it will check `localStorage` and retrieve any existing data. Then, it will update `budgetItems` state with data extracted from `localStorage`.

If the preferred method is "session" this function will do the same operations, but it will use `sessionStorage`.

```tsx
  // ...
  // Handle local/session storage
  function handleStorage(task: 'get' | 'update', newState: BudgetItemObjInterface[]) {
    if (props.storageMethod === 'local') {
      if (task === 'update') {
        // Overwrite items in localStorage
        window.localStorage.setItem('budget-app', JSON.stringify(newState))
      } else {
        // If there are any data in sessionStorage
        if (window && window.localStorage && window.localStorage.getItem('budget-app')) {
          // Extract the data from localStorage
          const recoveredLocalData = window.localStorage.getItem('budget-app')

          // If there data to be recovered
          if (recoveredLocalData) {
            // Update budgetItems state
            props.setBudgetItems(JSON.parse(recoveredLocalData))
          }
        }
      }
    } else if (props.storageMethod === 'session') {
      if (task === 'update') {
        // Overwrite items in sessionStorage
        window.sessionStorage.setItem('budget-app', JSON.stringify(newState))
      } else {
        // If there are any data in sessionStorage
        if (window && window.sessionStorage && window.sessionStorage.getItem('budget-app')) {
          // Extract the data from sessionStorage
          const recoveredSessionData = window.sessionStorage.getItem('budget-app')

          // If there data to be recovered
          if (recoveredSessionData) {
            // Update budgetItems state
            props.setBudgetItems(JSON.parse(recoveredSessionData))
          }
        }
      }
    }
  }
  // ...
```

### Changing items

To make changing data inside items easier you will create function that will be a bit universal. It will have three parameters, value to use, id of the item to update and what property inside the item to update. This function will use `switch`, and `itemProperty` passed as argument, to decide which property to change, `isPaid`, `price` or `title`.

It will use the `id` passed as argument, along with `find()` method, to find the correct item to update. When it finds the correct item, it will use the `value`, passed as argument, and update the correct property in that item. Then, it will update `budgetItems` state and call `handleStorage` to update local or session storage.

```tsx
  // ...
  // Handle change of items
  function handleItemUpdate(value: string, id: string, itemProperty: string) {
    // Prepare new budgetItems state
    const newBudgetItemsState: BudgetItemObjInterface[] = [...props.budgetItems]

    // Decide which property to update
    switch (itemProperty) {
      case 'isPaid':
        // Find 'isPaid' property and update it with new value
        newBudgetItemsState.find((item: BudgetItemObjInterface) => item.id === id)!.isPaid = !newBudgetItemsState.find((item: BudgetItemObjInterface) => item.id === id)!.isPaid
        break
      case 'price':
        // Find 'price' property and update it with new value
        newBudgetItemsState.find((item: BudgetItemObjInterface) => item.id === id)!.price = parseInt(value, 10)
        break
      case 'title':
        // Find 'title' property and update it with new value
        newBudgetItemsState.find((item: BudgetItemObjInterface) => item.id === id)!.title = value
        break
    }

    // Update budgetItems state
    props.setBudgetItems(newBudgetItemsState)

    // Update local/session storage
    handleStorage('update', newBudgetItemsState)
  }
  // ...
```

### Adding new item

Function for adding new item on the list in your budget app will have one parameter, `itemToAdd`. First, it will copy the current `budgetItems` state. Next, it will extract data from `itemToAdd` passed as argument. Then, it will update `budgetItems` state and also call `handleStorage` to update local or session storage.

```tsx
  // ...
  // Handle adding new item
  function handleAddItem(itemToAdd: BudgetItemObjInterface) {
    // prepare new budgetItemsState
    const newBudgetItemsState = [...props.budgetItems]

    // Add new item to newBudgetItemsState
    newBudgetItemsState.push({
      date: itemToAdd.date,
      isPaid: itemToAdd.isPaid,
      price: itemToAdd.price,
      title: itemToAdd.title,
      id: itemToAdd.id
    })

    // Update budgetItems state
    props.setBudgetItems(newBudgetItemsState)

    // Update local/session storage
    handleStorage('update', newBudgetItemsState)
  }
  // ...
```

### Removing existing items

Function for removing items will be short. It will have one parameter, `id` of the item to remove. It will use `filter()` method to iterate over `budgetItems` state and remove the item with `id` that matches `id` passed as argument. After that, it will update `budgetItems` state and call `handleStorage` to update local or session storage.

```tsx
  // ...
  // Handle removing existing items
  function handleItemRemove(id: string) {
    // Find & remove correct budget item
    let newBudgetItemsState =  props.budgetItems.filter((item: BudgetItemObjInterface) => item.id !== id)

    // Update budgetItems state
    props.setBudgetItems(newBudgetItemsState)

    // Update local/session storage
    handleStorage('update', newBudgetItemsState)
  }
  // ...
```

### Returning the HomePage component

The last thing. You will create, and return, structure for `HomePage` component. It will start with `header` that will contain `BudgetTotal` component and link to settings page. Next, outside the `header`, will be `BudgetList` component followed by conditionally rendered `BudgetItemAdd` component and button to show this component. With this, `HomePage` component for your budget app is complete.

```tsx
  //  ...
  return (
    <div>
      <header>
        {/* Remaining budget */}
        <BudgetTotal
          budgetPeriod={props.budgetPeriod}
          budgetCurrency={props.budgetCurrency}
          budgetAmount={props.budgetAmount}
          budgetPaid={budgetPaid}
        />

        {/* Link to settings page/component */}
        <Link className="btn btn-settings" to="/settings">
          <IconSettings />
        </Link>
      </header>

      {/* List with all items */}
      <BudgetList
        budgetCurrency={props.budgetCurrency}
        budgetItems={props.budgetItems}
        handleItemUpdate={handleItemUpdate}
        handleItemRemove={handleItemRemove}
      />

      {/* Component for adding new item */}
      {showAddItem && (
        <BudgetItemAdd
          showAddItem={showAddItem}
          handleShowAddItem={setShowAddItem}
          handleAddItem={handleAddItem}
        />
      )}

      {/* Button to show component for adding new item */}
      <button
        className="btn btn-add"
        onClick={() => setShowAddItem(!showAddItem)}
      >+ <span className="btn-label">Add item</span></button>
    </div>
  )
}
```

### Putting it all together

When put together, this is how the code for `HomePage` component will look like:

```tsx
// pages/home.tsx

// Import react & Link
import * as React from 'react'
import { Link } from 'react-router-dom'

// Import components
import BudgetTotal from './../components/budget-total'
import BudgetList from './../components/budget-list'
import BudgetItemAdd from './../components/budget-item-add'
import IconSettings from './../components/icon-settings'

// Import interfaces
import { BudgetItemObjInterface, HomePageInterface } from './../interfaces'

// HomePage component
const HomePage = (props: HomePageInterface) => {
  // Prepare homepage states
  const [budgetPaid, setBudgetPaid] = React.useState(0)
  const [showAddItem, setShowAddItem] = React.useState(false)

  // Recalculate total budget
  React.useEffect(() => {
    // Prepare total costs
    let costs = 0

    // Iterate over items and add costs to total costs
    props.budgetItems.forEach((item: BudgetItemObjInterface) => {
      if (item.isPaid) {
        costs += item.price
      }
    })

    // Update budgetPaid state
    setBudgetPaid(costs)
  }, [props.budgetItems]) // Watch 'budgetItems' state for changes

  // Handle local/session storage
  function handleStorage(task: 'get' | 'update', newState: BudgetItemObjInterface[]) {
    if (props.storageMethod === 'local') {
      if (task === 'update') {
        // Overwrite items in localStorage
        window.localStorage.setItem('budget-app', JSON.stringify(newState))
      } else {
        // If there are any data in sessionStorage
        if (window && window.localStorage && window.localStorage.getItem('budget-app')) {
          // Extract the data from localStorage
          const recoveredLocalData = window.localStorage.getItem('budget-app')

          // If there data to be recovered
          if (recoveredLocalData) {
            // Update budgetItems state
            props.setBudgetItems(JSON.parse(recoveredLocalData))
          }
        }
      }
    } else if (props.storageMethod === 'session') {
      if (task === 'update') {
        // Overwrite items in sessionStorage
        window.sessionStorage.setItem('budget-app', JSON.stringify(newState))
      } else {
        // If there are any data in sessionStorage
        if (window && window.sessionStorage && window.sessionStorage.getItem('budget-app')) {
          // Extract the data from sessionStorage
          const recoveredSessionData = window.sessionStorage.getItem('budget-app')

          // If there data to be recovered
          if (recoveredSessionData) {
            // Update budgetItems state
            props.setBudgetItems(JSON.parse(recoveredSessionData))
          }
        }
      }
    }
  }

  // Handle change of items
  function handleItemUpdate(value: string, id: string, itemProperty: string) {
    // Prepare new budgetItems state
    const newBudgetItemsState: BudgetItemObjInterface[] = [...props.budgetItems]

    switch (itemProperty) {
      case 'isPaid':
        // Find 'isPaid' property and update it with new value
        newBudgetItemsState.find((item: BudgetItemObjInterface) => item.id === id)!.isPaid = !newBudgetItemsState.find((item: BudgetItemObjInterface) => item.id === id)!.isPaid
        break
      case 'price':
        // Find 'price' property and update it with new value
        newBudgetItemsState.find((item: BudgetItemObjInterface) => item.id === id)!.price = parseInt(value, 10)
        break
      case 'title':
        // Find 'title' property and update it with new value
        newBudgetItemsState.find((item: BudgetItemObjInterface) => item.id === id)!.title = value
        break
    }

    // Update budgetItems state
    props.setBudgetItems(newBudgetItemsState)

    // Update local/session storage
    handleStorage('update', newBudgetItemsState)
  }

  // Handle adding new item
  function handleAddItem(payload: BudgetItemObjInterface) {
    // prepare new budgetItemsState
    const newBudgetItemsState = [...props.budgetItems]

    // Add new item to newBudgetItemsState
    newBudgetItemsState.push({
      date: payload.date,
      isPaid: payload.isPaid,
      price: payload.price,
      title: payload.title,
      id: payload.id
    })

    // Update budgetItems state
    props.setBudgetItems(newBudgetItemsState)

    // Update local/session storage
    handleStorage('update', newBudgetItemsState)
  }

  // Handle removing existing items
  function handleItemRemove(id: string) {
    // Find & remove correct budget item
    let newBudgetItemsState =  props.budgetItems.filter((item: BudgetItemObjInterface) => item.id !== id)

    // Update budgetItems state
    props.setBudgetItems(newBudgetItemsState)

    // Update local/session storage
    handleStorage('update', newBudgetItemsState)
  }

  return (
    <div>
      <header>
        <BudgetTotal
          budgetPeriod={props.budgetPeriod}
          budgetCurrency={props.budgetCurrency}
          budgetAmount={props.budgetAmount}
          budgetPaid={budgetPaid}
        />

        <Link className="btn btn-settings" to="/settings"><IconSettings /></Link>
      </header>

      <BudgetList
        budgetCurrency={props.budgetCurrency}
        budgetItems={props.budgetItems}
        handleItemUpdate={handleItemUpdate}
        handleItemRemove={handleItemRemove}
      />

      {showAddItem && (
        <BudgetItemAdd
          showAddItem={showAddItem}
          handleShowAddItem={setShowAddItem}
          handleAddItem={handleAddItem}
        />
      )}

      <button
        className="btn btn-add"
        onClick={() => setShowAddItem(!showAddItem)}
      >+ <span className="btn-label">Add item</span></button>
    </div>
  )
}

export default HomePage
```

## Setting up app router

It is time to build the app router, the most important part of your budget app. First, you will need to import few components from `react-router-dom` library, namely `BrowserRouter`, `Switch` and `Route`. You will use these components to create router for your budget app.

Next, import `HomePage` and `SettingsPage` components, and `BudgetItemObjInterface` interface. You will use the `HomePage` and `SettingsPage` components, with `Switch` and `Route`, to specify which page should be rendered on what URL, or path. Next, you will create states for budget items, period, currency, amount and storage method.

You've worked with these data throughout the budget app. In those case, these data were passed through `props`. They were all passed from here, the app router. This is here where the "central" state of our budget app is. It is also here where you can set the default values for app settings. So, feel free to change those values.

```tsx
// app-router.tsx

// Import react & BrowserRouter, Switch, Route from react-router-dom
import * as React from 'react'
import { BrowserRouter, Switch, Route } from 'react-router-dom'

// Import pages
import HomePage from './pages/home'
import SettingsPage from './pages/settings'

// Import interface
import { BudgetItemObjInterface } from './interfaces'

// AppRouter component
const AppRouter = () => {
  // Prepare default app states
  const [budgetItems, setBudgetItems] = React.useState<BudgetItemObjInterface[]>([]) // Default settings values
  const [budgetPeriod, setBudgetPeriod] = React.useState('monthly') // Default settings values
  const [budgetCurrency, setBudgetCurrency] = React.useState('USD') // Default settings values
  const [budgetAmount, setBudgetAmount] = React.useState(2500) // Default settings values
  const [storageMethod, setStorageMethod] = React.useState('none') // Default settings values
  // ...
```

### Handling initial render

Every time the `AppRouter` component mounts, when you refresh the window, the app will do two things. First, it will check if there are any settings stored either in `localStorage` or `sessionStorage`. If there are any it will recover them. It will extract the settings data from the storage and update the `budgetPeriod`, `budgetCurrency`, `budgetAmount` and `storageMethod` states.

The second thing is that it will do the same for items. If there are any existing items stored in `localStorage` or `sessionStorage` it will recover them. It will extract the items data from the storage and update `budgetItems` state. You will do this using `useEffect` hook.

To execute this only on the initial render, you will need to add empty dependency array to the end of the `useEffect` hook. Without this empty array the `useEffect` hook would be triggered on every render and every update.

Now, when you refresh your browser your budget app will automatically recover all existing data. Well, only if you set preferred method set to either "local" or "session". If you set it to "None", all data will be lost on refresh.

```tsx
  // ...
  // Restore settings & items from local/session storage if any exists
  React.useEffect(() => {
    // Check if there are any existing data for settings in sessionStorage
    if (window && window.sessionStorage && window.sessionStorage.getItem('budget-app-settings') !== null && window.sessionStorage.getItem('budget-app-settings')!.length > 0) {
      // Get data from sessionStorage
      const recoveredSettings = window.sessionStorage.getItem('budget-app-settings')

      // If storage contains any data process them
      if (recoveredSettings) {
        // Get all recovered state data
        const { oldBudgetPeriod, oldBudgetCurrency, oldBudgetAmount, oldStorageMethod } = JSON.parse(recoveredSettings)

        // Update all settings
        setBudgetPeriod(oldBudgetPeriod)
        setBudgetCurrency(oldBudgetCurrency)
        setBudgetAmount(oldBudgetAmount)
        setStorageMethod(oldStorageMethod)
      }
    } else if (window && window.localStorage && window.localStorage.getItem('budget-app-settings') !== null && window.localStorage.getItem('budget-app-settings')!.length > 0) {
      // Of if there are any existing data for settings in localStorage
      // Get data from localStorage
      const recoveredSettings = window.localStorage.getItem('budget-app-settings')

      // If storage contains any data process them
      if (recoveredSettings) {
        // Get all recovered state data
        const { oldBudgetPeriod, oldBudgetCurrency, oldBudgetAmount, oldStorageMethod } = JSON.parse(recoveredSettings)

        // Update all settings
        setBudgetPeriod(oldBudgetPeriod)
        setBudgetCurrency(oldBudgetCurrency)
        setBudgetAmount(oldBudgetAmount)
        setStorageMethod(oldStorageMethod)
      }
    }

    // Check if there are any existing data for items in sessionStorage
    if (window && window.sessionStorage && window.sessionStorage.getItem('budget-app') !== null && window.sessionStorage.getItem('budget-app')!.length > 0) {
      // Get items data from sessionStorage
      const recoveredItems = window.sessionStorage.getItem('budget-app')

      // If there are any items to be recovered
      if (recoveredItems) {
        // Extract recovered items data
        const { oldItems } = JSON.parse(recoveredItems)

        // Update budgetItems state
        setBudgetItems(oldItems)
      }
    } else if (window && window.localStorage && window.localStorage.getItem('budget-app') !== null && window.localStorage.getItem('budget-app')!.length > 0) {
      // Of if there are any existing data for items in localStorage
      // Get items data from localStorage
      const recoveredItems = window.localStorage.getItem('budget-app')

      // If there are any items to be recovered
      if (recoveredItems) {
        // Extract recovered items data
        const { oldItems } = JSON.parse(recoveredItems)

        // Update budgetItems state
        setBudgetItems(oldItems)
      }
    }
  }, [])// Run on initial render
  // ...
```

### Updating items when storage method changes

Next, let's take care of updating items when storage method changes. When you change the storage method, the budget app will automatically check the current preferred method and save all items on your list in local or session storage. After that, it will remove data in other storages, but not in your preferred.

If you choose "None" as your preferred storage method, it will remove data in both, local and also session, storages. All this will be done using `useEffect` hook. This hook will be triggered when either `budgetItems` or `storageMethod` changes.

```tsx
  // ...
  // Update items if budgetItems or storageMethod changes
  React.useEffect(() => {
    if (storageMethod === 'session') {
      // Save items to sessionStorage
      window.sessionStorage.setItem('budget-app', JSON.stringify({
        oldItems: budgetItems
      }))

      // Remove duplicate data in localStorage
      window.localStorage.removeItem('budget-app')
    } else if (storageMethod === 'local') {
      // Save items to localStorage
      window.localStorage.setItem('budget-app', JSON.stringify({
        oldItems: budgetItems
      }))

      // Remove duplicate data in sessionStorage
      window.sessionStorage.removeItem('budget-app')
    } else if (storageMethod === 'none') {
      // Remove all previous data from both storages
      window.localStorage.removeItem('budget-app')
      window.sessionStorage.removeItem('budget-app')
    }
  }, [budgetItems, storageMethod])// Watch budgetItems & storageMethod props
  // ...
```

### Updating settings

If you use "local" or "session" storage method, the budget app will also automatically save, or backup, settings data in appropriate storage. Similarly to the previous hook, this one will also check your preferred storage method.

If it is "local" or "session" it will save all current settings in appropriate storage. It will also remove existing settings data in the other storage. If you choose "None", it will again clear settings data in both storages.

To make sure all settings are saved, this `useEffect` hook will be triggered every time either budget period, currency, amount or storage method changes. To do this it will watch `budgetPeriod`, `budgetCurrency`, `budgetAmount` and `storageMethod` states.

```tsx
  // ...
  // Update settings if budgetPeriod, budgetCurrency, budgetAmount or storageMethod changes
  React.useEffect(() => {
    if (storageMethod === 'session') {
      // Save settings to sessionStorage
      window.sessionStorage.setItem('budget-app-settings', JSON.stringify({
        oldBudgetPeriod: budgetPeriod,
        oldBudgetCurrency: budgetCurrency,
        oldBudgetAmount: budgetAmount,
        oldStorageMethod: storageMethod
      }))

      // Remove duplicate data in localStorage
      window.localStorage.removeItem('budget-app-settings')
    } else if (storageMethod === 'local') {
      // Save settings to localStorage
      window.localStorage.setItem('budget-app-settings', JSON.stringify({
        oldBudgetPeriod: budgetPeriod,
        oldBudgetCurrency: budgetCurrency,
        oldBudgetAmount: budgetAmount,
        oldStorageMethod: storageMethod
      }))

      // Remove duplicate data in sessionStorage
      window.sessionStorage.removeItem('budget-app-settings')
    } else if (storageMethod === 'none') {
      // Remove all previous data from both storages
      window.localStorage.removeItem('budget-app-settings')
      window.sessionStorage.removeItem('budget-app-settings')
    }
  }, [budgetPeriod, budgetCurrency, budgetAmount, storageMethod])// Watch budgetPeriod, budgetCurrency, budgetAmount & storageMethod props
  // ...
```

### Creating app router

The last thing, wiring the app router. Now, you will specify which page should be rendered on what URL. To do so you will first create `BrowserRouter` component. The `BrowserRouter` is the parent component that is used to store all of your `Route` components. The `Route` components tell your app which components it is supposed to render based on specific route.

The route is defined through `path` attribute. You can specify what component you want to render in two ways. First, you can pass the component name to `component` attribute on `Router` component (`<Route path="/foo" component={Foo}>`). Second, you can render the component as a child component of the `Router` component.

For now, let's use the second way. You will create two `Routes` components, one for homepage and one for settings page. The `Route` for homepage will have `path` set to "/", root route. For this route, you also need to add `exact` attribute and set it to `true`.

Without this parameter the route would be render on all routes that match or contain the "/". So, on all routes. The `exact` attribute set to `true` will ensure component for homepage will be rendered only when the URL exactly matches "/", without any extra characters.

The `Route` for settings page will have `path` set to "/settings". Since there are no other routes that could collide with "/settings" route there is no need to use `exact` attribute. Next step is adding correct page component as a child for correct `Router` component.

The last step is wrapping the `Route` components inside `Switch` component. This will make sure the app will render only the first child `Route` its `path` matches the URL. You can learn more about all these components in [React Router docs].

```tsx
  // ...
  return (
    <div className="app">
      <BrowserRouter>
        <Switch>
          {/* Add homepage */}
          <Route path="/" exact={true}>
            <HomePage
              budgetItems={budgetItems}
              setBudgetItems={setBudgetItems}
              budgetAmount={budgetAmount}
              budgetPeriod={budgetPeriod}
              budgetCurrency={budgetCurrency}
              storageMethod={storageMethod}
            />
          </Route>

          {/* Add settings */}
          <Route path="/settings">
            <SettingsPage
              budgetPeriod={budgetPeriod}
              budgetCurrency={budgetCurrency}
              budgetAmount={budgetAmount}
              storageMethod={storageMethod}
              setBudgetPeriod={setBudgetPeriod}
              setBudgetCurrency={setBudgetCurrency}
              setBudgetAmount={setBudgetAmount}
              setStorageMethod={setStorageMethod}
            />
          </Route>
        </Switch>
      </BrowserRouter>
    </div>
  )
}
```

### Putting it all together

Now, let's put all the snippets above together. This is how the `AppRouter` will look like:

```tsx
// app-router.tsx

// Import react & BrowserRouter, Switch, Route from react-router-dom
import * as React from 'react'
import { BrowserRouter, Switch, Route } from 'react-router-dom'

// Import pages
import HomePage from './pages/home'
import SettingsPage from './pages/settings'

// Import interface
import { BudgetItemObjInterface } from './interfaces'

// AppRouter component
const AppRouter = () => {
  // Prepare default app states
  const [budgetItems, setBudgetItems] = React.useState<BudgetItemObjInterface[]>([])
  const [budgetPeriod, setBudgetPeriod] = React.useState('monthly')
  const [budgetCurrency, setBudgetCurrency] = React.useState('USD')
  const [budgetAmount, setBudgetAmount] = React.useState(2500)
  const [storageMethod, setStorageMethod] = React.useState('none')

  // Restore settings & items from local/session storage if any exists
  React.useEffect(() => {
    // Check if there are any existing data for settings in sessionStorage
    if (window && window.sessionStorage && window.sessionStorage.getItem('budget-app-settings') !== null && window.sessionStorage.getItem('budget-app-settings')!.length > 0) {
      // Get data from sessionStorage
      const recoveredSettings = window.sessionStorage.getItem('budget-app-settings')

      // If storage contains any data process them
      if (recoveredSettings) {
        // Get all recovered state data
        const { oldBudgetPeriod, oldBudgetCurrency, oldBudgetAmount, oldStorageMethod } = JSON.parse(recoveredSettings)

        // Update all settings
        setBudgetPeriod(oldBudgetPeriod)
        setBudgetCurrency(oldBudgetCurrency)
        setBudgetAmount(oldBudgetAmount)
        setStorageMethod(oldStorageMethod)
      }
    } else if (window && window.localStorage && window.localStorage.getItem('budget-app-settings') !== null && window.localStorage.getItem('budget-app-settings')!.length > 0) {
      // Of if there are any existing data for settings in localStorage
      // Get data from localStorage
      const recoveredSettings = window.localStorage.getItem('budget-app-settings')

      // If storage contains any data process them
      if (recoveredSettings) {
        // Get all recovered state data
        const { oldBudgetPeriod, oldBudgetCurrency, oldBudgetAmount, oldStorageMethod } = JSON.parse(recoveredSettings)

        // Update all settings
        setBudgetPeriod(oldBudgetPeriod)
        setBudgetCurrency(oldBudgetCurrency)
        setBudgetAmount(oldBudgetAmount)
        setStorageMethod(oldStorageMethod)
      }
    }

    // Check if there are any existing data for items in sessionStorage
    if (window && window.sessionStorage && window.sessionStorage.getItem('budget-app') !== null && window.sessionStorage.getItem('budget-app')!.length > 0) {
      // Get items data from sessionStorage
      const recoveredItems = window.sessionStorage.getItem('budget-app')

      // If there are any items to be recovered
      if (recoveredItems) {
        // Extract recovered items data
        const { oldItems } = JSON.parse(recoveredItems)

        // Update budgetItems state
        setBudgetItems(oldItems)
      }
    } else if (window && window.localStorage && window.localStorage.getItem('budget-app') !== null && window.localStorage.getItem('budget-app')!.length > 0) {
      // Of if there are any existing data for items in localStorage
      // Get items data from localStorage
      const recoveredItems = window.localStorage.getItem('budget-app')

      // If there are any items to be recovered
      if (recoveredItems) {
        // Extract recovered items data
        const { oldItems } = JSON.parse(recoveredItems)

        // Update budgetItems state
        setBudgetItems(oldItems)
      }
    }
  }, [])// Run on initial render

  // Update items if budgetItems or storageMethod changes
  React.useEffect(() => {
    if (storageMethod === 'session') {
      // Save settings to sessionStorage
      window.sessionStorage.setItem('budget-app', JSON.stringify({
        oldItems: budgetItems
      }))

      // Remove duplicate data in localStorage
      window.localStorage.removeItem('budget-app')
    } else if (storageMethod === 'local') {
      // Save settings to localStorage
      window.localStorage.setItem('budget-app', JSON.stringify({
        oldItems: budgetItems
      }))

      // Remove duplicate data in sessionStorage
      window.sessionStorage.removeItem('budget-app')
    } else if (storageMethod === 'none') {
      // Remove all previous data from both storages
      window.localStorage.removeItem('budget-app')
      window.sessionStorage.removeItem('budget-app')
    }
  }, [budgetItems, storageMethod])// Watch budgetItems & storageMethod props

  // Update settings if budgetPeriod, budgetCurrency, budgetAmount or storageMethod changes
  React.useEffect(() => {
    if (storageMethod === 'session') {
      // Save settings to sessionStorage
      window.sessionStorage.setItem('budget-app-settings', JSON.stringify({
        oldBudgetPeriod: budgetPeriod,
        oldBudgetCurrency: budgetCurrency,
        oldBudgetAmount: budgetAmount,
        oldStorageMethod: storageMethod
      }))

      // Remove duplicate data in localStorage
      window.localStorage.removeItem('budget-app-settings')
    } else if (storageMethod === 'local') {
      // Save settings to localStorage
      window.localStorage.setItem('budget-app-settings', JSON.stringify({
        oldBudgetPeriod: budgetPeriod,
        oldBudgetCurrency: budgetCurrency,
        oldBudgetAmount: budgetAmount,
        oldStorageMethod: storageMethod
      }))

      // Remove duplicate data in sessionStorage
      window.sessionStorage.removeItem('budget-app-settings')
    } else if (storageMethod === 'none') {
      // Remove all previous data from both storages
      window.localStorage.removeItem('budget-app-settings')
      window.sessionStorage.removeItem('budget-app-settings')
    }
  }, [budgetPeriod, budgetCurrency, budgetAmount, storageMethod])// Watch budgetPeriod, budgetCurrency, budgetAmount & storageMethod props

  return (
    <div className="app">
      <BrowserRouter>
        <Switch>
          {/* Add homepage */}
          <Route path="/" exact={true}>
            <HomePage
              budgetItems={budgetItems}
              setBudgetItems={setBudgetItems}
              budgetAmount={budgetAmount}
              budgetPeriod={budgetPeriod}
              budgetCurrency={budgetCurrency}
              storageMethod={storageMethod}
            />
          </Route>

          {/* Add settings */}
          <Route path="/settings">
            <SettingsPage
              budgetPeriod={budgetPeriod}
              budgetCurrency={budgetCurrency}
              budgetAmount={budgetAmount}
              storageMethod={storageMethod}
              setBudgetPeriod={setBudgetPeriod}
              setBudgetCurrency={setBudgetCurrency}
              setBudgetAmount={setBudgetAmount}
              setStorageMethod={setStorageMethod}
            />
          </Route>
        </Switch>
      </BrowserRouter>
    </div>
  )
}

export default AppRouter
```

## Rendering budget app

All components, and pages, for your budget app are ready. Now, all you need to do is to take the `AppRouter` component and render it in the DOM. You can do this in `index.tsx`.

```tsx
// index.tsx

// Import react & renderer
import * as React from 'react'
import { render } from 'react-dom'

// Import components
import AppRouter from './app-router'

// Import styles
import './styles/styles.css'

// Cache the '#root' div
const rootElement = document.getElementById('root')

// Render AppRouter component in the DOM
render(<AppRouter />, rootElement)
```

## Styles

One more thing. Your budget app works as it is supposed to. The problem is that it looks like a skeleton. There are no styles. Let's fix this. Here are some styles for inspiration.

```css
/* Variables */
:root {
  --color-black: #1e272e;
  --color-blue: #0fbcf9;
  --color-gray: #ccc;
  --color-green: #0be881;
  --color-red: #ff3f34;
}

/* Default styles */
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

body,
#root,
.app {
  min-height: 100vh;
}

body {
  margin: 0;
  font: 16px / 1.414 sans-serif;
  color: var(--color-black);
}

.app {
  position: relative;
  padding: 8px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 0 8px;
}

h1,
h2 {
  margin: 0;
}

h2 {
  font-size: 21px;
}

a {
  color: var(--color-black);
  text-decoration: none;
}

/* Buttons */
.btn {
  border: 0;
  cursor: pointer;
  line-height: 1;
  transition: .25s all ease-in-out;
}

.btn-add,
.btn-cross,
.btn-settings {
  display: flex;
  align-items: center;
  flex-flow: row nowrap;
  justify-content: center;
  padding: 0;
  margin: 0;
  height: 32px;
  text-align: center;
  background: transparent;
  color: var(--color-gray);
}

.btn-add,
.btn-cross {
  font-weight: 700;
  color: var(--color-gray);
}

.btn-add:hover,
.btn-cross:hover {
  color: var(--color-black);
}

.btn-cross,
.btn-settings {
  width: 32px;
  border-radius: 50%;
}

.btn-add {
  margin: auto;
  font-size: 17px;
  border: 0;
}

.btn-add:focus {
  outline: 0;
}

.btn-cross {
  font-size: 28px;
}

.btn-remove,
.btn-settings {
  fill: var(--color-gray);
}

.btn-remove:hover,
.btn-settings:hover {
  fill: var(--color-black);
}

.btn-remove {
  background: transparent;
}

.btn-label {
  margin-left: 4px;
  font-size: 17px;
}

/* Form */
fieldset {
  display: flex;
  margin: 0;
  padding: 0;
  border: 0;
}

fieldset + fieldset {
  margin-top: 21px;
}

input:not([type=checkbox]):not([type=submit]),
select {
  padding: 6px 0;
  width: 100%;
  font-size: 14px;
  background: #fff;
  border: 0;
  border-bottom: 1px solid var(--color-gray);
}

input:focus {
  outline: 0;
  border-bottom-color: var(--color-blue);
}

label {
  font-size: 14px;
  font-weight: 700;
  cursor: default;
}

label + input {
  margin-top: 4px;
}

.custom-checkbox-checkbox {
  display: none;
  visibility: hidden;
}

.custom-checkbox-label {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  position: relative;
  line-height: 1;
}

.custom-checkbox-label::before {
  display: block;
  margin-right: 6px;
  content: '';
  width: 16px;
  height: 16px;
  background: #fff;
  border: 2px solid var(--color-gray);
  border-radius: 2px;
}

.custom-checkbox-checkbox:checked + .custom-checkbox-label::before {
  background: var(--color-blue);
  border-color: var(--color-blue);
}

.custom-checkbox-checkbox:checked + .custom-checkbox-label::after {
  content: '';
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Cdefs/%3E%3Cpath fill='%23fff' d='M1 14l4-4 8 8L27 4l4 4-18 18z'/%3E%3C/svg%3E");
  background-size: 14px;
  background-position: center;
  background-repeat: no-repeat;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  width: 16px;
  height: 16px;
}

/* Modal */
.modal-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,.15);
}

.modal-dialog {
  position: relative;
  padding: 28px 8px 22px;
  width: 100%;
  max-width: 340px;
  background: #fff;
  border-radius: 4px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, .25);
}

.modal-dialog .btn-cross {
  position: absolute;
  top: 4px;
  right: 4px;
}

.modal-dialog form {
  padding: 0 16px;
}

/* Budget total */
.budget-total-positive {
  color: var(--color-green);
}

.budget-total-negative {
  color: var(--color-red);
}

/* Budget list */
.budget-list {
  margin-bottom: 16px;
}

/* Budget item */
.budget-item {
  display: flex;
  align-items: center;
  flex-flow: row nowrap;
  justify-content: space-between;
}

.budget-item + .budget-item {
  margin-top: 8px;
}

.budget-item input:not([type=checkbox]):not([type=submit]) {
  border: 0;
}

.budget-item input:not([type=checkbox]):not([type=submit]):focus {
  border-bottom: 1px solid var(--color-blue);
}

.budget-item-paid,
.budget-item-date,
.budget-item-price,
.budget-item-remove {
  width: 100%;
}

.budget-item-paid,
.budget-item-price,
.budget-item-remove {
  display: flex;
  align-items: center;
}

.budget-item-paid {
  width: 100%;
  max-width: 24px;
}

.budget-item-title {
  flex-grow: 1;
}

.budget-item-date {
  max-width: 150px;
}

.budget-item-date input {
  height: 29px;
}

.budget-item-price {
  align-items: center;
  max-width: 100px;
}

.budget-item-price input {
  text-align: right;
}

.budget-item-price span {
  font-size: 14px;
  line-height: 1;
}

.budget-item-remove {
  justify-content: flex-end;
  max-width: 40px;
}
```

## Conclusion: How to build a budget app with React, TypeScript & Web Storage API

Congratulations, you've just built your own budget app! However, why stop here? Play and tinker with your new budget app. Think about what features you would like it to have. Then, go and implement them. You can also add more styles to make the app look the way you want it. Remember, your creativity is the only limit. So, let it go haywire and have fun.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Part 1]: https://blog.alexdevero.com/build-budget-app-pt1/
[GitHub]: https://github.com/alexdevero/budget-app-ts/tree/blog-tutorial
[works]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
[React Router docs]: https://reacttraining.com/react-router/web/guides/quick-start

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
