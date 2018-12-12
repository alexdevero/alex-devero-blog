# [React Native] & Expo-How to Build Your First Mobile App

Have you heard about React native and Expo? Building desktop is great, but what about building mobile apps? What if you don't have access to Android or Apple device. Or, you don't want to learn Swift or Java. This is not a problem. React native and Expo allows you to build mobile apps on any platform for any platform. This tutorial will show you how to do it.

<!--
Table of Contents:
## Setting up the project Pt.1
## Setting up the project Pt.2
## Adding some constants
## Creating a simple component
## Building the navigation bar
## Creating a simple navigator switch for routing
## Building the App component
## Home screen
## About screen
## Settings screen
## Epilogue: React Native & Expo-How to Build Your First Mobile App
-->

## Setting up the project Pt.1

Before you start working on the app itself, there are some things to do. You will need to create a couple of configuration files. These files are `package.json`, `babel.config.js` and `app.json`. Then, you should also create `.gitignore`, at least if you plan to use git. There are some files generated automatically every time you run the project. These files don't need to be included in git. Let's start with this file.

```
# ./.gitignore
node_modules/**/*
.expo/*
npm-debug.*
*.jks
*.p12
*.key
*.mobileprovision
```

Next, you will need to install some dependencies to get this project up and running. Now, in order to use these dependencies, and start this project, you will also need a few npm scripts. These scripts include script for development, ejecting and testing. There will be actually three scripts for development-"default", one for Android and one for iOS.

Now, you will need need to specify the `main`, or the app entry. After that, you should also specify preset for `jest`. The answer for the second thing is `jest-expo`. And, for the first? You will use `AppEntry.js` from `expo` module. Now you are ready to install all dependencies with yarn or npm. So, `npm install` or `yarn`.

Aside to these, you will also probably need to install `expo-cli`. And, you should install this dependency globally.

```
// ./package.json
{
  "main": "node_modules/expo/AppEntry.js",
  "private": true,
  "jest": {
    "preset": "jest-expo"
  },
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "eject": "expo eject",
    "test": "node ./node_modules/jest/bin/jest.js --watchAll"
  },
  "dependencies": {
    "expo": "^31.0.2",
    "react": "16.5.0",
    "react-native": "https://github.com/expo/react-native/archive/sdk-31.0.0.tar.gz",
    "react-navigation": "^2.18.2"
  },
  "devDependencies": {
    "babel-preset-expo": "^5.0.0",
    "jest-expo": "^31.0.0"
  }
}
```

## Setting up the project Pt.2

That was the first part. There are two last steps to make. First, you will need to create `babel.config.js` to make sure the code is transpiled is it should be. Second, your app will need config in the form of JSON. This will be the main config file for Expo to set up your app and make it work properly. Let's start with `babel.config.js`.

```
// ./babel.config.js

module.exports = function(api) {
  api.cache(true)

  return {
    presets: ['babel-preset-expo']
  }
}
```

Then, let's put together the main config file for Expo. When you are done with this file, it is time to start working on the app itself.

```
// ./app.json
{
  "expo": {
    "name": "react-native-app",
    "slug": "react-native-app",
    "privacy": "public",
    "sdkVersion": "31.0.0",
    "platforms": [
      "ios",
      "android"
    ],
    "version": "0.0.1",
    "orientation": "portrait",
    "icon": "./assets/images/icon.png",
    "splash": {
      "image": "./assets/images/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "updates": {
      "fallbackToCacheTimeout": 0
    },
    "assetBundlePatterns": [
      "**/*"
    ],
    "ios": {
      "supportsTablet": true
    }
  }
}
```

_Side note: As you may have noticed, there are two external assets mentioned in the Expo config. Namely, 'icon' and 'image', inside 'splash'. All necessary information you need to create your custom splash image are in [splash screens Expo documentation]. And, for icon, head on to [app icons Expo documentation]. Then, create `./assets/images/` directory and put your icon and splash image there._

## Adding some constants

When you build your React native app, you may want to re-use some things. For example, you may want to use the same colors. This is a very good idea to make the design and style of your app consistent. So, let's create a new folder, called `constants` in the root. Then, inside this folder, create a new file called `Colors.js`.

