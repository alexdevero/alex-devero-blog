# How to Build [Password Generator] with Electron & React Pt.3 – The Final Part

The main task of a password generator is generating passwords, right? This will be our goal for this final part. First, we will implement some functionality for `Input` and `Checkbox` components. Then, we will add a few tweaks. After that, we will finally put together the core piece of our password generator, the method for generating passwords! I hope you ready because we have a lot of work to do today. So, without further ado, let's bring this awesome app to life!

<!--
Table of Contents:
## Expanding the state
## Input, Checkbox and new methods
### Adding new props
## Passing the props down the chain
## Preparing the password generator
## Creating the password generator
## Closing thoughts on how to build password generator
-->

How to Build Password Generator with Electron & React [part 1].

How to Build Password Generator with Electron & React [part 2].

You can find the password generator app on [GitHub].

## Expanding the state

Let's start the work on our password generator by adding some key-value pairs to the `state` we will need today. Then, we can continue by creating two new methods, one will be for handling inputs and the second for handling checkboxes. Both these methods will have access to `state` and update it, will be able to change values for specific keys. `State` is defined in `src/App/App.jsx` and those two new methods will be defined here as well. So, let's open this file and start working.

At this moment, our `state` contains four key-value pairs, `showAdvancedSettings`, `showBasicSettings` and `showResult`. Let's add a few more. These will be `settingsAsci`, `settingsLower`, `settingsNumbers`, `settingsSpace` and `settingsUpper`. All these keys will be boolean and their default value will be `false`. We will use these keys for checkboxes and for switching on or off different options for our password generator, listed on the `BasicSettings` screen. Let's stay here for a second because we are not done yet.

Next, we will add another three pairs. These are `settingsCustom`, `settingsEntropy` and `settingsLength`. The value of `settingsCustom` will be a string, an empty string for now. The value of `settingsEntropy` and `settingsLength` will be an integer. Now, we can set the default value to "0" and let the user decide how long the password should be, or how many bits she wants to use for entropy. Or, we can add some starting values. Well, at least for the length since entropy may not be used as often. Okay, let's leave it with 0. This is all we need in the terms of `state`. The whole `App` component will then look like this.

```
// src/App/App.jsx

import React from 'react'
import styled, { injectGlobal } from 'styled-components'

import AdvancedSettings from './components/AdvancedSettings'
import BasicSettings from './components/BasicSettings'
import { Button, ButtonWrapper } from './components/Button'
import Info from './components/Info'
import Navigation from './components/Navigation'

injectGlobal`
  body {
    margin: 0;
    font: caption; /* Automatically pick whatever font is the UI font on a system */
    line-height: 1.414;
    color: #333;
  }

  h1,
  label {
    -webkit-user-select: none;
    cursor: default;
  }

  h1 {
    margin-top: 0;
    font-size: 24px;
  }
`

const AppWrapper = styled.div`
  padding-right: 16px;
  padding-left: 16px;
`

class App extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      settingsAsci: false,
      settingsCustom: '',
      settingsEntropy: 0,
      settingsLength: 0,
      settingsLower: false,
      settingsNumbers: false,
      settingsSpace: false,
      settingsUpper: false,
      showAdvancedSettings: false,
      showBasicSettings: false,
      showResult: false
    }
  }

  // Method for Showing Advanced settings screen
  toggleAdvancedSettings() {
    this.setState({
      showAdvancedSettings: !this.state.showAdvancedSettings,
      showBasicSettings: false
    })
  }

  // Method for Showing Basic settings screen
  toggleBasicSettings() {
    this.setState({
      showAdvancedSettings: false,
      showBasicSettings: !this.state.showBasicSettings
    })
  }

  generatePassword() {
    this.setState({
      showResult: true
    })
  }

  // Method for Checkbox component
  handleCheckbox(e) {
    e.preventDefault()

    let checkbox = e.currentTarget.querySelector('[type=checkbox]')
    let checkboxId = checkbox.getAttribute('id')

    checkbox.checked = checkbox.checked ? false : true

    this.setState({
      [checkboxId]: !this.state[checkboxId]
    })
  }

  // Method for Input component
  handleInput(e) {
    let inputId = e.currentTarget.getAttribute('id')
    let inputValue = e.currentTarget.value

    this.setState({
      [inputId]: inputValue
    })
  }

  render() {
    return (
      <AppWrapper>
        {/* Main navigation */}
        <Navigation toggleBasicSettings={() => this.toggleBasicSettings()} toggleAdvancedSettings={() => this.toggleAdvancedSettings()} state={this.state} />

        {/* Component with basic settings */}
        {this.state.showBasicSettings && <BasicSettings state={this.state} clickHandler={(e) => this.handleCheckbox(e)} clickInputHandler={(e) => this.handleInput(e)} />}

        {/* Component with advanced settings */}
        {this.state.showAdvancedSettings && <AdvancedSettings state={this.state} clickHandler={(e) => this.handleInput(e)} />}

        {/* Component with welcome message and result - the password generated by our password generator */}
        {!this.state.showBasicSettings && !this.state.showAdvancedSettings && <Info showResult={this.state.showResult} />}

        {/* Main control elements - button for generating password and for reseting our password generator */}
        <ButtonWrapper>
          {!this.state.showResult && <Button type="button" onClick={() => this.generatePassword()}>Generate password</Button>}

          {this.state.showResult && <Button type="button" onClick={() => this.generatePassword()}>Generate new</Button>}
        </ButtonWrapper>
      </AppWrapper>
    )
  }
}

export default App
```

