# How I Built My First [Electron App] & You Can Too Pt.4 – Adding Timer & Notification

Building an electron app is so easy anyone can do it! All you need is just an idea. Then, this mini series will show you how to take your idea and build your first electron app, step-by-step. In this part, our goal will be creating, and then implementing, Timer component with a simple notification for our Grease the Groove electron app. Without further ado, let’s begin ... and have some fun!

<!--
Table of Contents:
## Building the Timer component
### Setting up the state
### Converting the time to seconds, minutes and hours
### Mount, start, stop and ... restart
### Creating the countdown
### Creating a simple notification
### Putting the Timer component together
## Implementing the Timer component
## Closing thoughts on building an electron app
-->
How I Built My First Electron App & You Can Too [part 1].
How I Built My First Electron App & You Can Too [part 2].
How I Built My First Electron App & You Can Too [part 3].

Before we begin, let me quickly show you the folder structure, we discussed in the second part. It will make navigating through the project much easier and faster for us. Whenever you will not know where to go, you can take a look here.

```
grease-the-groove-app
├── builds/
├── dist/
├── node_modules/
├── src/
│   └── app/
│       └── components/
│       └── App.jsx
│   └── assets/
│       └── grease-the-groove-icon.ico
│       └── grease-the-groove-icon.png
│       └── grease-the-groove-icon.svg
│   └── index.js
├── .babelrc
├── .editorconfig
├── main.js
├── package.json
├── README.md
├── webpack.build.config.js
├── webpack.dev.config.js
└── yarn.lock
```

## Building the Timer component

In the end of the previous part, I promised you that today we will start with creating and implementing component for Timer for our electron app. So, let's start with this challenge, or puzzle. Let's tackle the hardest task for this part right in the beginning. First, navigate to the `src/app/components` directory and create a new file called `Timer.jsx` here. Now, let' open this file and put together the code we will need to get our timer up and running.

Let's talk about the timer. What is the necessary functionality, the must-haves, we would like to have? First, we need to create a method that will convert the time user set to more readable format. This means converting user's input to seconds, minutes and hours so we can then display these values. Next, we add a method that will take the value of `pauseLength` prop and store it inside `state`. `componentDidMount` will do the job. This also means that timer will be a stateful component.

Next, we can add a few more methods that will allow us, and any other potential user, to start, stop and restart the timer. These features will make our electron app more useful and easier to work with. Then, we will need a method for the timer itself, or the countdown. This method will decrease the length of rest pause by 1 second and update specific keys inside `state`. With every decrease, or cycle, it will also check if we are at 0. If so, it will stop the timer.

Finally, let's also add one additional and very simple method that will play a sound and show JavaScript alert popup window. We can then use this as a notification to let the user know that the rest pause ended and that it is time to grease the groove and do another set.

### Setting up the state

Let's start with the skeleton of the `Timer` component and setting up the `state`. `state` will contain three items. These will be `isTimerRunning`, `seconds` and `time`. `isTimerRunning` will be a boolean and we will use it as a indicator whether timer is running or not. `seconds` will store the length of the rest pause in seconds. `time` will be an object that will store remaining time in seconds, minutes and hours, one key/value pair for each.

Next, still in the `constructor` let's also bind the methods we will create for our Timer component. These are `countDown`, `playSound`, `restartTimer`, `startTimer` and `stopTimer`. Let's also add one additional variable, `timer`, we will later use to start and stop the timer. And, this is all we need for now.

```
// Import React library
import React from 'react'

// Component for Timer
export default class Timer extends React.Component {
  constructor(props) {
    super(props)

    // Create state with default key we will use later.
    this.state = {
      isTimerRunning: false,
      seconds: this.props.pauseLength * 60,
      time: {}
    }

    this.timer = 0

    // Bind methods we will use
    this.countDown = this.countDown.bind(this)
    this.playSound = this.playSound.bind(this)
    this.restartTimer = this.restartTimer.bind(this)
    this.startTimer = this.startTimer.bind(this)
    this.stopTimer = this.stopTimer.bind(this)
  }
}
```

### Converting the time to seconds, minutes and hours

