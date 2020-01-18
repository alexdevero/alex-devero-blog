# Build Your Own [Meme Generator] with React, React Hooks and TypeScript
Have you ever wanted to build your own meme generator? What about learning about React, React hooks and TypeScript? This tutorial will help you do both. Build your own meme generator and learn how to work with React, React Hooks and TypeScript at the same time!
<!--more-->
<!--
Table of Contents:
## Briefing
## Project setup
## Form component
## Content component
## Result component
## Main (index) component
### Imports
### Refs and states
### Fetching the API
### Handling the text inputs
### Handling the image change
### Handling the file input
### Generating the meme image
### Handling the "Reset" button
### Combining fetchImage with useEffect
### Returning all components
## Putting it all together
## Styles
## Conclusion: Build your own Meme Generator...
-->

You can find the code on my [GitHub].

## Briefing

This meme generator will allow you to generate png or jpg image from HTML content. This content can be anything you want. For this project, it will be a single image and two headings, positioned absolutely on the image. The first heading will be at the top of the image and the second will be at the bottom.

You will be able to add the image in two ways. First, the meme generator will fetch random image from `api.imgflip.com`. Don't worry, no token or registration required. Second, you will be able to open image from your disk, using `file` input. To generate the png or jpg file this meme generator will use `dom-to-image-more` package.

About the code. This tutorial will use React hooks such as `useState`, `useEffect` and `useRefs`. Since you will use hooks there is no need for class components. So, you will build all components for your meme generator as functional components. You will write this meme generator in TypeScript and you will also work with `interfaces` and `types`.

## Project setup

Let's set up the files you will need to build your meme generator. You can do this very quickly by using [create-react-app] as your starting template. If you want, you can install this package globally on your computer, with your favorite package manager ([pnpm], [yarn] or [npm]). However, this is not really necessary.

You can also create the starting template without installing anything. This can be done either with npx, instead of npm, or pnpx, instead of pnpm. These two commands will download the desired package, install it temporarily, automatically start it, and remove it after you are done. No need to fill your HDD.

One more thing, you will write this meme generator in [TypeScript], a superset of JavaScript. If you want to create the starter template with create-react-app with support for TypeScript you have to include `--typescript` flag in the command. If you don't want to use TypeScript in this project, omit the `--typescript` flag.

To the installation. For npx, use `npx create-react-app react-meme-generator-ts --typescript`. You can also use npm directly, `npm init react-meme-generator-ts --typescript`. For pnpx, it will be `npx create-react-app react-meme-generator-ts --typescript`. For yarn, use `yarn create react-app react-meme-generator-ts --typescript`.

These commands will create a starter template for your meme generator. Now, let's also add the `dom-to-image-more` package. When you are done with this, you are ready to start. Your `package.json` will look something like this:

```
{
  "name": "react-meme-generator-ts",
  "version": "1.0.0",
  "description": "Meme generator web app built with React, React hooks and TypeScript.",
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
    "dom-to-image-more": "2.8.0",
    "react": "16.11.0",
    "react-dom": "16.11.0",
    "react-scripts": "3.2.0"
  },
  "devDependencies": {
    "@types/react": "16.9.11",
    "@types/react-dom": "16.9.3",
    "typescript": "3.6.4"
  }
}
```

One thing. Below is the final structure of the meme generator you are going to build. You can use this to help yourself orient in the code.

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
│ │ ├─content.tsx
│ │ ├─form.tsx
│ │ └─result.tsx
│ ├─styles
│ │ └─styles.css
│ ├─index.tsx
│ └─react-app-env.d.ts
├─ package.json
└─ tsconfig.json
```

## Form component

The first component you will build will be a form. To be specific, it will actually be a `div` with couple of `input` elements and buttons. There will be two inputs, one for text at the top and one for the text on the bottom. Next, there four buttons, one for generating real png image of the meme.

Second button will change the image, load random image provided by `api.imgflip.com`. Third button will allow you to upload your own image from your disk. This will button will actually be `file` input wrapped inside `label` element. The fourth button will reset the image, i.e. remove the generated meme from DOM.

About the "Reset" button. The meme generator will display this button only when some meme image is generated. Otherwise, this button component will not exist in the DOM.

```
// Import react
import * as React from 'react'

