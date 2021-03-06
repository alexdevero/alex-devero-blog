# Getting Started with Web Storage API - Local Storage and Session Storage

The local storage and session storage are two storage mechanisms of the Web Storage API. This API provides an easy way to store data in the browser. This tutorial will help you learn what local storage and session storage are and how to use them. You will also learn when to use which.

<!--more-->
<!--
Table of Contents:
## A quick introduction
## The local storage and the session storage
### The local storage
### The session storage
## Web Storage API methods
### The setItem() method
### An alternative to the setItem() method
### The getItem() method
### An alternative to the getItem() method
### The removeItem() method
### An alternative to the removeItem() method
### The clear() method
### The key() method
## The length property
## Looping over web storage
## Conclusion: Getting Started with Web Storage API - Local Storage and Session Storage
-->

## A quick introduction

There are multiple ways to store data in the browser. You can store data using [IndexedDB], [Cache] and cookies. Aside to these, there is also the Web Storage API. This API provides two additional mechanisms you can use to store data in the browser. These mechanisms are local storage and session storage.

One benefit of this additional Web Storage API is that it makes it easier to store data in the browser. Yes, you can store some simple data with cookies. However, even that can be tedious. This can't be said about Web Storage API. With the Web Storage API, saving, retrieving, deleting and also checking for existence of data is simple and easy.

Another benefit of Web Storage API is that all data store are private. When you store some data either in local storage or in session other websites can't access them. This applies also if you open a page over HTTP protocol and then over HTTPS protocol. The later will not be able to access data stored over HTTP.

These privacy restrictions also apply to severs. Web Storage is available only in the browser. You access it via the `window` object. This object doesn't exist on the server. So, you don't have to worry about your storage data being send to the server, like cookies often are.

## The local storage and the session storage

The Web Storage API offers two types of storage. The first one is local storage. The second is session storage. Both these storage types work with the same methods and store, and retrieve, the data in the same format. Where these storage types differ is how long they store the data.

### The local storage

When you store some data in local storage these data will persist even when you close the browser. If you open the browser again, you will be able to retrieve the data you stored previously. There is also no expiration date. So, even if you give it a few days, or weeks, your data will persist.

The only way to delete data in local storage is by deleting them explicitly. You can do this in two ways. First, you can delete the data with JavaScript. The process similar to storing the data. The only difference is that you will use a different method.

The second way to remove data stored in local storage is by cleaning Browser cache and especially the Locally Stored Data. The amount of data you can store in a local storage will differ based on the device and browser you use. The average is usually somewhere around 5MB. This is still more than you can store in a cookie.

### The session storage

What about the session storage? When you store data in session storage these data will be available only for that page session. When you close the tab, or the browser, data in session storage are gone. If you open multiple browser windows, or tabs, with the same site all windows and tabs will use different session storage.

Similarly to local storage, the data you store in session storage are never send to the server. They are always kept in the browser. Unlike the local storage, session storage can handle more data. According to [some sources], session storage is limited only by only by system memory, at least in some browsers.

## Web Storage API methods

The Web Storage API provides couple of methods to store, retrieve and remove data in web storage. The nice thing is that all these methods work with local storage and also with session storage. When you want to use these methods, make sure to use the correct storage you want. Let's take a look at these methods and how to use them.

### The setItem() method

The setItem() method is what you need when you want to store data, either in local storage or in sessions storage. This method accepts two parameters. The first parameter is the `key`. The second parameter is the `value`. As you may guess, the storage is created as an object.

This is one reason why working with Web Storage API is easier than working with cookies. With Web Storage API, you can work with the data as you would with [objects]. You save data in the form of a key/value pairs. Then, you retrieve any stored data also by using specific key. This will give you the value assigned to this key.

```JavaScript
// Storing data in local storage with setItem() method
localStorage.setItem('name', 'Alex')

localStorage.name
// Output:
// "Alex"


// Storing data in session storage with setItem() method
sessionStorage.setItem('name', 'Tom')

sessionStorage.name
// Output:
// "Tom"
```

There are two things to remember when you want to store data in storage. First, the value you pass to `setItem()` method as a `key` and `value` must be strings. If you pass something else, it will be automatically converted to a string. This is important if you want to check for the type of value. That value will always be a string.

This is especially important if you want to store complex data such as objects or arrays. In that case, one thing you can do is to use `JSON.stringify()`. This will convert the object, or an array, into a string and store it in this format in web storage.

Later, when you will want to retrieve the data, you can use `JSON.parse()`. This will convert the string back to the original format, such as an object or an array.