Now, we can create the first method for our Timer. This method, let's call it `timeConverter`, will allow our electron app to accept user's input for how long she wants to rest. Then, it will convert these data into seconds, minutes and hours. Finally, it will store these values into an object and return it.

```
// Method for converting and formatting seconds to more readable format.
timeConverter(secs) {
  let hours = Math.floor(secs / (60 * 60))

  let minutesDivisor = secs % (60 * 60)
  let minutes = Math.floor(minutesDivisor / 60)

  let secondsDivisor = minutesDivisor % 60
  let seconds = Math.ceil(secondsDivisor)

  let obj = {
    'h': hours,
    'm': minutes,
    's': seconds
  }

  return obj
}
```

### Mount, start, stop and ... restart

Now, let's tackle the simpler and smaller methods that will add some usefullness into our electron app. The methods I am talking about, we will create as next, will be `startTimer`, `stopTimer`, `restartTimer`. The `startTimer` will check whether the timer is running and if not it will start it by using `setInterval` and `countDown` methods. We will create the `countDown` method right after these. The `stopTimer` method will stop the timer by "clearing" the currently running interval. Then, it will set the `isTimerRunning` to false.

The third method, `restartTimer`, will also stop the timer by "clearing" the currently running interval. Then, it will take the predefined length of the rest pause from `pauseLength` prop, convert it with `timeConverter`, decrease the time by 1 second and update specific keys inside `state`, namelly the `isTimerRunning`, `seconds` and `time`. But before these, let's quickly add `componentDidMount` method that will update the `time` key inside `state` with value of `pauseLength` prop, after formatting it.

```
// When component is mounted, update the state.
// with new data for 'time' key (the length of pause between sets).
componentDidMount() {
  let restPauseLength = this.props.pauseLength * 60 // pauseLength is in minutes

  this.setState({
    time: this.timeConverter(this.state.seconds)
  })
}

// Method for starting the timer.
startTimer() {
  if (!this.state.isTimerRunning) {
    this.timer = setInterval(this.countDown, 1000)
  }
}

// Method for stopping the timer.
stopTimer() {
  clearInterval(this.timer)

  this.setState({
    isTimerRunning: false
  })
}

// Method for restarting the timer.
// This method will stop the timer and revert it to its initial state.
restartTimer() {
  clearInterval(this.timer)

  let newTime = this.timeConverter(this.props.pauseLength * 60)
  let newSeconds = this.state.seconds - 1

  this.setState({
    isTimerRunning: false,
    seconds: this.props.pauseLength * 60,
    time: newTime
  })
}
```

### Creating the countdown

As next, let's create the core method for the timer, the counter. This method will take the time stored inside `seconds` key in `state`, decrease it by 1 second and update the `isTimerRunning`, `seconds`, `time` keys inside Timer `state`. Then, as the last thing, it will check if the timer is on 0. If so, it will play sound and display the notification and stop the timer by "clearing" the currently running interval.

```
// Method for the countdown.
countDown() {
  // Remove one second, set state so a re-render happens.
  let seconds = this.state.seconds - 1

  // Update specific keys in state.
  this.setState({
    isTimerRunning: true,
    seconds: seconds,
    time: this.timeConverter(seconds)
  })

  // If we're at 0 play notification sound and stop the timer.
  if (seconds === 0) {
    this.playSound()

    clearInterval(this.timer)
  }
}
```

### Creating a simple notification

It is time for the last method for our Timer component, as well as our electron app. There are already various npm packages for implementing native desktop notifications. However, I decided to keep it very simple for now and use only a sound and JavaScript `alert` popup window. To do this, we will use an mp3 file with a short sound. Let's import it in the beginning of this file (Timer component) to keep all imports on one place.

Then, we will use that file file and create new `Audio` object, set the default volume and use `play` method to play the sound when `playSound` is called. When the sound is played, after some small delay (5 milliseconds), we will display the `alert` popup window with some message.