// Interface for Form Component
interface FormInterface {
  isMemeGenerated: boolean;
  textBottom: string;
  textTop: string;
  handleImageChange: () => void;
  handleImageInputChange: (event: React.ChangeEvent) => void;
  handleInputChange: (event: React.ChangeEvent) => void;
  handleMemeGeneration: () => void;
  handleMemeReset: () => void;
}

// Form component
const Form = (props: FormInterface) => {
  return (
    <div className="form">
      <div className="form__inputs">
        {/* Input for the text at the top */}
        <input
          name="text-top"
          placeholder="Text top"
          type="text"
          value={props.textTop}
          onChange={props.handleInputChange}
        />

        {/* Input for the text at the bottom */}
        <input
          name="text-bottom"
          placeholder="Text bottom"
          type="text"
          value={props.textBottom}
          onChange={props.handleInputChange}
        />
      </div>

      <div className="form__btns">
        {/* Button to load random image from api.imgflip.com */}
        <button
          className="btn btn-primary"
          type="button"
          onClick={props.handleImageChange}
        >
          Change image
        </button>

        {/* 'Button' to load image from disk */}
        <label
          className="btn btn-primary"
          htmlFor="fileInput"
        >
          Load image
          <input id="fileInput" name="fileInput" type="file" accept=".jpg, .jpeg, .png" onChange={props.handleImageInputChange} hidden />
        </label>

        {/* Button to generate png image of the meme */}
        <button
          className="btn btn-primary"
          type="button"
          onClick={props.handleMemeGeneration}
        >
          Generate meme
        </button>

        {/* Button to remove the meme image from the DOM */}
        {props.isMemeGenerated && <button
          className="btn btn-danger"
          type="button"
          onClick={props.handleMemeReset}
        >
          Reset
        </button>}
      </div>
    </div>
  )
}

export default Form
```

## Content component

The `Content` component will be very simple. There will be one wrapper `div` with `img` element to preview the meme image, and `h1` for the text at the top and `h2` for the text at the bottom. The wrapper `div` will have a `ref`.

You will use this ref later to make it easier to reference this `div`, and generate the meme from its HTML content. That's it for the `Content` component.

```
// Import react
import * as React from 'react'

// Interface for Content component
interface ContentInterface {
  activeImage: string;
  contentContainerRef: React.RefObject<any>;
  textBottom: string;
  textTop: string;
}

// Content component
const Content = (props: ContentInterface) => {
  return (
    <div className="content" ref={props.contentContainerRef}>
      {/* Image preview */}
      <img src={props.activeImage} alt="Meme" />

      {/* Text at the top */}
      <h1>{props.textTop}</h1>

      {/* Text at the bottom */}
      <h2>{props.textBottom}</h2>
    </div>
  )
}

export default Content
```

## Result component

The third component you will build will be the `Result` component. This component will be a `div` that will wrap the png or jpeg image, this meme generator will create. The wrapper `div` will also have a `ref`. You will use this `ref` to append the newly generated meme image, and also to remove any existing when you click the "Reset" button.

```
// Import react
import * as React from 'react'

// Interface for Result component
interface ResultInterface {
  resultContainerRef: React.RefObject<any>;
}

// Result component
const Result = (props: ResultInterface) => {
  return (
    <div ref={props.resultContainerRef} className="result"></div>
  )
}