Here, you can add colors for the default scenarios and states. For example, errors, active elements, warnings, notifications, tint colors and so on. And, don't forget to export your color palette.

```
// ./constants/Colors.js

const tintColor = '#2f95dc'

export default {
  tintColor,
  tabIconDefault: '#ccc',
  tabIconSelected: tintColor,
  tabBar: '#fefefe',
  errorBackground: 'red',
  errorText: '#fff',
  warningBackground: '#eaeb5e',
  warningText: '#666804',
  noticeBackground: tintColor,
  noticeText: '#fff'
}
```

After that, you may also want to have some general constants. For example, constants for the `width` and `height` of the device your app is running on. So, let's create one more file in the same directory called `Layout.js`. Here, you can use `Dimensions` module provided by React native to get the `width` and `height` of the device. Then, again make sure to export these constants.

```
// ./constants/Layout.js

// Import 'Dimensions' module from 'react-native'
import { Dimensions } from 'react-native'

// Create constants for app width and height
const width = Dimensions.get('window').width
const height = Dimensions.get('window').height

// Export everything
export default {
  window: {
    width,
    height
  },
  isSmallDevice: width < 375
}
```

## Creating a simple component

Now, let's build some simple component. This can be an icon that will be in the navigation bar, or the tap bar. Don't worry. You don't have to build your own icon from scratch. You can use `Icon` module from Expo and customize to your taste and needs. Below is a simple example of such an icon. You can call it `TabBarIcon` and put it in a new directory called `components`.

```
// ./components/TabBarIcon.js

// Import React and 'Icon' module from 'Expo'
import React from 'react'
import { Icon } from 'expo'

// Import color constants
import Colors from '../constants/Colors'

// Create, and export, component for navigation icon
export default class TabBarIcon extends React.Component {
  render() {
    return (
      <Icon.Ionicons
        name={this.props.name}
        size={26}
        style={{ marginBottom: -3 }}
        color={this.props.focused ? Colors.tabIconSelected : Colors.tabIconDefault}
      />
    )
  }
}
```

## Building the navigation bar

You have component for icon in tap bar, but you don't have any tab bar, yet. Let's build it. Again, this easier because React native do the majority of heavy lifting for you. You will start by importing React and one useful module from React native called `Platform`. This module will help you recognize what platform, OS specifically, is your app running on.

You can then use this information choose specific icon for iOS as well as Android. After that, you will also need to import `createStackNavigator`
and `createBottomTabNavigator` from `react-navigation`. You will use the `createStackNavigator` to specify what screen component to show on what screen. Then, you will use `createBottomTabNavigator` to create and export a simple tab bar on the bottom of the screen.

This tap bar will then allow you, and users of your app, to switch between different app screens, or routes. This also means that this is the place where you import all screen components for React native app.

```
// ./navigation/MainTabNavigator.js

// Import React and all necessary modules
import React from 'react'
import { Platform } from 'react-native'
import { createStackNavigator, createBottomTabNavigator } from 'react-navigation'

// Import screens
import HomeScreen from '../screens/HomeScreen'
import AboutScreen from '../screens/AboutScreen'
import SettingsScreen from '../screens/SettingsScreen'

// Import TabBarIcon component
import TabBarIcon from '../components/TabBarIcon'

// Add stack for Home screen
const HomeStack = createStackNavigator({
  Home: HomeScreen // Specify component for each screen
})

// Add stack for About screen
const AboutStack = createStackNavigator({
  About: AboutScreen // Specify component for each screen
})

// Add stack for Settings screen
const SettingsStack = createStackNavigator({
  Settings: SettingsScreen // Specify component for each screen
})

// Create and setup navigation item for Home screen
HomeStack.navigationOptions = {
  tabBarLabel: 'Home', // Text shown below the icon in tap bar
  tabBarIcon: ({ focused }) => (
    <TabBarIcon
      focused={focused}
      name={Platform.OS === 'ios' ? `ios-home` : 'md-home'}
    />
  )
}

// Create and setup navigation item for Settings screen
SettingsStack.navigationOptions = {
  tabBarLabel: 'Settings', // Text shown below the icon in tap bar
  tabBarIcon: ({ focused }) => (
    <TabBarIcon
      focused={focused}
      name={Platform.OS === 'ios' ? 'ios-options' : 'md-options'}
    />
  )
}

// Create and setup navigation item for About screen
AboutStack.navigationOptions = {
  tabBarLabel: 'About', // Text shown below the icon in tap bar
  tabBarIcon: ({ focused }) => (
    <TabBarIcon
      focused={focused}
      name={Platform.OS === 'ios' ? 'ios-information-circle' : 'md-information-circle'}
    />
  )
}

// Export stacks for all app screens
export default createBottomTabNavigator({
  HomeStack,
  AboutStack,
  SettingsStack
})
```

