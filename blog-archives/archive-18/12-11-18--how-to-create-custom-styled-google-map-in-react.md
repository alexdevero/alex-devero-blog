# How to Create a Custom-styled [Google Map] in React

Creating a custom-styled Google Map is easier than you think. No more default styles and ugly UI. Learn how to create Google Map that perfectly fits the design of your website or app. This article will teach you all you need to know to do it. Say No to generic maps. Unleash your creativity! Build maps that are usable and beautiful!

<!--
Table of Contents:
## Resolving dependencies
## Creating Google Map with custom styles and marker
## Adding custom styles
## Implementing Google Map component
## Creating the index.html
## Adding an info window
## Epilogue: How to Create a Custom-styled Google Map in React
-->

## Resolving dependencies

We need to install necessary dependencies before we jump right into React. These dependencies will be `react`, `react-dom`, `react-google-maps` and `react-scripts`. Use npm or yarn to install these dependencies, either `npm i react react-dom react-google-maps react-scripts` or `yarn add react react-dom react-google-maps react-scripts`.

Next, we will use `react-scripts` to create `start`, `build`, `test` and `eject` npm scripts. The final version of `package.json` can look like the example below.

```
{
  "name": "react-google-map-tutorial",
  "version": "0.1.0",
  "description": "A simple tutorial to create a custom-styled Google Map",
  "private": true,
  "main": "src/index.jsx",
  "keywords": [],
  "dependencies": {
    "react": "^16.6.1",
    "react-dom": "^16.6.1",
    "react-google-maps": "9.4.5",
    "react-scripts": "2.11.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```

## Creating Google Map with custom styles and marker

Let's start with creating the component for our custom-styled Google Map. Then, when we are done with this, we can create `index.jsx`. Here, we will take care of rendering our Google Map in DOM. Back to the map component. Let's create a new file called "GoogleMapWithMarker.jsx" and import React library. Then, we will also need to import necessary modules for Google Map, from `react-google-maps` library.

These modules are `withScriptjs`, `withGoogleMap`, `GoogleMap` and `Marker`. `withScriptjs`, `withGoogleMap` are HOCs. `GoogleMap` and `Marker` are UI components. I know. It is a lot of things, but all these pieces are necessary for the Google Map to work properly. Next, we can also add import for file with custom styles for our Google Map.

We will store these custom styles in JSON format in file called "GoogleMapStyles.json". We will take a look at the styles in right after we are done with this Google Map component. Next, we will import an image in svg format for custom map marker. Since we are talking about the marker, there is one thing we should discuss.

There are two ways for using the marker. First, we can import in the form of an external file and use that file. Second, we can use inline version. Meaning, we can use the code for svg or png as a value for `url` key inside `icon` settings object for Marker. This may not work in IE11. If you need to support this browser, for whatever reason use the first option. In this tutorial, we will use the second, inlined, version.

Now, let's take a look at the Google Map component. Let's create functional component called "GoogleMapComponentWithMarker". This component will contain `GoogleMap` component. This component will have some default props. These props are `defaultZoom`, `defaultCenter` and `defaultOptions`. The `defaultZoom` is for setting the zoom level of the map.

The `defaultCenter` is for setting the center of the map. Finally, the `defaultOptions` allows us to modify the behavior and style of our Google Map. For example, we can disable map's default and annoying UI by setting `disableDefaultUI` to `true`. We can also choose if the map should be draggable or not, by setting `draggable` either to `true` or `false`.

We can also disable or enable keyboard shortcuts via `keyboardShortcuts`, scale control via `scaleControl` and mouse wheel via `scrollwheel`. And, we can also change default styles of the map with `styles`. There is a bunch of other options available for `GoogleMap` and you can find them all in [docs]. We will use those I mentioned above.

Inside the `GoogleMap` component will be `Marker` component. It will have two props, `icon` and `position`. We will use `icon` prop to implement our custom map marker and `position` to place the marker on the map. Position has two keys, `lat` for latitude and `lng` for longitude. Finally, we will wrap all this in `withScriptjs` and `withGoogleMap` HOCs.