export default Result
```

## Main (index) component

It is time for the fourth and most important and complex component. This component will render all smaller components you've built so far. It will also provide them with logic and functionality. So, when you finish this component your meme generator be ready to use. Well, almost. It will need some styles. But now, the main component.

### Imports

As the first thing, you will need to import `react`, `react-dom` and  `dom-to-image-more` packages. Next, you will also need to import all components you've built so far, i.e. `Content`, `Form` and `Result`. Then, you can add import for CSS stylesheet so you can later add some CSS styles to style your meme generator.

### Refs and states

At the top of the main `App` component, you will create refs for the content and result `div` elements, `contentContainerRef` and `resultContainerRef`, using `useRef` React hook. Next, you will add states for images fetched from API, active image, top and bottom texts and for boolean isMemeGenerated. All with React `useState` React hook.

```
function App() {
  // Create refs
  let contentContainerRef = React.useRef<HTMLElement | null>(null)
  let resultContainerRef = React.useRef<HTMLElement | null>(null)

  // Create useState hooks
  const [images, setImages] = React.useState([])
  const [activeImage, setActiveImage] = React.useState('')
  const [textTop, setTextTop] = React.useState('')
  const [textBottom, setTextBottom] = React.useState('')
  const [isMemeGenerated, setIsMemeGenerated] = React.useState(false)

  // ...
}
```

### Fetching the API

Then will come the first method, fetchImage. This method will be async. It will use `fetch` method to fetch the data from `api.imgflip.com` endpoint. The result will be an array of images with some additional information. You will store this array in `images` state using the `setImages` React hook.

After that you will take the first image in the array and set it as active image, i.e. store it in `activeImage` state, using the `setActiveImage`.

```
  // ...
  // Fetch images from https://api.imgflip.com/get_memes
  async function fetchImage() {
    // Get the memes
    const imgData = await fetch('https://api.imgflip.com/get_memes').then(res => res.json()).catch(err => console.error(err))
    const { memes } = await imgData.data

    // Update images state
    await setImages(memes)

    // Update activeImage state
    await setActiveImage(memes[0].url)
  }
  // ...
```

### Handling the text inputs

Second method will be `handleInputChange`. You will use this method to handle inputs for meme image texts, the top and bottom. You will use `event.target.name` and `if` statement to detect which text is firing the event. Then, you will change the `textTop`, or `textBottom`, state using the `setTextTop`, or `setTextBottom`, React hook.

You will use `event.target.value` to extract the text from the input, and pass it to the state.

```
  // ...
  // Handle input elements
  function handleInputChange(event) {
    if (event.target.name === 'text-top') {
      // Update textTop state
      setTextTop(event.target.value)
    } else {
      // Update textBottom state
      setTextBottom(event.target.value)
    }
  }
  // ...
```

### Handling the image change

The third method will be `handleImageChange`. This method will be initiated by clicking on the "Reset" button. It will take the array of images stored in `images` state, generate random number, and use that number as an index to choose one random image from the array.

```
  // ...
  // Choose random images from images fetched from api.imgflip.com
  function handleImageChange() {
    // Choose random image
    const image = images[Math.floor(Math.random() * images.length)]

    // Update activeImage state
    setActiveImage(image.url)
  }
  // ...
```

### Handling the file input

The fourth method will be `handleImageInputChange`. This method will load the file loaded via the file input and use the `setActiveImage` React hook to change the `activeImage` state to the URL created for the image file you've uploaded from your disk.

```
  // ...
  // Handle image upload via file input
  function handleImageInputChange(event) {
    // Update activeImage state
    setActiveImage(window.URL.createObjectURL(event.target.files[0]))
  }
  // ...
```

### Generating the meme image

The fifth method will be `handleMemeGeneration`. First, you will create a condition to check for any `childNodes` inside the result container. If there is child node, this method will remove it. Otherwise, it will proceed to generating the meme image. This will make it sure there is always only one rendered image.

The generator will generate the image in png format, using the `domtoimage` package and its `toPng` method. You can also use jpg (with `toJpeg`) or svg (with `toSvg`) formats. Next, you will pass the `contentContainerRef.current` as argument to the `toPng` method, to find the content container where you want to render the meme image.

After that, you will create new image element, use URL of the generated image as `src` and append this new image to DOM, using the `resultContainerRef`. When this is done, you will change `isMemeGenerated` state to `true` using the `setIsMemeGenerated` React hook. This will tell React to display the "Reset" button.

```
  // ...
  // Handle meme generation
  function handleMemeGeneration() {
    // Remove any existing images
    if (resultContainerRef.current.childNodes.length > 0) {
      resultContainerRef.current.removeChild(resultContainerRef.current.childNodes[0])
    }

    // Generate meme image from the content of 'content' div
    domtoimage.toPng(contentContainerRef.current).then((dataUrl) => {
      // Create new image
      const img = new Image()

      // Use url of the generated image as src
      img.src = dataUrl

      // Append new image to DOM
      resultContainerRef.current.appendChild(img)

      // Update state for isMemeGenerated
      setIsMemeGenerated(true)
    })
  }
  // ...