```
// Import sound for notification
import bellSound from './../../assets/definite.mp3'

// ... some code

// Method for playing notification sound
// and displaying a simple alert popup window.
playSound() {
  const soundFile = new Audio(bellSound);

  soundFile.volume = 1 // 0.5 is half volume

  soundFile.play()

  // Wait for 0.5s and display the notification
  // in the form of JavaScript alert popup window.
  setTimeout(() => {
    alert('Time to Grease the Groove!')
  }, 500)
}
```

### Putting the Timer component together

Now, let's put together all the parts we previously created and import the file for sound notification. We can put this file into `assets` directory, inside `src`. Then, we can create the structure to render the Timer component. The structure will be simple. One `p` element and three buttons, one for starting the timer, one for resetting it and one for stopping it.

```
// Import React library
import React from 'react'

// Import sound for notification
import bellSound from './../../assets/definite.mp3'

// Component for Timer
export default class Timer extends React.Component {
  constructor(props) {
    super(props)

    // Create state with default key we will use later.
    this.state = {
      isTimerRunning: false,
      seconds: this.props.pauseLength * 60,
      time: {}
    }

    this.timer = 0

    // Bind methods we will use
    this.countDown = this.countDown.bind(this)
    this.playSound = this.playSound.bind(this)
    this.restartTimer = this.restartTimer.bind(this)
    this.startTimer = this.startTimer.bind(this)
    this.stopTimer = this.stopTimer.bind(this)
  }

  // Method for converting and formatting seconds to more readable format.
  timeConverter(secs) {
    let hours = Math.floor(secs / (60 * 60))

    let minutesDivisor = secs % (60 * 60)
    let minutes = Math.floor(minutesDivisor / 60)

    let secondsDivisor = minutesDivisor % 60
    let seconds = Math.ceil(secondsDivisor)

    let obj = {
      'h': hours,
      'm': minutes,
      's': seconds
    }

    return obj
  }

  // When component is mounted, update the state.
  // with new data for 'time' key (the length of pause between sets).
  componentDidMount() {
    let restPauseLength = this.props.pauseLength * 60 // pauseLength is in minutes

    this.setState({
      time: this.timeConverter(this.state.seconds)
    })
  }

  // Method for starting the timer.
  startTimer() {
    if (!this.state.isTimerRunning) {
      this.timer = setInterval(this.countDown, 1000)
    }
  }

  // Method for stopping the timer.
  stopTimer() {
    clearInterval(this.timer)

    this.setState({
      isTimerRunning: false
    })
  }

  // Method for restarting the timer.
  // This method will stop the timer and revert it to its initial state.
  restartTimer() {
    clearInterval(this.timer)

    let newTime = this.timeConverter(this.props.pauseLength * 60)
    let newSeconds = this.state.seconds - 1

    this.setState({
      isTimerRunning: false,
      seconds: this.props.pauseLength * 60,
      time: newTime
    })
  }

  // Method for the countdown.
  countDown() {
    // Remove one second, set state so a re-render happens.
    let seconds = this.state.seconds - 1

    // Update specific keys in state.
    this.setState({
      isTimerRunning: true,
      seconds: seconds,
      time: this.timeConverter(seconds)
    })

    // If we're at zero play notification sound and stop the timer.
    if (seconds === 0) {
      this.playSound()

      clearInterval(this.timer)
    }
  }

  // Method for playing notification sound
  // and displaying a simple alert popup window.
  playSound() {
    const soundFile = new Audio(bellSound);

    soundFile.volume = 1 // 0.5 is half volume

    soundFile.play()

    // Wait for 0.5s and display the notification
    // in the form of JavaScript alert popup window.
    setTimeout(() => {
      alert('Time to Grease the Groove!')
    }, 500)
  }

  render() {
    return(
      <div>
        {/* Remaining rest time in readable format. */}
        <p>{this.state.time.h}h {this.state.time.m}m {this.state.time.s}s</p>

        {/* Buttons for interacting with timer. */}
        <button onClick={this.startTimer}>Start</button>

        <button onClick={this.restartTimer}>Reset</button>

        <button onClick={this.stopTimer}>Stop</button>
      </div>
    )
  }
}
```

## Implementing the Timer component

