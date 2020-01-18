# Build a [Contact Form] with React, AJAX, PHP and reCaptcha

Your new website is almost ready. The only thing you need is a contact form. Then, you are on the right place! This tutorial will show you how to build contact form with React, AJAX and PHP. What's more, you will also learn how to implement reCaptcha and make your contact form secure. Now, let's get to the work so you can ship your new website.

<!--
Table of Contents:
## Add package.json and install dependencies
## Create indexes
## Build your contact page
## Add the PHP
## Epilogue: Build a Contact Form with React, AJAX, PHP and reCaptcha
-->

## Add package.json and install dependencies

On one hand, you may already have a project with contact page and need just the contact form. On the other, you may not. Assuming the later is true, let's start with creating a minimal `package.json`. And, to keep things simple, let's add only necessary dependencies. These dependencies are `jquery`, `react`, `react-dom`, `react-recaptcha` and `react-scripts`.

The `react`, `react-dom` don't need any explanation. `react-recaptcha` is a React library for Google reCaptcha. You will use it in your form to make sure people, and robots especially, will not spam you. Or, at least to reduce the amount of spam messages. `react-scripts` will provide you with scripts to run, build, test and eject this project.

Finally, `jquery` will make it easier to handle the AJAX XMLHttpRequest. You will use it to submit the form. If you stick only with this, the final `package.json` will probably look like the example below. However, you can use any configuration and add anything you want. This is your contact form, or page. When you are done, install all dependencies with `npm i` or `yarn`.

```
// contact-form/package.json

{
  "name": "contact-form",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "jquery": "^3.3.1",
    "react": "^16.6.3",
    "react-dom": "^16.6.3",
    "react-recaptcha": "^2.3.10",
    "react-scripts": "2.1.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
```

## Create indexes

Next, if you don't have a contact page for the contact form, you will need to create `index.html` and `index.js`. The `index.html` will contain a container `div` for the contact form you will build with React. Below is an example of a simple `index.html`. Notice that you will need link to reCaptcha API script in `HEAD` section. This is necessary to make reCaptcha work. The dependency itself is not enough.

```
<!-- contact-form/public/index.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json">

    <title>Contact me</title>

    <!-- Load reCaptcha API -->
    <script src="https://www.google.com/recaptcha/api.js?onload=onloadCallback&render=explicit" async defer></script>
  </head>
  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>

    <!-- Container for React -->
    <div id="root"></div>
  </body>
</html>
```

In `index.js` you will import `React` and `ReactDOM` and also the contact page. After that, you will render the contact into HTML DOM, into the `div` container with `id` "root".

```
// contact-form/src/index.js

// Import React and ReactDOM
import React from 'react'
import ReactDOM from 'react-dom'

// Import contact page
import ContactPage from './contact-page'

// Render contact page in DOM
ReactDOM.render(<ContactPage />, document.getElementById('root'))
```

## Build your contact page

Now, when you have `index.html` and `index.js` ready, it is time to build the contact page. Or, at least to build the contact form. As usually, you will start with importing all necessary libraries. This means that you will need to import `jquery`, `react`, `react-dom`, `react-recaptcha`. And, you can also import stylesheet with some styles to make your contact form look better.

Then, you will create new React component called "ContactPage". This component will start with `state`. However, we will not use class `constructor`. This is not necessary. When it comes to `state`, you will use it as a place to store all the values provided by page visitors through all inputs in the contact form.

There will also be some additional `keys` that will help with validation of the contact form. After that, you will add a simple method to handle text inputs. It can be called "handleInput". You will use this method, along with `onChange` event, to find the correct `key` in contact page `state` and update its value.

You will do this by using the `name` attribute every input element in the contact form will have. Notice that this method will first test the length of the value and if the input is for email address. If it is email address, it will use regexp to validate the address provided by page visitors. Otherwise, it will skip this validation and just update the correct `key` in `state`.

