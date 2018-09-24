# How to Build a Great Style Guide with React & styled-components Pt.3

When you work on a design project it is easy to lose track of how all elements should look like. This leads to inconsistent design and more work later. That is why having a style guide is so useful. Style guide helps us work fast while keeping the design consistent. Learn how to build your own style guide from scratch with `React` and `styled-components`.

<!--
Table of Contents:
## Adding Font Awesome
## Buttons
## Forms
## Epilogue: How to Build UI Style Guide with React Pt.3
-->

## Adding Font Awesome

Let's start with one very quick digression. The section of our style guide with buttons will contain button variant with icon. This gives us two options. First, we can use our own icon and implement it through `img` element or CSS `background` property. Second, we can use one of the available icon fonts hosted on CDN and implement it by adding its stylesheet.

If we would want to add just one icon, the first option a no-brainer. However, you may want to use another icons in other sections of this style guide. Let's prepare for this use case and choose the second option. The font we will use will be [Font Awesome]. This is a very popular icon font that offers very rich palette of good-looking icons we can use. We will add this stylesheet to `index.html` in `./public/`.

_Side note: Two things. First, there are two versions of Font Awesome icon font-version 4 and 5. Version 4 is completely for free and contains around 675 icons. Version 5 has two variants, free and Pro. Free version contains approximately 1 341 icons. Pro around 3 978 icons. Not all icons are unique. Some icons have multiple variants, filled, outlined, thicker, lighter, etc._

_The second thing is that you will probably find the CDN link for version 5 only on Font Awesome website. Other CDNs, such as [cdnjs], host only version 4, 4.7.0 to be more specific. So, if you want to use version 5, you don't have to look for CDNs. Instead, head on right to Font Awesome website and grab the CDN link from there._

```
<!-- public/index.html -->

<!DOCTYPE html>
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

    <title>UI Style Guide</title>

    <!-- Roboto typeface -->
    <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700" rel="stylesheet">

    <!-- Font Awesome stylesheet -->
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.3.1/css/all.css" integrity="sha384-mzrmE5qonljUremFsqc01SB46JvROS7bZs3IO2EmfFsd15uHvIt+Y8vEf7N7fWAU" crossorigin="anonymous">
  </head>

  ... rest of the code ...

</html>
```

## Buttons

The third section of our style guide will present styles dedicated to buttons. This, and also the following, section will contain two more or less generic component for rows. For buttons, it will be `ButtonsRow` and `ButtonVariant`. These generic components will help us place multiple variants of buttons next to each other on one row.

We will then be able to present different variants of buttons representing the same state, such as default, hover, active and disabled. The component for buttons, `Button`, will be relatively simple. We will add some basic styles and sometimes use `props` to switch between styles conditionally.

We will also use `props` to customize the buttons variants. For example, create large, medium, small, fab and ghost buttons and also buttons with simple icon provided by Font Awesome. Lastly, all states except "disabled" will present buttons in four color variants-blue (button primary), orange (button secondary), red (button error) and green (button success).

```
// ./components/buttons.jsx

// Import dependencies
import React from 'react'
import styled, { css } from 'styled-components'

// Import colors and sizes variables
import { colors, sizes } from './../variables'

// Import Container component
import { Container } from './generic-helpers'

// Import H5 heading
import { H5 } from './typography'

const ButtonsRow = styled.div`
  display: flex;
  flex-flow: row wrap;
  align-items: center;
  justify-content: flex-start;
  text-align: left;
  width: 100%;

  & + & {
    margin-top: 12px;
  }
`

const ButtonVariant = styled.div`
  width: 16.6666667%;

  &:nth-of-type(n+2) {
    text-align: center;
  }
`

const Button = styled.button`
  display: inline-block;
  width: ${props => (props.fab ? '32px' : 'initial')};
  font-size: ${sizes.sm};
  color: ${props => (props.ghost ? props.theme : '#fff')};
  background-color: ${props => (props.ghost ? 'transparent' : props.theme)};
  border: ${props => (props.ghost ? `1px solid ${props.theme}` : 0)};
  border-radius: ${props => (props.fab ? '50%' : '2px')};
  box-shadow: 0 3px 6px 0 rgba(0, 0, 0, 0.18), 0 4px 8px 0 rgba(0, 0, 0, 0.15);
  cursor: ${props => (props.disabled ? 'not-allowed' : 'pointer')};

  & + & {
    margin-top: 12px;
  }

  ${props =>
    props.active & !props.ghost &&
    css`
      background-color: ${colors.primaryActive};
  `};

  ${props =>
    props.active & props.ghost &&
    css`
      color: ${colors.primaryActive};
      border-color: ${colors.primaryActive};
  `};

  ${props =>
    props.hover & props.ghost &&
    css`
      color: ${colors.primaryHover};
      border-color: ${colors.primaryHover};
  `};

  ${props =>
    props.large | props.ghost &&
    css`
      padding: 14px 18px;
  `};

  ${props =>
    props.disabled & !props.ghost &&
    css`
      background-color: ${colors.disabled};
  `};

  ${props =>
    props.disabled & props.ghost &&
    css`
      color: ${colors.disabled};
      border-color: ${colors.disabled};
  `};

  ${props =>
    props.fab &&
    css`
      padding: 8px 16px;
      width: 40px;
      line-height: 24px;
  `};

  ${props =>
    props.medium &&
    css`
      padding: 10px 16px;
  `};

  ${props =>
    props.small &&
    css`
      padding: 6px 12px;
  `};

    ${props =>
      props.icon &&
      css`
      i {
        margin-right: 2px;
        font-size: 12px;
      }
  `};
