# Blog post title [...]
<!--more-->
<!--
Table of Contents:
-->

## Introduction

## Promises and states

pending: initial state, neither fulfilled nor rejected.

fulfilled: meaning that the operation completed successfully.

rejected: meaning that the operation failed.

## Promise methods

### Promise.resolve()

### Promise.reject()

Promise.prototype.catch()
Promise.prototype.finally()
Promise.prototype.then()

### Promise.all()

Promise.all will immediately reject if any of the promises fail to resolve, wherease Promise.allSettled will await the completion of all promises.

Promise.all() is passed an iterable (usually an array of other promises) and will attempt to resolve all of them. If any of these promises throws an exception or rejects, Promise.all will immediateley invoke its reject.

### Promise.allSettled()

Promise.allSettled() is also passed an iterable (usually an array of other promises) and will attempt to resolve all of them. If any of these promises throws an exception or rejects, its status is set to rejected.

An important note is that Promise.allSettled can never throw. You do not need to wrap it with try/catch - it will always resolve.

### Promise.race()

The Promise.race() method returns a promise that fulfills or rejects as soon as one of the promises in an iterable fulfills or rejects, with the value or reason from that promise. 1

### Promise.any()

## Conclusion: [...] ...

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[]:

<!--
### Meta:
-
-->

<!--
### Resources:
- https://blog.jonlu.ca/posts/promises
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
-->