## Input, Checkbox and new methods

Now, let's take a look at the methods for our Input and `Checkbox` components. In case of inputs, we will need a method that will do three things. First, it will get the `id` of the `input` element, which will match one specific key in `state`. Second, it will take the `value` of the input. Third, it will use the `id` and `value` and update `state`, using the `setState`. That's all. Let's call this method "handleInput".

```
handleInput(e) {
  let inputId = e.currentTarget.getAttribute('id')
  let inputValue = e.currentTarget.value

  this.setState({
    [inputId]: inputValue
  })
}
```

Next, let's add the second method that will handle our Checkboxes component. Similar to the method for Input component, this method will also get the `id` of the `checkbox` element. Then, it will check whether the `checkbox` element is checked or not. If it is not, it will change its state to checked. Otherwise, to unchecked. After that, it will use the `id` of the checkbox and update the `state`, again using the `setState`.

```
handleCheckbox(e) {
  e.preventDefault()

  let checkbox = e.currentTarget.querySelector('[type=checkbox]')
  let checkboxId = checkbox.getAttribute('id')

  checkbox.checked = checkbox.checked ? false : true

  this.setState({
    [checkboxId]: !this.state[checkboxId]
  })
}
```

### Adding new props

Now, we can add these two methods somewhere above the `render` method inside our `App` class. Then, we can implement them. And, we will do this by passing both methods via `props` to the `BasicSettings` and `AdvancedSettings` components. We can call this prop "clickHandler". However, because the `BasicSettings` component will require both methods we will call the second "clickInputHandler". The `AdvancedSettings` component will require only the method for inputs.

Another thing we will do, to make our password generator work properly, is passing the `state` itself as a prop to both, `BasicSettings` and `AdvancedSettings` components. We will do this because we will use the values in `state` to set the default state of our `Checkbox` and `Input` components.

```
// src/App/App.jsx

// ... some code

class App extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      settingsAsci: false,
      settingsCustom: '',
      settingsEntropy: 0,
      settingsLength: 0,
      settingsLower: false,
      settingsNumbers: false,
      settingsSpace: false,
      settingsUpper: false,
      showAdvancedSettings: false,
      showBasicSettings: false,
      showResult: false
    }
  }

  // Method for Showing Advanced settings screen
  toggleAdvancedSettings() {
    this.setState({
      showAdvancedSettings: !this.state.showAdvancedSettings,
      showBasicSettings: false
    })
  }

  // Method for Showing Basic settings screen
  toggleBasicSettings() {
    this.setState({
      showAdvancedSettings: false,
      showBasicSettings: !this.state.showBasicSettings
    })
  }

  generatePassword() {
    this.setState({
      showResult: true
    })
  }

  // Method for Checkbox component
  handleCheckbox(e) {
    e.preventDefault()

    let checkbox = e.currentTarget.querySelector('[type=checkbox]')
    let checkboxId = checkbox.getAttribute('id')

    checkbox.checked = checkbox.checked ? false : true

    this.setState({
      [checkboxId]: !this.state[checkboxId]
    })
  }

  // Method for Input component
  handleInput(e) {
    let inputId = e.currentTarget.getAttribute('id')
    let inputValue = e.currentTarget.value

    this.setState({
      [inputId]: inputValue
    })
  }

  render() {
    return (
      <AppWrapper>
        {/* Main navigation */}
        <Navigation toggleBasicSettings={() => this.toggleBasicSettings()} toggleAdvancedSettings={() => this.toggleAdvancedSettings()} state={this.state} />

        {/* Component with basic settings */}
        {/* PASSING clickHandler, clickInputHandler AND state AS A PROPS HERE */}
        {this.state.showBasicSettings && <BasicSettings state={this.state} clickHandler={(e) => this.handleCheckbox(e)} clickInputHandler={(e) => this.handleInput(e)} />}

        {/* Component with advanced settings */}
        {/* PASSING clickHandler AND state AS A PROPS HERE */}
        {this.state.showAdvancedSettings && <AdvancedSettings state={this.state} clickHandler={(e) => this.handleInput(e)} />}

        {/* Component with welcome message and result - the password generated by our password generator */}
        {!this.state.showBasicSettings && !this.state.showAdvancedSettings && <Info showResult={this.state.showResult} />}

        {/* Main control elements - button for generating password and for reseting our password generator */}
        <ButtonWrapper>
          {!this.state.showResult && <Button type="button" onClick={() => this.generatePassword()}>Generate password</Button>}

          {this.state.showResult && <Button type="button" onClick={() => this.generatePassword()}>Generate new</Button>}
        </ButtonWrapper>
      </AppWrapper>
    )
  }
}

export default App
```