`

const Buttons = () => {
  return (
    <Container>
      <H5>Default</H5>
      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.primary} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.secondary} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondary} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondary} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondary} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondary} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondary} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.error} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.error} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.error} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.error} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.error} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.error} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.success} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.success} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.success} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.success} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.success} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.success} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <H5>Hover</H5>
      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.primaryHover} large hover>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primaryHover} large hover icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primaryHover} ghost hover>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primaryHover} medium hover>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primaryHover} small hover>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primaryHover} fab hover>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.secondaryHover} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryHover} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryHover} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryHover} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryHover} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryHover} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.errorHover} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorHover} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorHover} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorHover} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorHover} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorHover} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.successHover} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successHover} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successHover} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successHover} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successHover} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successHover} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <H5>Active</H5>
      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.primary} large active>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} large active icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} ghost active>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} medium active>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} small active>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} fab active>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.secondaryActive} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryActive} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryActive} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryActive} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryActive} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.secondaryActive} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.errorActive} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorActive} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorActive} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorActive} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorActive} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.errorActive} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.successActive} large>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successActive} large icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successActive} ghost>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successActive} medium>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successActive} small>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.successActive} fab>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>

      <H5>Disabled</H5>
      <ButtonsRow>
        <ButtonVariant>
          <Button theme={colors.primary} large disabled>
            Large
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} large disabled icon>
            <i class="fas fa-bullhorn" /> with icon
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} ghost disabled>
            Ghost
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} medium disabled>
            Medium
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} small disabled>
            Small
          </Button>
        </ButtonVariant>

        <ButtonVariant>
          <Button theme={colors.primary} fab disabled>
            +
          </Button>
        </ButtonVariant>
      </ButtonsRow>
    </Container>
  )
}

export default Buttons
```

## Forms

Our style guide is almost complete. Forms is the last missing section. So, let's get right into it. As I mentioned in the previous section of our style guide, there will be two generic components, `FormsRow` and `InputElWrapper`. We will use these elements in the same way as in buttons section-to present form elements with the same state on the same line.

This section of our style guide will present four most common types of form elements-text input, textarea and checkbox and radio elements. Checkbox and radio elements will be custom-made. We will create our own design for these elements. Similar to buttons, we will present all these elements in four states-default, active, disabled and error.

Text input and textarea will use the same structure. We will create `InputLabel` for labels, `InputTextareaElement` for textarea element and `InputTextElement` for text input. We will wrap these elements with `InputElWrapper`. The structure of custom checkbox and radio elements will be one level more complex or deeper.

We will create three components-`InputOriginalElCustom` for the original checkbox/radio elements, `InputCheckboxElCustom` and `InputRadioElCustom` for our custom checkbox/radio elements and `InputLabelLabel` for labels, labels placed next to the checkbox/radio elements. These components will be wrapped inside `InputLabel` which will be wrapped by `InputElWrapper`.

```
// ./components/forms.jsx

import React from 'react'
import styled, { css } from 'styled-components'

// Import colors and sizes variables
import { colors, sizes } from './../variables'

// Import Container component
import { Container } from './generic-helpers'

// Import H5 heading
import { H5 } from './typography'

const FormsRow = styled.div`
  display: flex;
  flex-flow: row wrap;
  align-items: flex-start;
  justify-content: flex-start;
  text-align: left;
  width: 100%;

  & + & {
    margin-top: 12px;
  }
`

// Input label
const InputLabel = styled.label`
  margin-bottom: 8px;
  display: block;
  width: 100%;
  font-size: ${sizes.sm};
  white-space: pre;