```
// GoogleMapWithMarker.jsx

// Import React
import * as React from 'react'

// Import necessary components for React Google Maps
import {
  withScriptjs,
  withGoogleMap,
  GoogleMap,
  Marker
} from 'react-google-maps'

// Import custom styles to customize the style of Google Map
const styles = require('./GoogleMapStyles.json')

// Import custom icon for map marker
// You can use this if you need to support IE11 and lower.
// const mapMarker = require('./GoogleMapMarker.svg')

// Google Map component
const GoogleMapComponentWithMarker = withScriptjs(
  withGoogleMap(props => (
    <GoogleMap
      defaultZoom={13}
      defaultCenter={{
        lat: 40.7484445, // latitude for the center of the map
        lng: -73.9878584 // longitude for the center of the map
      }}
      defaultOptions={{
        disableDefaultUI: true, // disable default map UI
        draggable: true, // make map draggable
        keyboardShortcuts: false, // disable keyboard shortcuts
        scaleControl: true, // allow scale controle
        scrollwheel: true, // allow scroll wheel
        styles: styles // change default map styles
      }}
    >
      <Marker
        icon={{
          url:
            'data:image/svg+xml;utf-8, \
            <svg xmlns="http://www.w3.org/2000/svg" width="45" viewBox="0 0 512 512"><path fill="#e74c3c" d="M252.55 0h5.95c33.76.52 67.31 11.19 94.97 30.59 27.22 18.94 48.77 45.95 61.03 76.77 13.14 32.69 15.69 69.52 7.17 103.71-4.69 19.44-13.24 37.77-24.07 54.54-43.51 75.53-86.86 151.15-130.3 226.72-3.45 6.37-7.56 12.4-10.59 18.97l-.03.7h-1.21c-1.09-3.48-3.25-6.44-4.99-9.6-45.11-78.52-90.2-157.06-135.34-235.57-11.21-17.1-19.98-35.9-24.82-55.81-8.5-34.15-5.96-70.94 7.16-103.6 12.26-30.85 33.82-57.89 61.07-76.84C185.94 11.35 219.12.74 252.55 0m-6.26 64.44c-35.07 2.83-67.55 24.7-84.18 55.59-12.65 23.12-15.96 51.04-9.61 76.57 5.91 23.77 20.39 45.27 40.13 59.76 15.73 11.8 34.8 19.03 54.4 20.59 25.3 2.2 51.34-4.95 71.73-20.15 21.42-15.44 36.67-39.16 41.84-65.06 3.31-17.12 2.61-35.08-2.44-51.8-7.43-24.97-24.51-46.85-46.76-60.35-19.27-12.01-42.54-17.21-65.11-15.15z" /><path fill="#c0392b" d="M246.29 64.44c22.57-2.06 45.84 3.14 65.11 15.15 22.25 13.5 39.33 35.38 46.76 60.35 5.05 16.72 5.75 34.68 2.44 51.8-5.17 25.9-20.42 49.62-41.84 65.06-20.39 15.2-46.43 22.35-71.73 20.15-19.6-1.56-38.67-8.79-54.4-20.59-19.74-14.49-34.22-35.99-40.13-59.76-6.35-25.53-3.04-53.45 9.61-76.57 16.63-30.89 49.11-52.76 84.18-55.59m1.83 42.76c-15.04 1.8-29.3 9.21-39.45 20.45-10.03 10.95-16.02 25.5-16.56 40.34-.67 14.62 3.9 29.41 12.74 41.08 9.61 12.84 24.18 21.87 39.99 24.58 13.71 2.43 28.21.28 40.55-6.18 13.67-7.04 24.63-19.16 30.18-33.5 5.65-14.32 5.84-30.7.55-45.15-4.99-13.88-15-25.86-27.72-33.3-12.03-7.13-26.42-10.05-40.28-8.32z" /></svg>' // This may not work in <=IE11
        }}
        position={{
          lat: 40.7484445, // latitude to position the marker
          lng: -73.9878584 // longitude to position the marker
        }}
      />
    </GoogleMap>
  ))
)

// Export Google Map component
export default GoogleMapComponentWithMarker
```

## Adding custom styles