## Creating a simple navigator switch for routing

There is one last thing to finish the routing of your React native app. You need to create a navigator switch. The main job of this switch is to show only one screen at a time. To do this, you will use module form `react-navigation`, called `createSwitchNavigator`. This module will take care of everything.

Aside to that, you will also import React and the `MainTabNavigator` component you've created in previous section, the tap bar. Creating the navigator switch will be easy and fast. You will need just three lines of code. You will basically specify that the `MainTabNavigator` component is the main navigator switch. Then, as usually, make sure to export it.

```
// ./navigation/AppNavigator.js

// Import React and 'createSwitchNavigator' module from 'react-navigation'
import React from 'react'
import { createSwitchNavigator } from 'react-navigation'

// Import main navigation
import MainTabNavigator from './MainTabNavigator'

// Create, and export, navigator switch
export default createSwitchNavigator({
  Main: MainTabNavigator
})
```

## Building the App component

Now, let's put together the main App component. This component will be very simple. It will contain just one `view`, your `AppNavigator` component and default `StatusBar` if your React native app is running on iOS platform. [View] is the main building block for the UI of your app. If you are familiar with web development, you can think about it as `div`.

As usually, you will start by importing React and your `AppNavigator` component. What about the rest? Again, no need to write everything by yourself. Instead, you can import all necessary UI components as modules from React native library. And, you can also add some simple styles. And, as always, when you are done, make sure to export the `App` component.

```
// ./App.js

// Import React and necessary UI modules
import React from 'react'
import { Platform, StatusBar, StyleSheet, View } from 'react-native'

// Import main navigation
import AppNavigator from './navigation/AppNavigator'

// Add some simple styles
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  }
})

// Create and export the main App component
export default class App extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        {/* If app is running on iOS, show default status bar */}
        {Platform.OS === 'ios' && <StatusBar barStyle="default" />}

        {/* Show main app tap bar */}
        <AppNavigator />
      </View>
    )
  }
}
```

## Home screen

Okay, let's build your first screen. First, import React and all UI components you want to use from React native. The home screen itself can be simple. Just some heading can be enough. Along with some styles to make the screen looks pretty. You can also show a notification message that your app is in development or production mode.

Normally, using `view` as the main container would be enough. However, if you want to add something more, it might be a good idea to also use `ScrollView` component. This will allow you or other user to scroll. If you want to use this component, just make sure to nest it inside `view`. Finish your component for home screen by exporting it.

One thing. As you will see, your screen component contains static object called `navigationOptions`. This allows you to use a header above the rest of the content on the active screen. To do that, you just need to use some text. If you want to disable this header, set it to `null`.