## Passing the props down the chain

As our next step, we will need to modify both components of our password generator, the `BasicSettings` and `AdvancedSettings`. Meaning, we will need to take those `props` we passed to them from `App` class and pass them even deeper to `Input` and `Checkbox` components. In `BasicSettings`, we will add the `clickHandler`, `clickInputHandler` and `state` as new parameters for the `BasicSettings` function. Then, we will take the `clickHandler` and set it as `onClick` event handler on `SettingsOptionWrapper`.

In case of the `clickInputHandler`, we will not use it as an event handler on the `SettingsOptionWrapper`. Instead, we will pass it as a new `prop` directly on the `Input` component. After that, in both `BasicSettings.jsx` and `AdvancedSettings.jsx` files, we will take a specific key in `state` and pass it as a value for "isChecked" `prop` for every `Checkbox` component. Then, we will do the same and take a specific key in `state` and pass it as a value for "inputValue" `prop` for every `Input` component.

Basic settings
```
// src/App/components/BasicSettings.jsx

import React from 'react'
import styled from 'styled-components'

import Checkbox from './Checkbox'
import Input from './Input'
import SettingsOptionWrapper from './SettingsOption'

const BasicSettingsWrapper = styled.div`
  padding-bottom: 16px;
`

const BasicSettings = ({ clickHandler, clickInputHandler, state }) => {
  return(
    <BasicSettingsWrapper>
      <SettingsOptionWrapper onClick={clickHandler}>
        <Checkbox id="settingsLower" isChecked={state.settingsLower} label="Lowercase" hint="abcdefghijklmnopqrstuvwxyz" />
      </SettingsOptionWrapper>

      <SettingsOptionWrapper onClick={clickHandler}>
        <Checkbox id="settingsUpper" isChecked={state.settingsUpper} label="Uppercase" hint="ABCDEFGHIJKLMNOPQRSTUVWXYZ" />
      </SettingsOptionWrapper>

      <SettingsOptionWrapper onClick={clickHandler}>
        <Checkbox id="settingsNumbers" isChecked={state.settingsNumbers} label="Numbers" hint="0123456789" />
      </SettingsOptionWrapper>

      <SettingsOptionWrapper onClick={clickHandler}>
        <Checkbox id="settingsAsci" isChecked={state.settingsAsci} label="ASCII symbols" hint={"!" + "\"" + "#$%&'()*+,-./:;<=>?@[\]^_`{|}~"} />
      </SettingsOptionWrapper>

      <SettingsOptionWrapper onClick={clickHandler}>
        <Checkbox id="settingsSpace" isChecked={state.settingsSpace} label="Space" hint=" " />
      </SettingsOptionWrapper>

      <SettingsOptionWrapper>
        <Input id="settingsLength" inputValue={state.settingsLength} label="Length" type="number" clickHandler={clickInputHandler} />
      </SettingsOptionWrapper>
    </BasicSettingsWrapper>
  )
}

export default BasicSettings
```

Advanced settings
```
// src/App/components/AdvancedSettings.jsx

import React from 'react'
import styled from 'styled-components'

import Input from './Input'
import SettingsOptionWrapper from './SettingsOption'

const AdvancedSettingsWrapper = styled.div`
  padding-bottom: 16px;
`