The component for our Google Map is complete. Now, let's take care of custom styles. As we discussed, we will store them in `GoogleMapStyles.json`. The theme I used is from [Snazzy Maps]. This website contains a large collection of various themes. Light, dark, you will probably find one that fits your needs.

If you will not find any theme you like, you can create your own. Snazzy maps provide a simple editor to do that. So, you can make your own custom style in a few minutes. Another option is to choose existing style and then use the editor to customize it. This will help you create stunning theme for your Google Map even faster.

Below is an example of a dark theme. The theme should load immediately because we already set the filename as the value for `styles` key in `defaultOptions` prop in `GoogleMap` component above.

_Side note: there is one reason the custom style may not load. Google Map will not allow to use custom theme in "development" mode. This means that you will need to use your API key and include it in URL for Google Map. We will take care of this in the next section._

```
[
  {
    "featureType": "all",
    "elementType": "labels",
    "stylers": [
      {
        "visibility": "on"
      }
    ]
  },
  {
    "featureType": "all",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "saturation": 36
      },
      {
        "color": "#000000"
      },
      {
        "lightness": 40
      }
    ]
  },
  {
    "featureType": "all",
    "elementType": "labels.text.stroke",
    "stylers": [
      {
        "visibility": "on"
      },
      {
        "color": "#000000"
      },
      {
        "lightness": 16
      }
    ]
  },
  {
    "featureType": "all",
    "elementType": "labels.icon",
    "stylers": [
      {
        "visibility": "off"
      }
    ]
  },
  {
    "featureType": "administrative",
    "elementType": "geometry.fill",
    "stylers": [
      {
        "color": "#000000"
      },
      {
        "lightness": 20
      }
    ]
  },
  {
    "featureType": "administrative",
    "elementType": "geometry.stroke",
    "stylers": [
      {
        "color": "#000000"
      },
      {
        "lightness": 17
      },
      {
        "weight": 1.2
      }
    ]
  },
  {
    "featureType": "administrative.country",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#838383"
      }
    ]
  },
  {
    "featureType": "administrative.locality",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#c4c4c4"
      }
    ]
  },
  {
    "featureType": "administrative.neighborhood",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#aaaaaa"
      }
    ]
  },
  {
    "featureType": "landscape",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#151516"
      },
      {
        "lightness": "0"
      }
    ]
  },
  {
    "featureType": "poi",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#000000"
      },
      {
        "lightness": 21
      },
      {
        "visibility": "on"
      }
    ]
  },
  {
    "featureType": "poi",
    "elementType": "labels",
    "stylers": [
      {
        "visibility": "off"
      },
      {
        "hue": "#ff0000"
      }
    ]
  },
  {
    "featureType": "poi",
    "elementType": "labels.icon",
    "stylers": [
      {
        "saturation": "-100"
      }
    ]
  },
  {
    "featureType": "poi.business",
    "elementType": "geometry",
    "stylers": [
      {
        "visibility": "on"
      }
    ]
  },
  {
    "featureType": "road.highway",
    "elementType": "geometry.fill",
    "stylers": [
      {
        "color": "#6e6e6e"
      },
      {
        "lightness": "0"
      }
    ]
  },
  {
    "featureType": "road.highway",
    "elementType": "geometry.stroke",
    "stylers": [
      {
        "visibility": "off"
      }
    ]
  },
  {
    "featureType": "road.arterial",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#000000"
      },
      {
        "lightness": 18
      }
    ]
  },
  {
    "featureType": "road.arterial",
    "elementType": "geometry.fill",
    "stylers": [
      {
        "color": "#575757"
      }
    ]
  },
  {
    "featureType": "road.arterial",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#c3c3c3"
      }
    ]
  },
  {
    "featureType": "road.arterial",
    "elementType": "labels.text.stroke",
    "stylers": [
      {
        "color": "#2c2c2c"
      }
    ]
  },
  {
    "featureType": "road.local",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#000000"
      },
      {
        "lightness": 16
      }
    ]
  },
  {
    "featureType": "road.local",
    "elementType": "labels.text.fill",
    "stylers": [
      {
        "color": "#5f5f5f"
      },
      {
        "visibility": "on"
      }
    ]
  },
  {
    "featureType": "road.local",
    "elementType": "labels.text.stroke",
    "stylers": [
      {
        "visibility": "off"
      }
    ]
  },
  {
    "featureType": "transit",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#717171"
      },
      {
        "lightness": 19
      }
    ]
  },
  {
    "featureType": "water",
    "elementType": "geometry",
    "stylers": [
      {
        "color": "#000000"
      },
      {
        "lightness": 17
      }
    ]
  }
]
```

