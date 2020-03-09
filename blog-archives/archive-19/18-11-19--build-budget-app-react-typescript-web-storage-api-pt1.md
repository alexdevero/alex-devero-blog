# How to Build a [Budget App] With React, Typescript & Web Storage API Pt.1
Do you want to learn React, TypeScript or Web Storage API? This tutorial will help you with it. Step by step, it will help you build your own budget app using these technologies. Learn React, TypeScript and Web Storage API while building your own budget app!<!--more-->
<!--
Table of Contents:
## Introduction
## Project setup
### TypeScript
### Project structure
## Interfaces
## Icons
## Currency codes
## BudgetItem component
## BudgetList component
## BudgetItemAdd component
## Conclusion: How to build a budget app with React, TypeScript & Web Storage API
How to Build a Budget App With React, Typescript & Web Storage API [Part 2].
-->

<!-- !! Add this when 2nd part is out! -->
<!-- You can find the code on my [GitHub] (_make sure you are on "blog-tutorial" branch_). -->

## Introduction

At the end of this tutorial you will have a working budget app with following features. First, it will allow you to set a budget. You will also be able to choose in what currency you want the budget to be. Don't worry. You don't have to remember any codes. App will help you choose the currency code from options provided by datalist.

Second, it will allow you to choose a budget period-daily, monthly or yearly budget. Third, it will allow you to create a list of items, things, you either will buy or you already bought. Then, depending on the payment status, paid or not paid, it will show you how much budget remains. Or, if you are already in red numbers, if you've spent your entire budget.

Lastly, it will also allow you to store your data, items on the list and app settings, in app state or in `localStorage` or `sessionStorage`, using [Web Storage API]. Thanks to web storage API, you will be able to keep your data even if refresh your app in the browser. Well, only if you decide to use local or session storage as your preferred storage method. Otherwise, it will be erased.

As I mentioned, the tech stack for this budget app will be React, TypeScript and Web Storage API. In addition you will also use [React Router]. You will use this library to create routing for homepage and Settings page of your budget app. That's for the introduction. Now, let's get to work.

## Project setup

The first thing you will need to do is putting together the workflow, to compile all React and CSS files. You can handle this using your own bundler such as [Webpack] or [Parcel], and config. Simpler and easier option is to use ready-to-use boilerplate app provided by `create-react-app` package.

Using the `create-react-app` boilerplate is easy. You can use it with npm, using `npm init react-app budget-app-ts --typescript` or `npx create-react-app budget-app-ts --typescript`. Or for yarn, `yarn create react-app budget-app-ts --typescript`. If you don’t want to use TypeScript, omit the `--typescript` flag at the end of the command.

Next, you will need to install two additional packages. The first one is `react-router-dom`. You will use this for routing between pages in your budget app. In additional, you should also install types for this package, `@types/react-router-dom`. The second package is `shortid`, and types for it, `@types/shortid`.

You will use the `shortid` package to generate unique ids for every item on the list in your budget app. This is much better than using indexes, which is a very [bad practice]. It is also much easier than writing some id generator, or creating these ids manually. This is all you will need. Now, your `package.json` should look similar to this:

```json
{
  "name": "budget-app-ts",
  "version": "1.0.0",
  "description": "Minimal budget app built with React & TypeScript.",
  "license": "MIT",
  "private": false,
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
    "react": "16.12.0",
    "react-dom": "16.12.0",
    "react-router-dom": "5.1.2",
    "shortid": "2.2.15"
  },
  "devDependencies": {
    "@types/react": "16.9.11",
    "@types/react-dom": "16.9.4",
    "@types/react-router-dom": "5.1.2",
    "@types/shortid": "0.0.29",
    "react-scripts": "3.2.0",
    "typescript": "3.7.2"
  }
}
```

### TypeScript

For TypeScript, let's keep it simple and use the `tsconfig.json` generated by `create-react-app`. There is no need to change anything, unless you want to. The `tsconfig.json` for this project will look like this:

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

### Project structure

Below is the final structure of this budget app project. Use this as your map as you work on this tutorial. It will help you orient yourself. It will also help you ensure you have all files you need, and at the right place. Now, let's start working on your budget app.