`

// Text input
const InputTextElement = styled.input`
  padding-bottom: 6px;
  display: block;
  background: transparent;
  border-top: 0;
  border-right: 0;
  border-bottom: 1px solid ${colors.disabled};
  border-left: 0;
  outline: 0;
  transition: all .2s cubic-bezier(.4, 0, .2, 1) 0s;

  &:focus {
    outline: 0;
  }
`

// Textarea element
const TextareaElement = InputTextElement.withComponent('textarea') // candidate for deprecation

const InputTextareaElement = styled(TextareaElement)`
  min-height: 50px;
  resize: vertical;
`

// Checkbox input
const InputOriginalEl = styled.input`
  display: none;

  &:checked ~ div {
    background-color: ${colors.primary};
    border-color: ${colors.primary};

    &::after {
      transform: rotate(45deg) scale(1);
    }
  }
`

const InputOriginalElCustom = styled.div`
  position: absolute;
  top: 2px;
  left 4px;
  height: 20px;
  width: 20px;
  background: transparent;
  border: 2px solid hsla(0, 100%, 0%, .25);
  border-radius: 2px;
  transition: all .25s ease-in-out;

  &::after {
    position: absolute;
    content: '';
    left: 4px;
    top: 0;
    width: 8px;
    height: 12px;
    border: solid #fff;
    border-width: 0 2px 2px 0;
    transform: rotate(45deg) scale(0);
    transition: transform .25s ease-in-out;
  }
`

const InputLabelLabel = styled.span`
  margin-left: 22px;
`

// Radio input
const InputRadioElCustom = styled(InputOriginalElCustom)`
  &,
  &::after {
    border-radius: 50%;
  }

  &::after {
    left: 3px;
    top: 3px;
    width: 10px;
    height: 10px;
    background-color: #fff;
    transform: scale(1);
    transition: transform .25s ease-in-out;
  }
`

// General Input wrapper
const InputElWrapper = styled.fieldset`
  padding-top: 0;
  padding-bottom: 0;
  margin: 0;
  border: 0;

  &:first-of-type {
    padding-right: 8px;
    padding-left: 0;
  }

  &:nth-of-type(n+2) {
    padding-left: 8px;
    padding-right: 8px;
  }

  &:last-of-type {
    padding-right: 0;
    padding-left: 8px;
  }

  label,
  input:not(type=checkbox):not(type=radio),
  textarea {
    width: 100%;
  }

  ${props =>
    props.active &&
    css`
    label {
      color: ${colors.primary};
    }

    input,
    textarea {
      border-bottom-color: ${colors.primary};
    }

    ${InputOriginalElCustom} {
      background-color: ${colors.primary};
      border-color: ${colors.primary};

      &::after {
        transform: rotate(45deg) scale(1);
      }
    }

    ${InputRadioElCustom} {
      background-color: ${colors.primary};

      &::after {
        background-color: #fff;
      }
    }
  `}

  ${props =>
    props.disabled &&
    css`
    &,
    label,
    input,
    textarea {
      cursor: not-allowed;
    }

    label {
      color: hsl(212.3, 16.7%, 75%);
    }

    input,
    textarea,
    ${InputOriginalElCustom} {
      border-bottom-color: hsl(212.3, 16.7%, 75%);
    }

    ${InputRadioElCustom} {
      border-color: hsl(212.3, 16.7%, 75%);
    }
  `}

  ${props =>
    props.error &&
    css`
    label {
      color: ${colors.error};
    }

    input,
    textarea {
      border-bottom-color: ${colors.error};
    }

    ${InputOriginalElCustom} {
      background: transparent;
      border: 2px solid ${colors.error};
    }
  `}

  ${props =>
    props.custom &&
    css`
    position: relative;
  `}