## Implementing Google Map component

Now, it is time for the last but one step, implementing our custom-styled Google Map. This will be quick. First, we will import `React` and `React-DOM` libraries. Then, the `GoogleMapComponentWithMarker` component. We can also add some default styles, at least some fixed `height` for map container. After that will come the main component. Let's call it "MapWrapper".

We will create the `MapWrapper` component is `PureComponent`. It will return one `div` element. This `div` will contain our `GoogleMapComponentWithMarker` component. This component will need a number of props, namely `googleMapURL`, `loadingElement`, `containerElement` and `mapElement`. All these props are necessary.

The `loadingElement`, `containerElement` and `mapElement` accept HTML elements used for the Google map. The `googleMapURL` is for calling Google Map API and also for setting our API key. The API key is at the end of the URL, right after `&key=`. Remember that you need to use your own API key in order to load the map properly, not in "development" mode.

We talked about this in the side note in section about styles. When you load the map without any key, in "development" mode, custom styles will not work. You will see the default Google map. So, if you don't see map with custom styles it might be caused by missing API key, not your code.

```
// index.jsx

// Import React and React DOM
import * as React from 'react'
import { render } from 'react-dom'

// Import Google Map component
import GoogleMapComponentWithMarker from './GoogleMapWithMarker'

// Some default styles
const styles = {
  width: '100%',
  height: '536px'
}

// Wrapper with Google Map component
class MapWrapper extends React.PureComponent {
  render() {
    return (
      <div style={styles}>
        <GoogleMapComponentWithMarker
          googleMapURL="https://maps.googleapis.com/maps/api/js?v=3.exp&libraries=geometry,drawing,places&key="
          loadingElement={<div style={{ height: `100%` }} />}
          containerElement={<div style={{ height: `100%` }} />}
          mapElement={<div style={{ height: `100%` }} />}
        />
      </div>
    )
  }
}

// Render everything in HTML
render(<MapWrapper />, document.getElementById('root'))
```

## Creating the index.html

This will be the very last step we need to make. We need some place where we can render the custom-styled Google Map we created. This will be a very simple HTML file. We can use the default HTML template used in [create-react-app] project.

```
<!-- index.html -->

<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">
    <!--
      manifest.json provides metadata used when your web app is added to the
      homescreen on Android. See https://developers.google.com/web/fundamentals/engage-and-retain/web-app-manifest/
    -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json">
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    <!--
      Notice the use of %PUBLIC_URL% in the tags above.
      It will be replaced with the URL of the `public` folder during the build.
      Only files inside the `public` folder can be referenced from the HTML.

      Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
      work correctly both with client-side routing and a non-root public URL.
      Learn how to configure a non-root public URL by running `npm run build`.
    -->
    <title>React App</title>

  </head>

  <body>
    <div id="root"></div>
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
  </body>
</html>
```

## Adding an info window

Having a custom-styled Google Map is cool. What about adding some info window to the map marker? This can be additional contact information such as address, phone, or just anything you want. This will be easy. The first thing we need to do is update the `GoogleMapComponentWithMarker` component we created in `GoogleMapWithMarker.jsx`.

Let's open this file. Here, we will need to import additional module called `InfoWindow` from `react-google-maps`. Next, we will create new component, `InfoWindow`, right below `Marker` component inside the `GoogleMapComponentWithMarker` component. It will have three props, `position`, `visible` and `onCloseClick`. We will provide data for these props via props passed to `GoogleMapComponentWithMarker` in `index.jsx`.

The `position` prop works just like the `position` prop in `Marker`. It is used to place the info window on the map. The `onCloseClick` is a handler for event triggered by closing the info window. After that, will use `visible` prop to determine if the info box should be visible, `visible` is `true`, or not, `visible` is `false`.