```
budget-app-ts/
├─node_modules
├─public
│ ├─favicon.ico
│ ├─index.html
│ ├─manifest.json
│ └─robots.txt
├─src
│ ├─components
│ │ ├─item-item-add.tsx
│ │ ├─item-item.tsx
│ │ ├─item-list.tsx
│ │ ├─item-total.tsx
│ │ ├─icon-bin.tsx
│ │ └─icon-settings.tsx
│ ├─data
│ │ └─currency-codes.ts
│ ├─pages
│ │ └─home.tsx
│ │ └─settings.tsx
│ ├─styles
│ │ └─styles.css
│ ├─app-router.tsx
│ ├─index.tsx
│ ├─interfaces.ts
│ └─react-app-env.d.ts
├─ package.json
└─ tsconfig.json
```

## Interfaces

As the first thing, let's create interfaces for your budget app. It is better to do this now, for at least two reasons. First, it will help you plan and outline better the functionality of your components. Second, you will not run into issues with TypeScript complaining about missing types for `props`, etc.

Your budget app will need seven `interface` objects. These interface will be for `BudgetItemObj` object, `BudgetList`, `BudgetItem`, `BudgetTotal`, `HomePage`, `SettingsPage` and `BudgetItemAdd` component. The `BudgetItemObjInterface` will define the shape of on item on the list in your budget app.

Every item will contain `date` (date of payment), `isPaid` (if item has been paid), `price` (price of the item), `title` (title of the item) and `id` (unique id). The `BudgetListInterface` will contain `budgetCurrency`, `budgetItems` (array of `BudgetItemObjInterface`) and two handlers, `handleItemUpdate` and `handleItemRemove`.

The interface for `budgetItem` component will contain `budgetCurrency`, `budgetItem` and two handlers, `handleItemUpdate` and `handleItemRemove`. This is similar to the `BudgetListInterface` because you will pass many of the props of `budgetItem` component through the `BudgetList` component.

Next is `BudgetTotalInterface`. This interface will contain `budgetPeriod`, `budgetAmount`, `budgetPaid`, `budgetCurrency`. Almost all these props will come from app settings. Interfaces for pages will be also very similar. For homepage (`HomePageInterface`), `budgetItems`, `budgetAmount`, `budgetPeriod`, `budgetCurrency`, `storageMethod` and `setBudgetItems` hook dispatcher.

For Settings page (`SettingsPageInterface`), `budgetAmount`, `budgetPeriod`, `budgetCurrency`, `storageMethod` and `setBudgetPeriod`, `setBudgetCurrency`, `setBudgetAmount`, `setStorageMethod` hook dispatchers. The last one is `BudgetItemAddInterface`.

This interface will be very simple. It will contain `showAddItem`, `handleAddItem` handler and `handleShowAddItem` hook dispatcher. When you add types for every prop, handler and hook dispatcher in each interface, this is what you get:

```tsx
// Interface for BudgetItemObj object
export interface BudgetItemObjInterface {
  date: string;
  isPaid: boolean;
  price: number;
  title: string;
  id: string;
}

// Interface for BudgetList component
export interface BudgetListInterface {
  budgetCurrency: string;
  budgetItems: BudgetItemObjInterface[]
  handleItemUpdate: (value: string, id: string, itemProperty: string) => void;
  handleItemRemove: (id: string) => void;
}

// Interface for BudgetItem component
export interface BudgetItemInterface {
  budgetCurrency: string;
  budgetItem: BudgetItemObjInterface;
  handleItemUpdate: (value: string, id: string, itemProperty: string) => void;
  handleItemRemove: (id: string) => void;
}

// Interface for BudgetTotal component
export interface BudgetTotalInterface {
  budgetPeriod: string;
  budgetAmount: number;
  budgetPaid: number;
  budgetCurrency: string;
}

// Interface for Homepage
export interface HomePageInterface {
  budgetItems: BudgetItemObjInterface[];
  budgetAmount: number;
  budgetPeriod: string;
  budgetCurrency: string;
  storageMethod: string;
  setBudgetItems: React.Dispatch<React.SetStateAction<BudgetItemObjInterface[]>>;
}

// Interface for Settings page
export interface SettingsPageInterface {
  budgetAmount: number;
  budgetPeriod: string;
  budgetCurrency: string;
  storageMethod: string;
  setBudgetPeriod: React.Dispatch<React.SetStateAction<string>>;
  setBudgetCurrency: React.Dispatch<React.SetStateAction<string>>;
  setBudgetAmount: React.Dispatch<React.SetStateAction<number>>;
  setStorageMethod: React.Dispatch<React.SetStateAction<string>>;
}

// Interface for BudgetItemAdd component
export interface BudgetItemAddInterface {
  showAddItem: boolean;
  handleAddItem: (payload: BudgetItemObjInterface) => void;
  handleShowAddItem: React.Dispatch<React.SetStateAction<boolean>>;
}
```