```

### Handling the "Reset" button

The sixth method you will create is `handleMemeReset`. This method will remove existing child node inside result container, generated meme image. Then, it will set the `isMemeGenerated` state to `false` using the `setIsMemeGenerated` React hook. This will tell React to remove the "Reset" button.

```
  // ...
  // Handle resetting the meme generator/removing existing pictures
  function handleMemeReset() {
    // Remove existing child node inside result container (generated meme image)
    resultContainerRef.current.removeChild(resultContainerRef.current.childNodes[0])

    // Update state for isMemeGenerated
    setIsMemeGenerated(false)
  }
  // ...
```

### Combining fetchImage with useEffect

Almost the last step. You will combine `useEffect` React hook with `fetchImage` method. This will cause that when the app mounts it will automatically fetch images from the API and set the first one as active. And, you will render the `App` component in the DOM.

```
  // ...
  // Fetch images from https://api.imgflip.com/get_memes when app mounts
  React.useEffect(() => {
    // Call fetchImage method
    fetchImage()
  }, [])
  // ...
```

### Returning all components

The last step. Now, you will take all the components you've built, and imported, and add them to the main `App` component.

```
  // ...
  return (
    <div className="App">
      {/* Add Form component */}
      <Form
        textTop={textTop}
        textBottom={textBottom}
        handleImageInputChange={handleImageInputChange}
        handleInputChange={handleInputChange}
        handleImageChange={handleImageChange}
        handleMemeGeneration={handleMemeGeneration}
        handleMemeReset={handleMemeReset}
        isMemeGenerated={isMemeGenerated}
      />

      {/* Add Content component */}
      <Content
        activeImage={activeImage}
        contentContainerRef={contentContainerRef}
        textBottom={textBottom}
        textTop={textTop}
      />

      {/* Add Result component */}
      <Result resultContainerRef={resultContainerRef} />
    </div>
  )
}

// Render the App in the DOM
const rootElement = document.getElementById('root')
render(<App />, rootElement)
```

## Putting it all together

Now, let's put all the pieces for the `App` component together.

```
// Import react, react-dom & dom-to-image-more
import * as React from 'react'
import { render } from 'react-dom'
import domtoimage from 'dom-to-image-more'

// Import components
import Content from './components/content'
import Form from './components/form'
import Result from './components/result'

// Import styles
import './styles/styles.css'

// App component
function App() {
  // Create refs
  let contentContainerRef = React.useRef<HTMLElement | null>(null)
  let resultContainerRef = React.useRef<HTMLElement | null>(null)

  // Create useState hooks
  const [images, setImages] = React.useState([])
  const [activeImage, setActiveImage] = React.useState('')
  const [textTop, setTextTop] = React.useState('')
  const [textBottom, setTextBottom] = React.useState('')
  const [isMemeGenerated, setIsMemeGenerated] = React.useState(false)

  // Fetch images from https://api.imgflip.com/get_memes
  async function fetchImage() {
    // Get the memes
    const imgData = await fetch('https://api.imgflip.com/get_memes').then(res => res.json()).catch(err => console.error(err))
    const { memes } = await imgData.data

    // Update images state
    await setImages(memes)

    // Update activeImage state
    await setActiveImage(memes[0].url)
  }

  // Handle input elements
  function handleInputChange(event) {
    if (event.target.name === 'text-top') {
      // Update textTop state
      setTextTop(event.target.value)
    } else {
      // Update textBottom state
      setTextBottom(event.target.value)
    }
  }

  // Choose random images from images fetched from api.imgflip.com
  function handleImageChange() {
    // Choose random image
    const image = images[Math.floor(Math.random() * images.length)]

    // Update activeImage state
    setActiveImage(image.url)
  }

  // Handle image upload via file input
  function handleImageInputChange(event) {
    // Update activeImage state
    setActiveImage(window.URL.createObjectURL(event.target.files[0]))
  }

  // Handle meme generation
  function handleMemeGeneration() {
    // Remove any existing images
    if (resultContainerRef.current.childNodes.length > 0) {
      resultContainerRef.current.removeChild(resultContainerRef.current.childNodes[0])
    }

    // Generate meme image from the content of 'content' div
    domtoimage.toPng(contentContainerRef.current).then((dataUrl) => {
      // Create new image
      const img = new Image()

      // Use url of the generated image as src
      img.src = dataUrl

      // Append new image to DOM
      resultContainerRef.current.appendChild(img)

      // Update state for isMemeGenerated
      setIsMemeGenerated(true)
    })
  }

  // Handle resetting the meme generator/removing existing pictures
  function handleMemeReset() {
    // Remove existing child node inside result container (generated meme image)
    resultContainerRef.current.removeChild(resultContainerRef.current.childNodes[0])

    // Update state for isMemeGenerated
    setIsMemeGenerated(false)
  }

  // Fetch images from https://api.imgflip.com/get_memes when app mounts
  React.useEffect(() => {
    // Call fetchImage method
    fetchImage()
  }, [])

  return (
    <div className="App">
      {/* Add Form component */}
      <Form
        textTop={textTop}
        textBottom={textBottom}
        handleImageInputChange={handleImageInputChange}
        handleInputChange={handleInputChange}
        handleImageChange={handleImageChange}
        handleMemeGeneration={handleMemeGeneration}
        handleMemeReset={handleMemeReset}
        isMemeGenerated={isMemeGenerated}
      />

      {/* Add Content component */}
      <Content
        activeImage={activeImage}
        contentContainerRef={contentContainerRef}
        textBottom={textBottom}
        textTop={textTop}
      />

      {/* Add Result component */}
      <Result resultContainerRef={resultContainerRef} />
    </div>
  )
}