Next, you will add another method to handle visitor's interaction with checkboxes. It will work in similar way as the one for input. It will use `name` attribute, check if checkbox is `checked` and update the `state`. Let's call this method "handleInput". Then, you will add another two small and simple methods for reCaptcha.

The first one, called "onCaptchaLoad", will be used by reCaptcha when the plugin is loaded. It can just log a message in console. The second one will be used when reCaptcha successfully validates the visitor. When this happens, it will update the value of `isCaptchaValid` key in `state`. Finally, you will create the method for submitting the contact form.

This method will assume that fields for name, email and message are required. In other words, it will check the length of values of `inputEmail`, `inputName` and `inputMessage` keys stored in `state`. It will also check the value of `isCaptchaValid` key, to make sure reCaptcha validated the visitor.

If any of these checks fails, it will set the value of `state` key `isErrorShown` to `true`. This will trigger render of error message below the contact form. Otherwise, it will proceed. Meaning, it will set the `isErrorShow` key in `state` to `false` to make sure no error message is visible. Then, it will set the value of `isFormValid` key to `true`.

After doing this maintenance, it will proceed to making the AJAX XMLHttpRequest with jQuery. This will be simple. it will send the content of `state` via `data` and set the `type` of the request to `POST`. Next, it will specify the name of the PHP file that will provide the API for your contact form. Then, it will add methods to log `success` and `error`.

When this is done, the `handleFormSubmit` will do the last thing to finish the work. It will reset all values stored in `state`. If you use `defaultValue` attribute on inputs, and set to correct keys in `state`, this will trigger resetting the contact form and clearing all inputs. Below is example of how the contact form may look like.

_Side note: Google reCaptcha plugin requires unique `sitekey` key in order to run. If you don't have this key, you can get it on [Google reCaptcha website]. Then, pass this key to `sitekey` attribute on `Recaptcha` component in your contact form. I marked this area in the code with `{/* !! */}` to make it more visible._