```
// ./screens/HomeScreen.js

// Import React, necessary UI modules from React native
import React from 'react'
import { ScrollView, StyleSheet, Text, View } from 'react-native'

// Add some simple styles
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  },
  developmentModeText: {
    marginBottom: 20,
    color: 'rgba(0, 0, 0, .4)',
    fontSize: 14,
    lineHeight: 19,
    textAlign: 'center'
  },
  contentContainer: {
    paddingTop: 30,
  },
  welcomeContainer: {
    alignItems: 'center',
    marginTop: 10,
    marginBottom: 20
  },
  getStartedContainer: {
    alignItems: 'center',
    marginHorizontal: 50
  },
  welcomeText: {
    fontSize: 21,
    fontWeight: '700'
  }
})

// Create and export Home screen component
export default class HomeScreen extends React.Component {
  static navigationOptions = {
    header: null // disable app header
  }

  // Show notification about mode
  showDevelopmentModeWarning() {
    if (__DEV__) {
      return (
        <Text style={styles.developmentModeText}>
          Development mode is enabled, your app will be slower but you can use useful development
          tools.
        </Text>
      )
    } else {
      return (
        <Text style={styles.developmentModeText}>
          You are not in development mode, your app will run at full speed.
        </Text>
      )
    }
  }

  render() {
    return (
      <View style={styles.container}>
        <ScrollView style={styles.container} contentContainerStyle={styles.contentContainer}>
          <View style={styles.welcomeContainer}>
            <Text style={styles.welcomeText}>Welcome!</Text>
          </View>

          <View style={styles.getStartedContainer}>
            {this.showDevelopmentModeWarning()}
          </View>
        </ScrollView>
      </View>
    )
  }
}
```

## About screen

About screen can be another useful screen. You can use it to provide to user of your app with some additional useful information. For example, you can show the icon of your app, its name, slug and description. You can also show your name as well as the version of your app. Let's do it.

```
// ./screens/AboutScreen.js

// Import React and necessary UI modules
import React from 'react'
import { Text, ScrollView, StyleSheet, View } from 'react-native'
import { Icon } from 'expo'

// Add some simple styles
const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 15,
    backgroundColor: '#fff'
  },
  aboutTitleContainer: {
    paddingHorizontal: 15,
    paddingBottom: 15,
    paddingLeft: 8,
    flexDirection: 'row'
  },
  aboutTitleIconContainer: {
    marginRight: 15,
    paddingTop: 2
  },
  aboutNameText: {
    fontSize: 18,
    fontWeight: '600'
  },
  aboutSlugText: {
    fontSize: 14,
    color: '#a39f9f',
    backgroundColor: 'transparent'
  },
  aboutDescriptionText: {
    marginTop: 4,
    fontSize: 13,
    color: '#4d4d4d'
  },
  aboutHeaderContainer: {
    paddingVertical: 8,
    paddingHorizontal: 15,
    backgroundColor: '#fbfbfb',
    borderWidth: 1,
    borderColor: '#ededed'
  },
  aboutHeaderText: {
    fontSize: 14
  },
  aboutContentContainer: {
    paddingTop: 8,
    paddingBottom: 12,
    paddingHorizontal: 15
  },
  aboutContentText: {
    color: '#808080',
    fontSize: 14
  }
})

// Create and export About screen component
export default class AboutScreen extends React.Component {
  static navigationOptions = {
    title: 'About' // Enable app header and use 'About' as the label
  }

  render() {
    return (
      <ScrollView style={styles.container}>
        <View style={styles.aboutTitleContainer}>
          <View style={styles.aboutTitleIconContainer}>
            <Icon.Ionicons
              name="ios-home"
              size={60}
            />
          </View>

          <View style={styles.aboutTitleTextContainer}>
            <Text style={styles.aboutNameText} numberOfLines={1}>
              react-native-app
            </Text>

            <Text style={styles.aboutSlugText} numberOfLines={1}>
              react-native-app
            </Text>

            <Text style={styles.aboutDescriptionText}>
              Your first cool Reactive Native app.
            </Text>
          </View>
        </View>

        <View>
          <View style={styles.aboutHeaderContainer}>
            <Text style={styles.aboutHeaderText}>
              App name
            </Text>
          </View>

          <View style={styles.aboutContentContainer}>
            <Text style={styles.aboutContentText}>
              react-native-app
            </Text>
          </View>
        </View>

        <View>
          <View style={styles.aboutHeaderContainer}>
            <Text style={styles.aboutHeaderText}>
              Author
            </Text>
          </View>

          <View style={styles.aboutContentContainer}>
            <Text style={styles.aboutContentText}>
              John Doe
            </Text>
          </View>
        </View>

        <View>
          <View style={styles.aboutHeaderContainer}>
            <Text style={styles.aboutHeaderText}>
              Version
            </Text>
          </View>

          <View style={styles.aboutContentContainer}>
            <Text style={styles.aboutContentText}>
              0.0.1
            </Text>
          </View>
        </View>
      </ScrollView>
    )
  }
}
```