const AdvancedSettings = ({ clickHandler, state }) => {
  return(
    <AdvancedSettingsWrapper>
      <SettingsOptionWrapper>
        <Input id="settingsCustom" label="Custom characters" type="text" clickHandler={clickHandler} inputValue={state.settingsCustom} />
      </SettingsOptionWrapper>

      <SettingsOptionWrapper>
        <Input id="settingsEntropy" label="Entropy" type="number" clickHandler={clickHandler} inputValue={state.settingsEntropy} />
      </SettingsOptionWrapper>
    </AdvancedSettingsWrapper>
  )
}

export default AdvancedSettings
```

Finally, to finish this wiring, we will need to make a few changes in `Input` and `Checkbox` components. In case of the `Checkbox` component, we will add the "isChecked" `prop` we just created as another parameter. Then, we will use this parameter as a value for `defaultChecked` attribute. I just realized that we have the `clickHandler` as one of the parameters as well as an event handler on label, even though we are not using any of these. We can remove this code because we are dealing with click events through `SettingsOptionWrapper`.

```
// src/App/components/Checkbox.jsx

// ... some code

const Checkbox = ({id, hint, label, isChecked}) => {
  return(
    <LabelEl htmlFor={id}>
      <input id={id} name={id} type="checkbox" className="invisible" defaultChecked={isChecked} />

      <div className="checkbox">
        <svg width="20px" height="20px" viewBox="0 0 20 20">
          <path d="M3,1 L17,1 L17,1 C18.1045695,1 19,1.8954305 19,3 L19,17 L19,17 C19,18.1045695 18.1045695,19 17,19 L3,19 L3,19 C1.8954305,19 1,18.1045695 1,17 L1,3 L1,3 C1,1.8954305 1.8954305,1 3,1 Z"></path>

          <polyline points="4 11 8 15 16 6"></polyline>
        </svg>
      </div>

      <span>{label} <em>({hint})</em></span>
    </LabelEl>
  )
}

export default Checkbox
```

Lastly, there is the `Input` component. Just like we did above, we will add the "inputValue" `prop`, that now exists on Inputs, as a new parameter. As you probably remember, we passed the `clickHandler` directly to the `Input` component. So, we can keep this parameter where it is. There is, however, one change. We will not use it as an event handler on the `LabelEl`. Instead, we will as it as an event handler right on the `input` element itself.

```
// src/App/components/Input.jsx

// ... some code

const Input = ({id, label, clickHandler, type, inputValue}) => {
  return(
    <LabelEl htmlFor={id} className="label">

      <span>{label}</span>

      <input id={id} name={id} type={type} defaultValue={inputValue} onChange={clickHandler} />
    </LabelEl>
  )
}

export default Input
```

## Preparing the password generator

Now, it is all about the final step, creating and putting together our password generator. First, let's add one more key-value pair inside the `state`. The key will be `password` and its `value` will be an empty string. Then, pass the `password` as additional `prop` to the `Info` component. As a result, `Info` component will now have two `props`, `showResult` and `password`.

```
// src/App/App.jsx

// ... some code

class App extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      password: '',
      settingsAsci: false,
      settingsCustom: '',
      settingsEntropy: 0,
      settingsLength: 0,
      settingsLower: false,
      settingsNumbers: false,
      settingsSpace: false,
      settingsUpper: false,
      showAdvancedSettings: false,
      showBasicSettings: false,
      showResult: false
    }

    // ... some code

render() {
  return (
    <AppWrapper>
      // ... some code

      {/* Component with welcome message and result - the password generated by our password generator */}
      {!this.state.showBasicSettings && !this.state.showAdvancedSettings && <Info showResult={this.state.showResult} password={this.state.password} />}

      // ... some code
  )
}
```

Next, let's open the `src/App/components/Info.jsx` and add the `password` prop as second parameter and also as a content for the `InfoText` component. One more thing. The user may want to use our password generator to create a really very long password (good practice actually). So, let's make sure it will not break the layout by and `word-break` CSS property and setting it to `break-all`.

```
// src/App/components/Info.jsx

import React from 'react'
import styled from 'styled-components'

const InfoWrapper = styled.div`
  margin-top: 32px;
  margin-bottom: 32px;
`

const InfoText = styled.p`
  margin: 0;
  text-align: center;
  word-break: break-all;
  color: hsl(208.9, 11.9%, 50%);
`

const Info = ({ password, showResult }) => {
  return(
    {/* Welcome message */}
    <InfoWrapper>
      {!showResult && <InfoText>Please, open the basic and/or advanced settings and choose which options do you want to use. Then, click on the button below to generate your password.</InfoText>}

      {/* New password */}
      {showResult && <InfoText>{password}</InfoText>}
    </InfoWrapper>
  )
}