```
// contact-form/src/contact-page.js

// Import React and ReactDOM
import React, { Component } from 'react'

// Import jQuery
import $ from 'jquery'

// Import reCaptcha
import Recaptcha from 'react-recaptcha'

// Import some simple styles for contact form
import './styles/styles.css'

export default class ContactPage extends Component {
  state = {
    inputEmail: '',
    inputCheckBoth: false,
    inputCheckDesign: false,
    inputCheckDev: false,
    inputMessage: '',
    inputName: '',
    isCaptchaValid: false,
    isErrorShown: false,
    isFormValid: false
  }

  // Handle visitor's interaction with inputs
  handleInput = event => {
    // Test for input and length of the value
    if (event.target.value.length > 0 && event.target.name !== 'inputEmail') {
      this.setState({
        [event.target.name]: event.target.value
      })
    }

    // If input is for email address validate it with regexp
    if (event.target.name === 'inputEmail') {
      // eslint-disable-next-line
      const reg = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/

      if (reg.test(String(event.target.value).toLowerCase())) {
        this.setState({
          [event.target.name]: event.target.value
        })
      }
    }
  }

  // Handle visitor's interaction with checkboxes
  handleCheckbox = event => {
    this.setState({
      [event.target.name]: event.target.checked
    })
  }

  // Show message in console when reCaptcha plugin is loaded
  onCaptchaLoad = () => {
    console.log('Captcha loaded')
  }

  // Update state after reCaptcha validates visitor
  onCaptchaVerify = (response) => {
    this.setState({
      isCaptchaValid: true
    })
  }

  handleFormSubmit = event => {
    event.preventDefault()

    // Test
    if (this.state.inputEmail.length > 0 && this.state.inputName.length > 0 && this.state.inputMessage.length > 0 && this.state.isCaptchaValid) {
      this.setState({
        isErrorShown: false,
        isFormValid: true
      })

      // Send the form with AJAX
      $.ajax({
        data: this.state,
        type: 'POST',
        url: '/mailer.php',
        success: function(data) {
          console.info(data)
        },
        error: function(xhr, status, err) {
          console.error(status, err.toString())
        }
      })

      // Reset state after sending the form
      this.setState({
        inputEmail: '',
        inputCheckBoth: false,
        inputCheckDesign: false,
        inputCheckDev: false,
        inputMessage: '',
        inputName: '',
        isCaptchaValid: false,
        isErrorShown: false,
        isFormValid: false
      })
    } else {
      // Show error message
      this.setState({
        isErrorShown: true
      })
    }
  }

  render() {
    return (
      <div className="contact-page">
        <h1>Let's get in touch!</h1>

        <p>Feel free to get in touch with me. I am always open to discussing new projects, creative ideas or opportunities to be part of your visions.</p>

        <form action="">
          <fieldset>
            <label htmlFor="inputName">Name</label>

            <input onChange={this.handleInput} type="text" name="inputName" id="inputName" required={true} />
          </fieldset>

          <fieldset>
            <label htmlFor="inputEmail">Email</label>

            <input onChange={this.handleInput} type="email" name="inputEmail" id="inputEmail" required={true} />
          </fieldset>

          <div className="form__row">
            <div className="form__col">
              <fieldset>
                <label htmlFor="inputCheckDesign">
                  <input onClick={this.handleCheckbox} type="checkbox" name="inputCheckDesign" id="inputCheckDesign" defaultChecked={false} />

                  <span>Design</span>
                </label>
              </fieldset>
            </div>

            <div className="form__col">
              <fieldset>
                <label htmlFor="inputCheckDev">
                  <input onClick={this.handleCheckbox} type="checkbox" name="inputCheckDev" id="inputCheckDev" defaultChecked={false} />

                  <span>Development</span>
                </label>
              </fieldset>
            </div>

            <div className="form__col">
              <fieldset>
                <label htmlFor="inputCheckBoth">
                  <input onClick={this.handleCheckbox} type="checkbox" name="inputCheckBoth" id="inputCheckBoth" defaultChecked={false} />

                  <span>Design &amp development</span>
                </label>
              </fieldset>
            </div>
          </div>

          <fieldset>
            <label>message</label>

            <textarea onChange={this.handleInput} name="inputMessage" id="inputMessage" required={true} />
          </fieldset>

          {/* !! */}
          {/* Make sure to use your 'sitekey' for Google reCaptcha API! */}
          {/* !! */}
          <fieldset>
            <Recaptcha
              onloadCallback={this.onCaptchaLoad}
              sitekey="xxxxxxxxxxxxxxx"
              render="explicit"
              verifyCallback={this.onCaptchaVerify}
            />
          </fieldset>

          {this.state.isFormSubmitted && (
            <fieldset>
              <p>Thank you for contacting me. I will reply in four days.</p>
            </fieldset>
          )}

          {this.state.isErrorShown && (
            <fieldset>
              <p>Please, make sure to fill all fields.</p>
            </fieldset>
          )}

          <fieldset>
            <button onClick={this.handleFormSubmit} className="btn">
              Send
            </button>
          </fieldset>
        </form>
      </div>
    )
  }
}
```

## Add the PHP

You've just arrived to the final part. Now, you will write the PHP code and create API for your contact form so you can then send it. You may want to have the code for this contact form, and whole project, backed up in some repository. And, you may not want to tell everyone what your email address is. You can save your email in a file and then read it.

This is exactly the approach you will see in the PHP code for this contact form. First, you will save your email in some file. It doesn't have to be text file. It can be without any file extension. For example, it can be `.credentials`. Just make sure to include only your email address. No other text. Next, you will use `fopen()` function to open it and store it in `$credentialsFile` variable.

After that, you will use `fgets()` function on that `$credentialsFile` variable to read the first line and store the result in `$myEmail` variable. Next, you will extract data from the contact form you sent via AJAX. As you remember, you passed the whole `state` as the value for `data` in the AJAX request. And, you sent it as `POST`.

This means that all this data is now content of global `$_POST` variability. This variable is an associative array and you can access all data using specific name. This name are the same as the keys in `state`. In other words, `inputName`, `inputEmail`, `inputMessage`, `inputCheckBoth`, `inputCheckDesign`, `inputCheckDev` and so on.