One more thing. Let's add handler for `onClick` to the `Marker` component. We will use this handler to get `message`, `lang` and `lat` from it. We will use the content of `message` will be used as the text inside info window. The `lang` and `lat` will help us position the info window on the map, right above the marker.

```
// Import React
import * as React from 'react'

// Import necessary components for React Google Maps
import {
  withScriptjs,
  withGoogleMap,
  GoogleMap,
  InfoWindow,
  Marker
} from 'react-google-maps' // Add "InfoWindow"

// Import custom styles to customize the style of Google Map
const styles = require('./GoogleMapStyles.json')

// Import custom icon for map marker
// const mapMarker = require('./GoogleMapMarker.svg')

// Google Map component
const GoogleMapComponentWithMarker = withScriptjs(
  withGoogleMap(props => (
    <GoogleMap
      defaultZoom={13}
      defaultCenter={{
        lat: 40.7484445,
        lng: -73.9878584
      }}
      defaultOptions={{
        disableDefaultUI: true,
        draggable: true,
        keyboardShortcuts: false,
        scaleControl: true,
        scrollwheel: true,
        styles: styles
      }}
    >
      <Marker
        icon={{
          url:
            'data:image/svg+xml;utf-8, \
            <svg xmlns="http://www.w3.org/2000/svg" width="45" viewBox="0 0 512 512"><path fill="#e74c3c" d="M252.55 0h5.95c33.76.52 67.31 11.19 94.97 30.59 27.22 18.94 48.77 45.95 61.03 76.77 13.14 32.69 15.69 69.52 7.17 103.71-4.69 19.44-13.24 37.77-24.07 54.54-43.51 75.53-86.86 151.15-130.3 226.72-3.45 6.37-7.56 12.4-10.59 18.97l-.03.7h-1.21c-1.09-3.48-3.25-6.44-4.99-9.6-45.11-78.52-90.2-157.06-135.34-235.57-11.21-17.1-19.98-35.9-24.82-55.81-8.5-34.15-5.96-70.94 7.16-103.6 12.26-30.85 33.82-57.89 61.07-76.84C185.94 11.35 219.12.74 252.55 0m-6.26 64.44c-35.07 2.83-67.55 24.7-84.18 55.59-12.65 23.12-15.96 51.04-9.61 76.57 5.91 23.77 20.39 45.27 40.13 59.76 15.73 11.8 34.8 19.03 54.4 20.59 25.3 2.2 51.34-4.95 71.73-20.15 21.42-15.44 36.67-39.16 41.84-65.06 3.31-17.12 2.61-35.08-2.44-51.8-7.43-24.97-24.51-46.85-46.76-60.35-19.27-12.01-42.54-17.21-65.11-15.15z" /><path fill="#c0392b" d="M246.29 64.44c22.57-2.06 45.84 3.14 65.11 15.15 22.25 13.5 39.33 35.38 46.76 60.35 5.05 16.72 5.75 34.68 2.44 51.8-5.17 25.9-20.42 49.62-41.84 65.06-20.39 15.2-46.43 22.35-71.73 20.15-19.6-1.56-38.67-8.79-54.4-20.59-19.74-14.49-34.22-35.99-40.13-59.76-6.35-25.53-3.04-53.45 9.61-76.57 16.63-30.89 49.11-52.76 84.18-55.59m1.83 42.76c-15.04 1.8-29.3 9.21-39.45 20.45-10.03 10.95-16.02 25.5-16.56 40.34-.67 14.62 3.9 29.41 12.74 41.08 9.61 12.84 24.18 21.87 39.99 24.58 13.71 2.43 28.21.28 40.55-6.18 13.67-7.04 24.63-19.16 30.18-33.5 5.65-14.32 5.84-30.7.55-45.15-4.99-13.88-15-25.86-27.72-33.3-12.03-7.13-26.42-10.05-40.28-8.32z" /></svg>' // This may not work in <=IE11
        }}
        position={{
          lat: 40.7484445,
          lng: -73.9878584
        }}
        onClick={(message, lang, lat) =>
          props.handleMarkerClick(
            'Custom Google Map marker with infobox!',
            40.7484445,
            -73.9878584
          )
        } // Get the data that will be used for InfoWindow.
      />

      {props.isInfoboxVisible && (
        <InfoWindow
          position={{
            lat: props.infoboxPosY,
            lng: props.infoboxPosX
          }}
          onCloseClick={() => props.handleInfoboxClick()}
        >
          <div>
            <h4>{props.infoboxMessage}</h4>
          </div>
        </InfoWindow>
      )}
    </GoogleMap>
  ))
)

// Export Google Map component
export default GoogleMapComponentWithMarker
```