export default Info
```

## Creating the password generator

This will be really the final step. It will also be the step where I will let the code do the talking, along with a few comments. The reason for this is that this article is already quite long. Explaining the whole thing would make this article at least twice as big. So, please forgive me for now and let's focus on building an app with electron and React. Okay, let's open the `src/App/App.jsx` and find the `generatePassword` method. Then, use replace it with following code.

```
generatePassword() {
  // Check if user chose any option
  if (!this.state.settingsNumbers && !this.state.settingsLower && !this.state.settingsUpper && !this.state.settingsAsci && !this.state.settingsSpace && this.state.settingsCustom.length === 0 && this.state.settingsEntropy === 0) {
    return dialog.showMessageBox({type: 'warning', buttons: ['Close'], message: 'You didn\'t choose any options.'})
  }

  // Check the length of the password
  if (parseInt(this.state.settingsLength) === 0 || parseInt(this.state.settingsLength) < 0 || this.state.settingsLength === '') {
    return dialog.showMessageBox({type: 'warning', buttons: ['Close'], message: 'The password must be longer than 0.'})
  }

  // Variable for set of characters based on user's choice
  let characters = ''

  // Set of characters we will use according to the options
  const charactersSets = [
    [this.state.settingsAsci, '!\'#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'],
    [this.state.settingsCustom.length !== 0, this.state.settingsCustom],
    [this.state.settingsLower, 'abcdefghijklmnopqrstuvwxyz'],
    [this.state.settingsNumbers, '0123456789'],
    [this.state.settingsSpace, ' '],
    [this.state.settingsUpper, 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'],
  ]

  // Variable for the final password
  let password = ''

  // Get all symbols chosen by the user from charactersSets and add them to characters
  charactersSets.map((i) => {
    if (i[0]) characters += i[1]
  })

  // Prepare new array that will not contain any duplicate symbols
  let charactersArray = []

  // Remove duplicate symbols from characters and push them to charactersArray
  for (let i = 0; i < characters.length; i++) {
    let c = characters.charCodeAt(i)

    let s = null

    if (c < 0xD800 || c >= 0xE000) { // Regular UTF-16 symbols
      s = characters.charAt(i)
    } else if (0xD800 <= c && c < 0xDC00) { // Uppercase surrogate
      if (i + 1 < characters.length) {
        let d = characters.charCodeAt(i + 1)

        if (0xDC00 <= d && d < 0xE000) {
          // Valid symbols in supplementary plane
          s = characters.substr(i, 2)

          i++
        }
      }
    // Else remove unpaired surrogate
    } else if (0xDC00 <= d && d < 0xE000) { // Lowercase surrogate
      i++  // Remove unpaired surrogate
    }

    if (s !== null && charactersArray.indexOf(s) === -1) {
      charactersArray.push(s)
    }
  }

  // Check if user wants to use entropy and generate a random password
  if (parseInt(this.state.settingsEntropy) !== 0 || parseInt(this.state.settingsEntropy) > 0 || parseInt(this.state.settingsEntropy) && this.state.settingsEntropy !== '') {
    let entropy = Math.ceil(parseInt(this.state.settingsEntropy) * Math.log(2) / Math.log(charactersArray.length))

    for (let i = 0; i < entropy; i++) {
      password += charactersArray[Math.floor(Math.random() * charactersArray.length)]
    }
  } else {
    // Otherwise, use the length chosen by the user and charactersArray to generate a random password that matches
    for (let i = 0; i < this.state.settingsLength; i++) {
      password += charactersArray[Math.floor(Math.random() * charactersArray.length)]
    }
  }

  // Make sure none of the setting screens is open and update the 'password' and 'showResult' keys
  this.setState({
    password: password,
    showAdvancedSettings: false,
    showBasicSettings: false,
    showResult: true
  })
}
```

## Closing thoughts on how to [build password] generator

This is the end. Congratulations! You've just created your own password generator app with electron and React. If everything went well, you can now use `npm run start` in your terminal or command line and launch the app. I hope you enjoyed this final part and weren't disappointed because we didn't spend much of the time on the `generatePassword` method itself. Now, go ahead and try your new password generator! You can use [passwordmeter] to see how strong passwords you can create.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->

[part 1]: password-generator-pt1/
[part 2]: password-generator-pt2/
[GitHub]: https://github.com/alexdevero/password-generator
[passwordmeter]: http://www.passwordmeter.com/