// Render the App in the DOM
const rootElement = document.getElementById('root')
render(<App />, rootElement)
```

## Styles

Your meme generator is almost ready. The last thing you can do is adding some styles to make it look better.

```
/* Default styles */
html {
  box-sizing: border-box;
  font-size: 16px;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

body {
  margin: 0;
  font: 1rem sans-serif;
}

/* App */
.App {
  text-align: center;
}

/* Content */
.content {
  position: relative;
  display: flex;
  align-items: center;
  flex-flow: column;
  justify-content: center;
  margin-top: 16px;
}

img {
  max-width: 520px;
  height: auto;
  max-height: 500px;
  object-fit: contain;
}

h1,
h2 {
  position: absolute;
  margin: 0;
  width: 100%;
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  font-size: 48px;
  text-align: center;
  text-transform: uppercase;
  color: #fff;
  /* text-shadow: 0px 0px 2px black; */
  -webkit-text-stroke: 3px black;
  line-height: 1;
}

h1 {
  top: 16px;
}

h2 {
  bottom: 32px;
}

/* Form */
.form {
  margin: 0 auto;
  max-width: 380px;
}

.form__inputs,
.form__btns {
  display: flex;
  flex-flow: row nowrap;
}

.form__inputs {
  margin-bottom: 12px;
}

.form__inputs input,
.form__btns .btn  {
  border-radius: 2px;
}

.form__inputs input {
  padding: 8px;
  width: 100%;
  max-width: 50%;
  border: 1px solid #ccc;
}

.form__inputs input:focus {
  outline-color: #0984e3;
}

.form__inputs input + input,
.form__btns .btn + .btn {
  margin-left: 12px;
}

.form__btns {
  justify-content: center;
}

.form__btns .btn {
  padding: 8px 12px;
  border: 0;
  cursor: pointer;
  color: #fff;
  transition: background .25s ease-in-out;
}

/* Buttons */
.btn-primary {
  background: #0984e3;
}

.btn-primary:hover {
  background: #0767b2;
}

.btn-danger {
  background: #d63031;
}

.btn-danger:hover {
  background: #b02324;
}
```

## Conclusion: Build your own Meme Generator...

Good job! You've just built your own meme generator with React, React hooks and TypeScript. I hope you've enjoyed this tutorial and learned something new, something you can use in your future project. Next steps? Find a way to make this meme generator better. Add new features you would like it to have. Your imagination is the only limit. Have fun.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[GitHub]: https://github.com/alexdevero/react-meme-generator-ts
[create-react-app]: https://github.com/facebook/create-react-app
[pnpm]: https://pnpm.js.org/
[npm]: https://nodejs.org/en/
[yarn]: https://yarnpkg.com/lang/en/
[TypeScript]: https://www.typescriptlang.org/

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
-
-->