## Icons

Let's create components for two icons you will use in your budget app. One icon will be for removing item from the list and the second for link to Settings page. Icon for removing will be a recycle bin. Icon for Settings link will be cog, or gear. Both components will use SVG to render the icons.

First, let's create the `IconBin` component:

```tsx
// Import dependencies
import * as React from 'react'

// IconBin component
const IconBin = () => (
  <svg xmlns="http://www.w3.org/2000/svg" width="18" id="Layer_41" data-name="Layer 41" viewBox="0 0 50 50"><defs/><defs/><path d="M44 10h-9V8.6A6.6 6.6 0 0028.4 2h-6.8A6.6 6.6 0 0015 8.6V10H6a2 2 0 000 4h3v27.4a6.6 6.6 0 006.6 6.6h18.8a6.6 6.6 0 006.6-6.6V14h3a2 2 0 000-4zM19 8.6A2.6 2.6 0 0121.6 6h6.8A2.6 2.6 0 0131 8.6V10H19V8.6zm18 32.8a2.6 2.6 0 01-2.6 2.6H15.6a2.6 2.6 0 01-2.6-2.6V14h24v27.4z" className="cls-1"/><path d="M20 18.5a2 2 0 00-2 2v18a2 2 0 004 0v-18a2 2 0 00-2-2zM30 18.5a2 2 0 00-2 2v18a2 2 0 104 0v-18a2 2 0 00-2-2z" className="cls-1"/></svg>
)

export default IconBin
```

Next, the `IconSettings` component.

```tsx
// Import dependencies
import * as React from 'react'

// IconSettings component
const IconSettings = () => (
  <svg xmlns="http://www.w3.org/2000/svg" width="21" viewBox="0 0 896 1024"><defs/><path d="M447.938 350C358.531 350 286 422.531 286 512c0 89.375 72.531 162.062 161.938 162.062 89.438 0 161.438-72.688 161.438-162.062-.001-89.469-72.001-162-161.438-162zm324.687 255.062l-29.188 70.312 52.062 102.25 6.875 13.5-72.188 72.188-118.436-55.937-70.312 28.875L505.75 945.5l-4.562 14.5H399.156L355 836.688l-70.312-29-102.404 51.938-13.5 6.75-72.156-72.125 55.875-118.5-28.969-70.25-109.065-35.626L0 565.188V463.219L123.406 419l28.969-70.188-51.906-102.469-6.844-13.438 72.062-72.062 118.594 55.844 70.219-29.031 35.656-109.188L394.75 64h102l44.188 123.469 70.125 29.031L713.5 164.531l13.625-6.844 72.125 72.062-55.875 118.406L772.25 418.5l109.375 35.656L896 458.75v101.938l-123.375 44.374z"/></svg>
)

export default IconSettings
```

## Currency codes

Before moving any further, let's take care of another thing you will need. This will be array of currency codes. As I mentioned, the app will allow you to choose in what currency you want the budget to be. In order to make this as easy as possible, you will use `input` element along with a [datalist].

Why `datalist` and not `select`? There are currently around 167 currency codes. Imagine looking for one specific code in a `select` with 167 options. That would be insane. `datalist` makes it easier because it helps you narrow the selection of options as you write. One or two characters and from 167 options, there are only two or one left.

That said, you still need the data, the currency codes, for the `datalist`. So, let's store it in an array, in a separate file, and export it. After that, you can import this dataset, later when you will work on Settings page. There, you will loop over it using `map()` and generate `option` element for each code.