This is the last step is to implement our new Timer component into our electron app. We need to go back to `App.jsx` file. Here, we need to add new import for Timer at the top. Next, we can uncomment the timer component we already have inside `render` method.

```
// Import React library
import React from 'react'

// Import timer
import Timer from './components/Timer'

// Create the main component for our electron app
class App extends React.Component {

  // ... code from previus parts

  // Create the main render method
  render() {
    return (
      <div>
        <h1>Grease the Groove!</h1>

        <p>Are you ready to get stronger?</p>

        {/* Button to open/close the settings div */}
        <a href="#" onClick={(e) => this.toggleSettings(e)}>Settings</a>

        {/* Button to show/hide the Timer */}
        <a href="#" onClick={(e) => this.toggleTimer(e)}>Timer</a>

        {/* If the value of `isSettingsOpen` is true, open settings. */}
        {this.state.isSettingsOpen && <div className="settings">
          <p>How many sets do you want to do?</p>

          {/* Number input to let the user specify the number of sets he wants to do in a day. */}
          <input type="number" placeholder={this.state.numOfSets} onChange={(e) => this.updateNumOfSets(e)} />

          <p>How long should the rest pause be (in minutes)? You can use decimal numbers for seconds, i.e.: 0.2 for 12s.</p>

          {/* Number input to let the user specify the rest pause between sets. */}
          <input type="number" value={this.state.restPauseLength} onChange={(e) => this.updateRestPauseLength(e)} />
        </div>}

        {/* If the value of `isTimerShown` is true, show timer */}
        {/* and provide the timer with data about the length of the rest pause,
        stored inside app state via 'pauseLength' prop */}
        {this.state.isTimerShown && <Timer pauseLength={this.state.restPauseLength} />}

        {/* Create list of sets to do */}
        <ul>
          {this.generateSetsList()}
        </ul>
      </div>
    )
  }
}
```

It is time to test Let’s finally see the results of our work and run it for the first time. Well, almost. There is one last thing we have to do. We need to "tell" Webpack that we added an mp3 file. In other words, we need to add new test for "mp3" files, using `file-loader`, to the `rules` object. We also need to make sure to add this change into both configs, for build as well as for dev.

```
// webpack.build.config.js and webpack.dev.config.js
module.exports = {
  // ... the rest of the code

  module: {
    rules: [
      {
        test: /\.jsx?$/,
        use: [{ loader: 'babel-loader' }],
        include: defaultInclude
      },
      {
        test: /\.(jpe?g|png|gif|ico)$/,
        use: [{ loader: 'file-loader?name=img/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      },
      {
        test: /\.(eot|svg|ttf|woff|woff2)$/,
        use: [{ loader: 'file-loader?name=font/[name]__[hash:base64:5].[ext]' }],
        include: defaultInclude
      },
      {
        test: /\.mp3$/,
        use: 'file-loader'
      }
    ]
  },

  // ... the rest of the code
}
```

And, with this small change in place, we can finally fire up our command line or terminal and run either `yarn run dev` or `npm run dev` to start our electron app in dev mode and see the results of our today's work. If you followed this mini series, and used the code from previous parts, you should see your first electron app successfully launching. If not, check the command line, or terminal, and console and fix any errors that appeared.

## Closing thoughts on building an electron app

Congratulations! You just finished the fourth part of this mini series on building electron app. You've done a lot of work today. As a result, your new electron app now not only helps the user to log the sets. It also takes care about measuring the rest pause and notifying the user, with a simple notification, when it is time to grease the groove again. The last questions is, what is coming in the fifth, and probably also the last, part of this mini series?

In next part, we will take a look at how to improve the UI of our electron app. Our main goal and task will putting together styles and polishing the UI with `styled-components`. Then, we will take a look at how can we improve and clean up the code. In other words, we will polish our new electron on both sides, the visible as well as the hidden. After that, our electron app will be ready for official release.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 1]: https://blog.alexdevero.com/electron-app-pt1/
[part 2]: https://blog.alexdevero.com/electron-app-pt2/
[part 3]: https://blog.alexdevero.com/electron-app-pt3/

<!--
#### Resources:
-
-->