`

const Form = () => {
  return (
    <Container>
      <H5>Default</H5>

      <FormsRow>
        <InputElWrapper>
          <InputLabel htmlFor="exampleInputOne">Example input</InputLabel>

          <InputTextElement
            id="exampleInputOne"
            name="exampleInputOne"
            type="text"
          />
        </InputElWrapper>

        <InputElWrapper>
          <InputLabel htmlFor="exampleInputTwo">Example textarea</InputLabel>

          <InputTextareaElement id="exampleInputTwo" name="exampleInputTwo" />
        </InputElWrapper>

        <InputElWrapper custom>
          <InputLabel htmlFor="checkboxOne">
            <InputOriginalEl
              id="checkboxOne"
              name="checkboxOne"
              type="checkbox"
            />

            <InputOriginalElCustom />

            <InputLabelLabel>Example checkbox</InputLabelLabel>
          </InputLabel>
        </InputElWrapper>

        <InputElWrapper custom>
          <InputLabel htmlFor="radioOne">
            <InputOriginalEl id="radioOne" name="radioOne" type="radio" />

            <InputRadioElCustom />

            <InputLabelLabel>Example radio</InputLabelLabel>
          </InputLabel>
        </InputElWrapper>
      </FormsRow>

      <H5>Active</H5>

      <FormsRow>
        <InputElWrapper active>
          <InputLabel htmlFor="exampleInputThree">Example input</InputLabel>

          <InputTextElement
            id="exampleInputThree"
            name="exampleInputThree"
            type="text"
          />
        </InputElWrapper>

        <InputElWrapper active>
          <InputLabel htmlFor="exampleInputFour">Example textarea</InputLabel>

          <InputTextareaElement id="exampleInputFour" name="exampleInputFour" />
        </InputElWrapper>

        <InputElWrapper custom active>
          <InputLabel htmlFor="checkbox">
            <InputOriginalEl
              id="checkboxTwo"
              name="checkboxTwo"
              type="checkbox"
            />

            <InputOriginalElCustom />

            <InputLabelLabel>Example checkbox</InputLabelLabel>
          </InputLabel>
        </InputElWrapper>

        <InputElWrapper custom active>
          <InputLabel htmlFor="radioTwo">
            <InputOriginalEl id="radioTwo" name="radioTwo" type="radio" />

            <InputRadioElCustom />

            <InputLabelLabel>Example radio</InputLabelLabel>
          </InputLabel>
        </InputElWrapper>
      </FormsRow>

      <H5>Disabled</H5>

      <FormsRow>
        <InputElWrapper disabled>
          <InputLabel htmlFor="exampleInputFive">Example input</InputLabel>

          <InputTextElement
            id="exampleInputFive"
            name="exampleInputFive"
            type="text"
          />
        </InputElWrapper>

        <InputElWrapper disabled>
          <InputLabel htmlFor="exampleInputSix">Example textarea</InputLabel>

          <InputTextareaElement id="exampleInputSix" name="exampleInputSix" />
        </InputElWrapper>

        <InputElWrapper custom disabled>
          <InputLabel htmlFor="checkboxThree">
            <InputOriginalEl
              id="checkboxThree"
              name="checkboxThree"
              type="checkbox"
              disabled={true}
            />

            <InputOriginalElCustom />

            <InputLabelLabel>Example checkbox</InputLabelLabel>
          </InputLabel>
        </InputElWrapper>

        <InputElWrapper custom disabled>
          <InputLabel htmlFor="radioThree">
            <InputOriginalEl id="radioThree" name="radioThree" type="radio" />

            <InputRadioElCustom />

            <InputLabelLabel>Example radio</InputLabelLabel>
          </InputLabel>
        </InputElWrapper>
      </FormsRow>

      <H5>Error</H5>

      <FormsRow>
        <InputElWrapper error>
          <InputLabel htmlFor="exampleInputSeven">Example input</InputLabel>

          <InputTextElement
            id="exampleInputSeven"
            name="exampleInputSeven"
            type="text"
          />
        </InputElWrapper>

        <InputElWrapper error>
          <InputLabel htmlFor="exampleInputEight">Example textarea</InputLabel>

          <InputTextareaElement
            id="exampleInputEight"
            name="exampleInputEight"
          />
        </InputElWrapper>

        <InputElWrapper custom error>
          <InputLabel htmlFor="checkboxFour">
            <InputOriginalEl
              id="checkboxFour"
              name="checkboxFour"
              type="checkbox"
              disabled={true}
            />

            <InputOriginalElCustom />

            <InputLabelLabel>Example checkbox</InputLabelLabel>
          </InputLabel>
        </InputElWrapper>

        <InputElWrapper custom error>
          <InputLabel htmlFor="radioFour">
            <InputOriginalEl
              id="radioFour"
              name="radioFour"
              type="radio"
              disabled
            />

            <InputRadioElCustom />

            <InputLabelLabel>Example radio</InputLabelLabel>
          </InputLabel>
        </InputElWrapper>
      </FormsRow>
    </Container>
  )
}

export default Form
```

## Epilogue: How to Build UI Style Guide with React Pt.3

We are at the end of the third and final part of this mini series about creating a style guide. What a ride. I hope you enjoyed this tutorial and had a chance to learn something new, work on your skills and get better at what you know. As the saying goes, mastery comes with practice. With that, I look forward to seeing you here again the next week. Until then, have a great day!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 1]: https://blog.alexdevero.com/style-guide-react-pt1/
[part 2]: https://blog.alexdevero.com/style-guide-react-pt2/
[Font Awesome]: https://fontawesome.com/?from=io
[cdnjs]: https://cdnjs.com