You will use `trim` to remove any potential white space at the beginning or end of the input values. Next, you will once again check if name, email and message variables contain text. If not, the server will return 400 response code. Meaning, there is some problem. Otherwise, it will use the variables with contact form data, put together the content of the email, and send it.

When all this is done, server will return 200 response code. This means that the message as sent. Otherwise, if there is some issue, server will return either 500 or 403 error response code, which one depends on the type of the issue.

_Side note: You may hear about using `isset()` to check if checkboxes are checked. This is not necessary. In a fact, it would not work. As long as there are some checkboxes you would always get "1". Instead, you can just load the value just as you did with other inputs. The result will be the content of the state. You will get either `true` or `false`._

_It is up to you to decide whether to use these values in the email template. Otherwise, you can create some simple if statement with custom text when checkbox is checked (`true`) and when it is not (`false`)._

```
// contact-form/src/mailer.php

<?php
    // Only process POST requests.
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
      // Get email address from '.credentials' file in the root
      $credentialsFile = fopen(".credentials","r");
      $myEmail = fgets($credentialsFile);

      // Get the form fields and remove any potential whitespace.
      $name = strip_tags(trim($_POST["inputName"]));
      $name = str_replace(array("\r","\n"),array(" "," "),$name);
      $email = filter_var(trim($_POST["inputEmail"]), FILTER_SANITIZE_EMAIL);
      $message = trim($_POST["inputMessage"]);
      $checkBoth = trim($_POST["inputCheckBoth"]);
      $checkDesign = trim($_POST["inputCheckDesign"]);
      $checkDev = trim($_POST["inputCheckDev"]);

      // Check that data was sent to the mailer.
     if ( empty($name) OR empty($message) OR !filter_var($email, FILTER_VALIDATE_EMAIL)) {
        // Set a 400 (bad request) response code and exit.
        //http_response_code(400);
        echo "Oops! There was a problem with your submission. Please complete the form and try again.";
        exit;
      }

      // Set the recipient email address.
      $recipient = "$myEmail";

      // Print content of the state ($_POST array)
      // Don't use this on production!
      // $content = print_r($_POST);

      // Set the email subject.
      $subject = "New contact from $name";

      // Build the email content.
      $email_content = "Name: $name\n";
      $email_content .= "Email: $email\n\n";
      $email_content .= "Subject: New contact\n\n";
      $email_content .= "Message:\n$message\n\n";
      $email_content .= "Wants design: $checkDesign\n\n";
      $email_content .= "Wants dev: $checkDev\n\n";
      $email_content .= "Wants both: $checkBoth\n\n";

      // Build the email headers.
      $email_headers = "From: $name <$email>";

      // Send the email.
      if (mail($recipient, $subject, $email_content, $email_headers)) {
        // Set a 200 (okay) response code.
        //http_response_code(200);
        echo "Thank You! Your message has been sent.";
      } else {
        // Set a 500 (internal server error) response code.
        //http_response_code(500);
        echo "Oops! Something went wrong and we couldn\"t send your message.";
      }

    } else {
      // Not a POST request, set a 403 (forbidden) response code.
      //http_response_code(403);
      echo "There was a problem with your submission, please try again.";
    }
?>
```

## Epilogue: Build a Contact Form with React, AJAX, PHP and reCaptcha

Congratulations! You've just finished this short tutorial and created your own contact form. I hope you liked it and learn something new, something you can use. As you can see, you don't have to limit yourself to just one framework, technology or language. You can combine them as you want to get the job done. This is exactly what you did in this tutorial.

You created a contact form combining JavaScript in the form of React and AJAX with PHP. So, ignore those people saying that you have to choose one language or framework. The truth is that you don't have to. You can choose any languages and frameworks or their combination that you like. What matters is that it will get the job done.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[Google reCaptcha website]: http://www.google.com/recaptcha/admin
