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

## Conclusion: Getting Started with Web Storage API - Local Storage and Session Storage

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[IndexedDB]: https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API
[Cache]: https://developer.mozilla.org/en-US/docs/Web/API/Cache
[some sources]: http://www.gwtproject.org/doc/latest/DevGuideHtml5Storage.html

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