```ts
const currencyCodes = [
  'AED', 'ALL', 'AMD', 'ANG', 'AOA', 'ARS', 'AUD', 'AWG', 'AZN', 'BAM', 'BBD', 'BDT', 'BGN', 'BHD', 'BIF', 'BMD', 'BND', 'BOB', 'BOV', 'BRL', 'BSD', 'BTN', 'BWP', 'BYN', 'BZD', 'CAD', 'CDF', 'CLF', 'CLP', 'CNY', 'COP', 'COU', 'CRC', 'CUC', 'CUP', 'CVE', 'CZK', 'DJF', 'DKK', 'DOP', 'DZD', 'EGP', 'ERN', 'ETB', 'EUR', 'FJD', 'FKP', 'GBP', 'GEL', 'GHS', 'GIP', 'GMD', 'GNF', 'GTQ', 'GYD', 'HKD', 'HNL', 'HRK', 'HTG', 'HUF', 'CHE', 'CHF', 'CHW', 'IDR', 'ILS', 'INR', 'IQD', 'IRR', 'ISK', 'JMD', 'JOD', 'JPY', 'KES', 'KGS', 'KHR', 'KMF', 'KPW', 'KRW', 'KWD', 'KYD', 'KZT', 'LAK', 'LBP', 'LKR', 'LRD', 'LSL', 'LYD', 'MAD', 'MDL', 'MGA', 'MKD', 'MMK', 'MNT', 'MOP', 'MRU', 'MUR', 'MVR', 'MWK', 'MXN', 'MXV', 'MYR', 'MZN', 'NAD', 'NGN', 'NIO', 'NOK', 'NPR', 'NZD', 'OMR', 'PAB', 'PEN', 'PGK', 'PHP', 'PKR', 'PLN', 'PYG', 'QAR', 'RON', 'RSD', 'RUB', 'RWF', 'SAR', 'SBD', 'SCR', 'SDG', 'SEK', 'SGD', 'SHP', 'SLL', 'SOS', 'SRD', 'SSP', 'STN', 'SVC', 'SYP', 'SZL', 'THB', 'TJS', 'TMT', 'TND', 'TOP', 'TRY', 'TTD', 'TWD', 'TZS', 'UAH', 'UGX', 'USD', 'USN', 'UYI', 'UYU', 'UZS', 'VEF', 'VND', 'VUV', 'WST', 'XAF', 'XCD', 'XDR', 'XOF', 'XPF', 'XSU', 'XUA', 'YER', 'ZAR', 'ZMW', 'ZWL', 'AFN'
]

export default currencyCodes
```

## BudgetItem component

Now, let's create the `BudgetItem` component. You will use this component to render individual items on the list in your budget app. This component will not contain any logic. It will only accept some props and render the markup.

The markup for `BudgetItem` component will be following. There will be a checkbox to mark the item as paid or not. This budget app will lower your budget, subtract the price of the item from the total budget, only when the item is paid. Next will be title of the item, followed by the date the item was, or will be, paid.

This will be followed by price and button to remove the item from the list. This, `BudgetItem`, component will get all this data from `props`. These `props` will come from `BudgetList`. Here, you will iterate over array of all items and render `BudgetItem` component for each. Now, comes one interesting thing.

This budget app will allow you to edit all items on the list. You will not have to open some new page or modal to edit any item. You will be able to do this right there on the list. This way you will be able to edit the title, price and the payment date, and also check it off as paid or uncheck it as unpaid.

In order to implement this `BudgetItem` component will render all data, title, price, etc., through inputs. You will use text inputs for title and price, checkbox input (with custom styles) for marking the item as paid and date input for date of payment. Each of these inputs will also have a `onChange` event handler, `handleItemUpdate` function.

This handler function will be passed through `props`. It will accept three parameters, `value` passed to the input, type of the data (title, price, is item paid) and `id` of the item. The `id` will guarantee every change will be made only to one specific item.

```tsx
// Import dependencies
import * as React from 'react'

// Import interface
import { BudgetItemInterface } from './../interfaces'

// Import components
import IconBin from './icon-bin'

const BudgetItem = (props: BudgetItemInterface) => {
  return (
    <div className="budget-item">
      <div className="budget-item-paid">
        {/* Checkbox to mark the item as paid */}
        <input
          className="custom-checkbox-checkbox"
          type="checkbox"
          id={props.budgetItem.id}
          checked={props.budgetItem.isPaid}
          onChange={(event) => props.handleItemUpdate(event.target.value, props.budgetItem.id, 'isPaid')}
        />

        <label className="custom-checkbox-label" htmlFor={props.budgetItem.id} />
      </div>

      <div className="budget-item-title">
        {/* Title of the item */}
        <input
          type="text"
          value={props.budgetItem.title}
          onChange={(event) => props.handleItemUpdate(event.target.value, props.budgetItem.id, 'title')}
        />
      </div>

      <div className="budget-item-date">
        {/* Date the item was added */}
        <input
          type="date"
          value={props.budgetItem.date}
          onChange={(event) => props.handleItemUpdate(event.target.value, props.budgetItem.id, 'date')}
        />
      </div>

      <div className="budget-item-price">
        {/* Price of the item */}
        <input
          type="number"
          value={props.budgetItem.price}
          onChange={(event) => props.handleItemUpdate(event.target.value, props.budgetItem.id, 'price')}
        />
        {' '}
        <span>{props.budgetCurrency}</span>
      </div>

      <div className="budget-item-remove">
        {/* Delete item */}
        <button className="btn btn-remove" onClick={() => props.handleItemRemove(props.budgetItem.id)}><IconBin /></button>
      </div>
    </div>
  )
}

export default BudgetItem
```