Next, we need to edit the `MapWrapper` component inside `index.jsx`. Here, we will add `state` and `handleMarkerClick` and `handleInfoboxClick` methods. The `state` will contain four keys, `infoboxMessage`, `isInfoboxVisible`, `markerLang` and `markerLat`. We will pass all these keys as well as the methods as props to `GoogleMapComponentWithMarker`.

The `handleMarkerClick` will get the `message`, `lang` and `lat` from map marker and update `state` of `MapWrapper` with new values. We need to adjust the values of `lang` and `lat` because we are using custom marker. Original values would place the info window at the place where is the marker. In other words, the info window would cover the marker.

In addition to this, `handleMarkerClick` will also show the info window, by changing `isInfoboxVisible`. As previously, remember to include your Google Map API at the end of `googleMapURL`. If you want, you can skip passing keys of `state` as individual props and pass the whole `state` instead as one prop. Use the option you like.

```
// Import React and React DOM
import * as React from 'react'
import { render } from 'react-dom'

// Import Google Map component
import GoogleMapComponentWithMarker from './GoogleMapWithMarker'

// Some default styles
const styles = {
  width: '100%',
  height: '536px'
}

// Wrapper with Google Map component
class MapWrapper extends React.PureComponent {
  constructor(props) {
    super(props)

    this.state = {
      infoboxMessage: '',
      isInfoboxVisible: false,
      markerLang: 0,
      markerLat: 0
    }
  }

  handleMarkerClick = (message, lang, lat) => {
    this.setState({
      infoboxMessage: message, // Message shown in info window
      isInfoboxVisible: !this.state.isInfoboxVisible, // Show info window
      markerLang: lang + 0.006, // Y coordinate for positioning info window
      markerLat: lat - 0.0004 // X coordinate for positioning info window
    })
  }

  handleInfoboxClick = () => {
    this.setState({
      isInfoboxVisible: false
    })
  }

  render() {
    return (
      <div style={styles}>
        <GoogleMapComponentWithMarker
          googleMapURL="https://maps.googleapis.com/maps/api/js?v=3.exp&libraries=geometry,drawing,places&key="
          loadingElement={<div style={{ height: `100%` }} />}
          containerElement={<div style={{ height: `100%` }} />}
          mapElement={<div style={{ height: `100%` }} />}
          isInfoboxVisible={this.state.isInfoboxVisible} // Show/hide info window
          infoboxMessage={this.state.infoboxMessage} // Message shown in info window
          handleInfoboxClick={this.handleInfoboxClick} // Handle closing of the info window
          handleMarkerClick={this.handleMarkerClick} // Handle click on Marker component
          infoboxPosY={this.state.markerLang} // Y coordinate for positioning info window
          infoboxPosX={this.state.markerLat} // X coordinate for positioning info window
        />
      </div>
    )
  }
}

// Render everything in HTML
render(<MapWrapper />, document.getElementById('root'))
```

## Epilogue: How to Create a Custom-styled Google Map in React

Congratulations, you've made it! You've created your own custom-styled Google Map. From now on, you will know how to create maps that no longer look like every other map on the Internet. What's more, you know how to create map and customize it so it will fit any design. No more default styles and ugly UIs. No more limitations. Go and unleash your creativity!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[npm]: https://www.npmjs.com
[yarn]: https://yarnpkg.com/lang/en/
[docs]: https://tomchentw.github.io/react-google-maps/#googlemap
[Snazzy Maps]: https://snazzymaps.com/
[create-react-app]: https://github.com/facebook/create-react-app

<!-- https://codesandbox.io/s/0qzkqp5vxp -->

<!--
### Meta:
-
-->

<!--
#### Resources:
-
-->