## Settings screen

Let's take your React native app a bit farther. How? You can create a simple settings screen with working switches. These switches will then allow to enable or disable features you may want to create later. The good news is that even building these switches will be blazing fast. Yes, React native library has all you need.

The only thing you have to do is to import the UI element, or module, you want to use, the `Switch`. And, for managing the on/off states of those switches? You can use React `state` with a simple method to change the state of switches from `true` to `false` or the other way around.

```
// ./screens/SettingsScreen.js

// Import React and necessary UI modules
import React from 'react'
import { Text, ScrollView, StyleSheet, Switch, View } from 'react-native'

// Import color constants
import Colors from '../constants/Colors'

// Add some simple styles
const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 15,
    backgroundColor: '#fff'
  },
  switchContainer: {
    display: 'flex',
    alignItems: 'center',
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 16,
    paddingHorizontal: 15
  },
  switchLabel: {
    flex: 0
  }
})

// Create and export Settings screen component
export default class SettingsScreen extends React.Component {
  static navigationOptions = {
    title: 'Settings' // Enable app header and use 'Settings' as the label
  }

  // Define default states for switch components
  state = {
    isOptionOneEnabled: false,
    isOptionTwoEnabled: false,
    isOptionThreeEnabled: false,
    isOptionFourEnabled: false
  }

  // Handle change of switch state
  handleSwitch = (option) => {
    this.setState({
      [option]: !this.state[option]
    })
  }

  render() {
    return (
      <ScrollView style={styles.container}>
        <View style={styles.switchContainer}>
          <Text style={styles.switchLabel}>
            Option 1
          </Text>

          <Switch trackColor={{true: Colors.tintColor}} onValueChange={() => this.handleSwitch('isOptionOneEnabled')} value={this.state.isOptionOneEnabled} />
        </View>

        <View style={styles.switchContainer}>
          <Text style={styles.switchLabel}>
            Option 2
          </Text>

          <Switch trackColor={{true: Colors.tintColor}} onValueChange={() => this.handleSwitch('isOptionTwoEnabled')} value={this.state.isOptionTwoEnabled} />
        </View>

        <View style={styles.switchContainer}>
          <Text style={styles.switchLabel}>
            Option 3
          </Text>

          <Switch trackColor={{true: Colors.tintColor}} onValueChange={() => this.handleSwitch('isOptionThreeEnabled')} value={this.state.isOptionThreeEnabled} />
        </View>

        <View style={styles.switchContainer}>
          <Text style={styles.switchLabel}>
            Option 4
          </Text>

          <Switch trackColor={{true: Colors.tintColor}} onValueChange={() => this.handleSwitch('isOptionFourEnabled')} value={this.state.isOptionFourEnabled} />
        </View>
      </ScrollView>
    )
  }
}
```

## Epilogue: React Native & Expo-How to Build Your First Mobile App

Congratulation! You've just built your own mobile app with React native and Expo! I hope you enjoyed this tutorial, had fun and learn a lot. However, this was just the beginning of your journey. There is much much more. So, where to go from here? There are two places where you should go. The first one is [Expo Documentation].

The second is documentation for React native. These two places contain all information you need to take your React native app to another level. Why to stick only with what you learned today. Now you know how to use React native and Expo to build that awesome app you always wanted to have. So, go ahead and build it!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[splash screens documentation]: https://docs.expo.io/versions/latest/guides/splash-screens
[app icons documentation]: https://docs.expo.io/versions/v31.0.0/guides/app-icons
[View]: https://facebook.github.io/react-native/docs/view
[Expo Documentation]: https://docs.expo.io/versions/latest/
[documentation]: https://facebook.github.io/react-native/

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
-
-->