```JavaScript
// Storing data in local storage with setItem() method
localStorage.setItem('age', '35')

localStorage.age
// Output:
// "35"

typeof localStorage.age
// Output:
// "string"

// Storing data in session storage with setItem() method
sessionStorage.setItem('isAlive', true)

sessionStorage.isAlive
// Output:
// "true"

typeof localStorage.isAlive
// Output:
// "string"


// Storing objects in web storage using JSON.stringify()
sessionStorage.setItem('name', JSON.stringify({ status: 'living'}))

sessionStorage.name
// Output:
// "{"status":"living"}"

// Retrieving objects from web storage using JSON.parse()
JSON.parse(sessionStorage.name)
// Output:
// {status: "living"}
```

The second thing is that there is no "updateItem" method. When you want to update some value the process is simple. You just have to use the same key. When you use the same key, new value will automatically overwrite the old one. This can be a good thing as well as a bad thing.

It can be a good thing because it makes it easier to work with Web Storage API. You don't have to remember another method. It can also be a bad thing because it makes it easier to accidentally overwrite your data. Way to avoid this is by paying attention to the keys you use. Make sure you are using unique, or make sure you really want to overwrite the data.

```JavaScript
// Overwriting data in local storage with setItem() method
localStorage.setItem('name', 'Jack')
localStorage.setItem('name', 'Andrei')

localStorage.name
// Output:
// "Andrei"


// Overwriting data in session storage with setItem() method
sessionStorage.setItem('name', 'Sandra')
sessionStorage.setItem('name', 'Victoria')

sessionStorage.name
// Output:
// "Victoria"
```

### An alternative to the setItem() method

There is one thing you may have noticed on the previous examples. We were able to access data in web storage by using object dot notation. You can use the object dot notation not only to access data in a web storage but also to store them there. The syntax is similar to accessing.

The difference is that when you want to store some data in a key, an assignment has to follow the dot notation. You have to add equal sign and some expression you want to store, like `localStorage.newKey = 'some value'` or `sessionStorage.newKey = 'some value'`. This way, you can store data just as easily as with `setItem()` method.

```JavaScript
// Adding data to local storage with dot notation
localStorage.book = 'Zero to One'

localStorage.book
// Output:
// "Zero to One"

// Adding data to session storage with dot notation
sessionStorage.book = 'Hard Things About Hard Things'

sessionStorage.book
// Output:
// "Hard Things About Hard Things"
```

### The getItem() method

So far, we retrieved and accessed the values in web storage by using specific key and object dot notation. This is one way to do this. You can do this also by using the `getItem()` method. This method is created for this purpose, of retrieving data from web storage. It accepts a single parameter, the `value`.

When you pass in some key that doesn't exist `getItem()` method will return `null`. Otherwise, it will return the value assigned to that key. This also makes `getItem()` method useful for testing if some specific key exists in a storage before you try to retrieve it. Or, if you want to avoid rewriting existing values.

This works because `null` is a one of the [eight] values that is considered falsy in JavaScript. This means that you can use `getItem()` method in a conditional statement to check if key exists before you try to access it or create it, or update it.

```JavaScript
// Retrieving and accessing data in local storage with getItem() method
// Store some data in local storage
localStorage.setItem('favoriteLanguage', 'JavaScript')

// Check if "favoriteLanguage" key exists
if (localStorage.getItem('favoriteLanguage')) {
  // Retrieve value of "favoriteLanguage"
  localStorage.getItem('favoriteLanguage')
}
// Output:
// "JavaScript"


// Retrieving and accessing data in session storage with getItem() method
sessionStorage.setItem('favoriteLanguage', 'Assembly')

// Check if "favoriteLanguage" key exists
if (localStorage.getItem('favoriteLanguage')) {
  // Retrieve value of "favoriteLanguage"
  localStorage.getItem('favoriteLanguage')
}
// Output:
// "Assembly"
```

### An alternative to the getItem() method

Similarly to the storing data in web storage, you can also use object dot notation to retrieve data from it. This is what we have already done in previous examples. You can also use the dot notation to check if specific key exists in web storage. It works in the same way as with the `getItem()` method.

When object, such as the web storage, doesn't have specific key it will return `null` if you ask for that key. Otherwise, you will get the value assigned to that key.

```JavaScript
// Retrieving and accessing data in local storage using dot notation
// Store some data in local storage
localStorage.setItem('favoriteColor', 'black')

// Check if "favoriteColor" key exists
if (localStorage.favoriteColor) {
  // Retrieve value of "favoriteColor"
  localStorage.favoriteColor
}
// Output:
// "black"


// Retrieving and accessing data in session storage using dot notation
// Store some data in session storage
sessionStorage.setItem('favoriteColor', 'red')

// Check if "favoriteColor" key exists
if (sessionStorage.favoriteColor) {
  // Retrieve value of "favoriteColor"
  sessionStorage.favoriteColor
}
// Output:
// "red"
```

### The removeItem() method

When you want to delete a single key/value pair from web storage the `removeItem()` is your go-to method. This method takes a single parameter, the name of the key you want to remove. When you use this method it will always return `undefined`, no matter if the key actually existed and was removed or if it didn't exist at all.

```JavaScript
// Removing data from local storage with removeItem() method
// Store some data in local storage
localStorage.setItem('username', 'jackblack')

// Check if "username" key exists
if (localStorage.getItem('username')) {
  // Retrieve value of "username"
  localStorage.getItem('username')
}
// Output:
// "jackblack"

// Remove "username" from local storage
localStorage.removeItem('username')

// Check if "username" key exists
if (localStorage.getItem('username')) {
  // Retrieve value of "username"
  localStorage.getItem('username')
}
// Output:
// undefined


// Removing data from session storage with removeItem() method
// Store some data in session storage
sessionStorage.setItem('username', 'skyhigh')

// Check if "username" key exists
if (sessionStorage.getItem('username')) {
  // Retrieve value of "username"
  sessionStorage.getItem('username')
}
// Output:
// "skyhigh"

// Remove "username" from session storage
sessionStorage.removeItem('username')

// Check if "username" key exists
if (sessionStorage.getItem('username')) {
  // Retrieve value of "username"
  sessionStorage.getItem('username')
}
// Output:
// undefined
```

### An alternative to the removeItem() method

When you work with JavaScript objects, there is a quick way to delete their properties. You can o that with the help of `delete` operator. You can use this operator also to delete property from a web storage. The syntax is the same. There is the `delete` operator, storage type and property to delete, in a dot notation.

```JavaScript
// Removing data from local storage with delete operator
// Store some data in local storage
localStorage.setItem('season', 'summer')

// Check if "season" key exists
if (localStorage.getItem('season')) {
  // Retrieve value of "season"
  localStorage.getItem('season')
}
// Output:
// "summer"

// Remove "season" from local storage
delete localStorage.season

// Check if "season" key exists
if (localStorage.getItem('season')) {
  // Retrieve value of "season"
  localStorage.getItem('season')
}
// Output:
// undefined


// Removing data from session storage with delete operator
// Store some data in session storage
sessionStorage.setItem('season', 'spring')

// Check if "season" key exists
if (sessionStorage.getItem('season')) {
  // Retrieve value of "season"
  sessionStorage.getItem('season')
}
// Output:
// "spring"

// Remove "season" from session storage
delete sessionStorage.season

// Check if "season" key exists
if (sessionStorage.getItem('season')) {
  // Retrieve value of "season"
  sessionStorage.getItem('season')
}
// Output:
// undefined
```

### The clear() method

The `removeItem()` method will suffice when you want to remove some data from web storage. When you want to remove all data a better choice will be `clear()` method. This method is as simple as it can be. It doesn't accept any parameter. You just use it as it is and will remove everything in the storage you work with.

```JavaScript
// Removing data from local storage with clear() metod
// Store some data in local storage
localStorage.setItem('firstName', 'Mark')
localStorage.setItem('lastName', 'Zuck')

// Check the amount of items in stored in local storage
localStorage.length
// Output:
// 2

// Remove all data from local storage
localStorage.clear()

// Check the amount of items in stored in local storage again
localStorage.length
// Output:
// 0


// Removing data from session storage with clear() metod
// Store some data in session storage
sessionStorage.setItem('brand', 'Tesla')
sessionStorage.setItem('model', 'X')

// Check the amount of items in stored in session storage
sessionStorage.length
// Output:
// 2

// Remove all data from session storage
sessionStorage.clear()

// Check the amount of items in stored in session storage again
sessionStorage.length
// Output:
// 0
```

### The key() method

The `key()` method provides a simple and quick way to retrieve an item from web storage based on its index number. When you want to use this method you pass the index number as the only argument. As a result, you will get the key of the item, the name of the key from the key/value pair.

If you try to get a value of an item that doesn't exist the `key()` method will return `null`.

```JavaScript
// Retrieving data from local storage with key() metod
// Store some data in local storage
localStorage.name = 'Stan'
localStorage.email = 'stan@stan.com'
localStorage.gender = 'male'

// Retrieve the second item from local storage with key() metod
localStorage.key(1)
// Output:
// "name"


// Retrieving data from session storage with key() metod
// Store some data in session storage
sessionStorage.name = 'Stan'
sessionStorage.email = 'stan@stan.com'
sessionStorage.gender = 'male'

// Retrieve the second item from session storage with key() metod
sessionStorage.key(1)
// Output:
// "name"
```

You may have noticed something weird in the example above. That key we got for index "1" was "name". Shouldn't we get "email" instead? This is the problem with `key()` method. The items are not ordered in the order you created them. They are not even ordered alphabetically.

If that was the case, index "1" would return "gender" instead of "name". The actual order of items is hard to say because it is defined by the user-agent, the browser you are using. Switch browser and you may get different results. So, don't rely too much on the `key()` method as it can be quite unpredictable.

## The length property

When you want to quickly check if storage contains any data one thing you can use `length`. This can be especially handy if you don't know the name of items' keys. From the get-go, the value of `length` property is always 0. This means that storage doesn't contain any data. This number will increase with the items you add.

```JavaScript
// Checking if local storage contains data with length property
localStorage.length
// Output:
// 0

// Add some data to local storage
localStorage.day = 'Monday'
localStorage.month = 'January'

// Check if local storage contains data again
localStorage.length
// Output:
// 2


// Checking if session storage contains data with length property
sessionStorage.length
// Output:
// 0

// Add some data to session storage
sessionStorage.currentlyReading = 'JavaScript: The Definitive Guide'
sessionStorage.onTheShelf = 'JavaScript: The Good Parts'

// Check if session storage contains data again
sessionStorage.length
// Output:
// 2
```

## Looping over web storage

You know that you can add, retrieve and also delete data from web storage in the same way as with objects. That is by using dot notation. Another thing you can do with web storage, just like with objects, is looping over them. You can do this using either [for loop] or [for...in loop].

There is one thing you need to know before you try to loop over a web storage. Looping will also retrieve built-in properties. These properties include the `length` property and also all the methods we discussed today. One way to avoid this by using `hasOwnProperty()` method.

This method returns `true` if some object contains specific property as its own property. It returns `false` for all properties that were inherited. This means all built-in properties that exist on the object prototype. With this method and conditional statement we can quickly check if specific property is built-in or not and return only those that are not.

```JavaScript
// Looping over web storage - getting all keys
// Add some data to local storage
localStorage.firstName = 'John'
localStorage.lastName = 'Doe'
localStorage.age = '47'

// First check if local storage contains any items
if (localStorage.length > 0) {
  // Then, use for...in loop to loop over all items in localStorage
  for (let key in localStorage) {
    // Check if each property is not built-in
    if (localStorage.hasOwnProperty(key)) {
      // Log only keys of properties that are not built-in
      console.log(key)
    }
  }
}

// Output:
// firstName
// lastName
// age


// Looping over web storage - getting all values
// Add some data to session storage
sessionStorage.firstName = 'John'
sessionStorage.lastName = 'Doe'
sessionStorage.age = '47'

// First check if session storage contains any items
if (sessionStorage.length > 0) {
  // Then, use for...in loop to loop over all items in sessionStorage
  for (let key in sessionStorage) {
    // Check if each property is not built-in
    if (sessionStorage.hasOwnProperty(key)) {
      // Log only values of properties that are not built-in
      console.log(sessionStorage[key])
    }
  }
}

// Output:
// 'John'
// 'Doe'
// '47'
```

## Conclusion: Getting Started with Web Storage API - Local Storage and Session Storage

The Web Storage API with its local storage and session storage mechanisms provides a nice and comfortable way to store data in the browser. In a recap, you've learned what local and session storage mechanisms are. Next, you've learned what are the main differences between those two.

After that, you've also learned about the default Web Storage API methods, what each does and how to use it. Lastly, you've learned how to use for and for...in loops to loop over web storage. I hope you enjoyed this tutorial and learned something that will help you become a better JavaScript developer.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[IndexedDB]: https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API
[Cache]: https://developer.mozilla.org/en-US/docs/Web/API/Cache
[some sources]: http://www.gwtproject.org/doc/latest/DevGuideHtml5Storage.html
[objects]: https://blog.alexdevero.com/javascript-objects-pt1/
[eight]: https://developer.mozilla.org/en-US/docs/Glossary/Falsy
[for loop]: https://blog.alexdevero.com/javascript-loops/#for-loop
[for...in loop]: https://blog.alexdevero.com/javascript-loops/#for8230in-loop

<!--
### Meta:
-
-->

<!--
### Keywords:
- JavaScript local storage
- local storage
- JavaScript session storage
- session storage
-->

<!--
### Resources:
-
-->