## BudgetList component

Next, let's create the `BudgetList` component. This component will be very simple and short. Similarly to the `BudgetItem`, there will also be no logic.

```tsx
// Import dependencies
import * as React from 'react'

// Import interfaces
import { BudgetItemObjInterface, BudgetListInterface } from './../interfaces'

// Import components
import BudgetItem from './budget-item'

const BudgetList = (props: BudgetListInterface) => {
  return (
    <div className="budget-list">
      {props.budgetItems.map((item: BudgetItemObjInterface) => {
        return (
          <BudgetItem
            key={item.id}
            budgetCurrency={props.budgetCurrency}
            budgetItem={item}
            handleItemUpdate={props.handleItemUpdate}
            handleItemRemove={props.handleItemRemove}
          />
        )
      })}
    </div>
  )
}

export default BudgetList
```

## BudgetItemAdd component

This, the `BudgetItemAdd` component, will be the last component you will in this, first, part of this tutorial. This component will be a modal dialog that will allow you to add new item on your list, right on the homepage. Unlike the previous component, this component will contain some logic.

About the logic. At the top of this component, you will use React `useState` hook to create four state, one state for every input. Next, you will create `handleFormSubmit` function. When triggered, this function will process state for every input, use `shortid` package to generate unique `id`, create new item, reset the form and close the modal dialog.

About the structure. There will be fieldset with label and input for date of payment, item title, item price and also checkbox for marking the item as paid. Then, there will be a button, `input` (type `submit`). All form elements will be wrapped inside a `form`. This will be wrapped inside a `div` a `modal-dialog`, with a `button` to close he modal dialog.

As the last thing, this dialog will be wrapped inside another `div`, a `modal-wrapper`. This `div` will work as an overlay when the modal dialog for adding new item will be visible.

About the button. The reason for using input is that you want to trigger `submit` event on the form. When this happens, you can use the `handleFormSubmit` function to handle this event and create new item. To do this, attach the `handleFormSubmit` function as a handler for `onSubmit` event on the `form` element.

_Note: You don't have to use form with "submit" input. You can also use a "div" with "button". In that case, attach the "handleFormSubmit" function on that button as a handler for "onClick" event. This way, everything will work as well._

```tsx
// Import dependencies
import * as React from 'react'
import shortid from 'shortid'

// Import interface
import { BudgetItemAddInterface } from './../interfaces'

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

## Conclusion: How to build a budget app with React, TypeScript & Web Storage API

This is it for the first part of this tutorial. Let's recap. Today, you have set up the project workflow, along with installing additional dependencies, and configuring TypeScript. Next, you've prepared interfaces for some components, two icon components for UI and dataset for `datalist` with currency codes that will be on Settings page.

Lastly, you've built the first components for your budget app, the `BudgetItem`, `BudgetList` and `BudgetItemAdd`. In the next part, you will finish this tutorial by creating `ItemItemAdd` component, Homepage, Settings page, routing for these pages and implement web storage API to store your data.

At the top of this, you will also add some styles to make your budget app look great. But, that, is on the program for the next part. Until then, have a great day and stay tuned.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
<!-- [Part 1]: -->
[GitHub]: https://github.com/alexdevero/budget-app-ts/tree/blog-tutorial
[Web Storage API]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API
[React Router]: https://reacttraining.com/react-router/
[Webpack]: https://webpack.js.org/
[Parcel]: https://parceljs.org/
[bad practice]: https://blog.alexdevero.com/react-best-practices-pt2/#7-don8217t-use-indexes-as-a-key-prop
[datalist]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist