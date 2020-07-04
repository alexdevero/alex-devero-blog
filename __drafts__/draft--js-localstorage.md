# Getting Started with Web Storage API - Local Storage and Session Storage

The local storage and session storage are two storage mechanisms of The Web Storage API. This API provides an easy way to store data in the browser. This tutorial will help you learn what local storage and session storage are and how to use them. You will also learn when to use which.

<!--more-->
<!--
Table of Contents:
-->

## A quick introduction

There are multiple ways methods to store data in the browser. You can store data using [IndexedDB], [Cache] and cookies. Aside to these, there is also the Web Storage API. This API provides two additional mechanisms you can use to store data in the browser. These mechanisms are local storage and session storage.

One benefit of this additional Web Storage API is that it makes it easier to store data in the browser. Yes, you can store some simple data with cookies. However, even that can be tedious. This can't be said about Web Storage API. With The Web Storage API, saving, retrieving, deleting and also checking for existence of data is simple and easy.

Another benefit of Web Storage API is that all data store are private. When you store some data either in local storage or in session other websites can't access them. This applies also if you open a page over HTTP protocol and then over HTTPS protocol. The later will not be able to access data stored over HTTP.

These privacy restrictions also apply to severs. Web Storage is available only in the browser. You access it via the `window` object. This object doesn't exist on the server. So, you don't have to worry about your storage data being send to the server, like cookies often are.

## The local storage and session storage

The Web Storage API offers two types of storage. The first one is local storage. The second is session storage. Both these storage types work with the same methods and store, and retrieve, the data in the same format. Where these storage types differ is how long they store the data.

### Local storage

When you store some data in local storage these data will persist even when you close the browser. If you open the browser again, you will be able to retrieve the data you stored previously. There is also no expiration date. So, even if you give it a few days, or weeks, your data will persist.

The only way to delete data in local storage is by deleting them explicitly. You can do this in two ways. First, you can delete the data with JavaScript. The process similar to storing the data. The only difference is that you will use a different method.

The second way to remove data stored in local storage is by cleaning Browser cache and especially the Locally Stored Data. The amount of data you can store in a local storage will differ based on the device and browser you use. The average is usually somewhere around 5MB. This is still more than you can store in a cookie.

### Session storage

What about the session storage? When you store data in session storage these data will be available only for that page session. When you close the tab, or the browser, data in session storage are gone. If you open multiple browser windows, or tabs, with the same site all windows and tabs will use different session storage.

Similarly to local storage, the data you store in session storage are never send to the server. They are always kept in the browser. Unlike the local storage, session storage can handle more data. According to [some sources], session storage is limited only by only by system memory, at least in some browsers.

## Web Storage API methods

The Web Storage API provides couple of methods to store, retrieve and remove data in web storage. The nice thing is that all these methods work with local storage and also with session storage. When you want to use these methods, make sure to use the correct storage you want. let's take a look at these methods and how to use them.

### The setItem() method

The setItem() method is what you need when you want to store data, either in local storage or in sessions storage. This methods accepts two parameters. The first parameter is the `key`. The second parameter is the `value`. As you may guess, the storage is created as an object.

This is one reason why working with Web Storage API is easier than working with cookies. With Web Storage API, you can work with the data as you would with [objects]. You save data in the form of a key/value pairs. Then, you retrieve any stored data also by using specific key. This will give you the value assigned to this key.

```JavaScript
// Storing data in local storage with setItem() method
localStorage.setItem('name', 'Alex')

console.log(localStorage.name)
// Output:
// "Alex"


// Storing data in session storage with setItem() method
sessionStorage.setItem('name', 'Tom')

console.log(sessionStorage.name)
// Output:
// "Tom"
```

There are two things to remember when you want to store data in storage. First, The value you pass to `setItem()` method as a `key` and `value` must be strings. If you pass something else, it will be automatically converted to a string. This is important if you want to check for the type of value. That value will always be a string.

```JavaScript
// Storing data in local storage with setItem() method
localStorage.setItem('age', '35')

console.log(localStorage.age)
// Output:
// "35"

console.log(typeof localStorage.age)
// Output:
// "string"

// Storing data in session storage with setItem() method
sessionStorage.setItem('isAlive', true)

console.log(sessionStorage.isAlive)
// Output:
// "true"

console.log(typeof localStorage.isAlive)
// Output:
// "string"
```

The second thing is that there is no "updateItem" method. When you want to update some value the process is simple. You just have to use the same key. When you use the same key, new value will automatically overwrite the old one. This can be a good thing as well as a bad thing.

It can be a good thing because it makes it easier to work with Web Storage API. You don't have to remember another method. It can also be a bad thing because it makes it easier to accidentally overwrite your data. Way to avoid this is by paying attention to the keys you use. Make sure you are using unique, or make sure you really want to overwrite the data.

```JavaScript
// Overwriting data in local storage with setItem() method
localStorage.setItem('name', 'Jack')
localStorage.setItem('name', 'Andrei')

console.log(localStorage.name)
// Output:
// "Andrei"


// Overwriting data in session storage with setItem() method
sessionStorage.setItem('name', 'Sandra')
sessionStorage.setItem('name', 'Victoria')

console.log(sessionStorage.name)
// Output:
// "Victoria"
```

### An alternative to the setItem() method

There is one thing you may have notice on the previous examples. We were able to access data in web storage by using object dot notation. You can use the object dot notation not only to access data in a web storage but also to store them there. The syntax is similar to accessing.

The difference is that when you want to store some data in a key, an assignment has to follow the dot notation. You have to add equal sign and some expression you want to store, like `localStorage.newKey = 'some value'` or `sessionStorage.newKey = 'some value'`. This way, you can store data just as easily as with `setItem()` method.

```JavaScript
// Adding data to local storage with dot notation
localStorage.book = 'Zero to One'

console.log(localStorage.book)
// Output:
// "Zero to One"

// Adding data to session storage with dot notation
sessionStorage.book = 'Hard Things About Hard Things'

console.log(sessionStorage.book)
// Output:
// "Hard Things About Hard Things"
```

### The removeItem() method

```JavaScript
```

### The clear() method

```JavaScript
```

### The key() method

```JavaScript
```

## Conclusion: Getting Started with Web Storage API - Local Storage and Session Storage

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[IndexedDB]: https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API
[Cache]: https://developer.mozilla.org/en-US/docs/Web/API/Cache
[some sources]: http://www.gwtproject.org/doc/latest/DevGuideHtml5Storage.html
[objects]: https://blog.alexdevero.com/javascript-objects-pt1/

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
- https://flaviocopes.com/web-storage-api/
- https://javascript.info/localstorage
- https://blog.logrocket.com/the-complete-guide-to-using-localstorage-in-javascript-apps-ba44edb53a36/
- https://www.taniarascia.com/how-to-use-local-storage-with-javascript/
- https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
-->
