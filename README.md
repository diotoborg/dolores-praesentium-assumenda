# @diotoborg/dolores-praesentium-assumenda
Make a callback-based or promise-based functions to support both promises and callbacks.  Uses the native promise implementation. with typescript support.

[![npm Package](https://img.shields.io/npm/v/@diotoborg/dolores-praesentium-assumenda.svg)](https://www.npmjs.org/package/@diotoborg/dolores-praesentium-assumenda)
[![License](https://img.shields.io/npm/l/@diotoborg/dolores-praesentium-assumenda.svg)](https://github.com/diotoborg/dolores-praesentium-assumenda/blob/main/LICENSE)


Installation
------------

    npm i @diotoborg/dolores-praesentium-assumenda


Import or Require
-----------------
    import ppc from "@diotoborg/dolores-praesentium-assumenda";
    OR
    import {fromCallback,fromPromise} from "@diotoborg/dolores-praesentium-assumenda";
    OR
    const ppc = require("@diotoborg/dolores-praesentium-assumenda");
    OR
    const fromCallback = require("@diotoborg/dolores-praesentium-assumenda");
    OR
    const fromPromise = require("@diotoborg/dolores-praesentium-assumenda");

## Here is an example usage of `fromCallback` function:

Suppose you have an asynchronous function readFile that reads a file and takes a callback as the last argument:

```js
function readFile(filename, callback) {
  // Asynchronous operation to read file
}
```
You can convert this function to return a Promise with `fromCallback` function as follows:
```js
import {fromCallback} from "@diotoborg/dolores-praesentium-assumenda";

const readFilePromise = fromCallback(readFile);

// You can now call the function with a Promise:
readFilePromise(filename)
  .then((data) => console.log(data))
  .catch((err) => console.error(err));

// Or with a callback:
readFilePromise(filename, (err, data) => {
  if (err) {
    console.error(err);
  } else {
    console.log(data);
  }
});
```
This allows you to use the same function in either Promise-based or callback-based code.


## Here is an example usage of `fromPromise` function:

Suppose we have a function getUser that returns a promise:
```js
function getUser(userId) {
  return new Promise((resolve, reject) => {
    // some async operation to fetch user
    setTimeout(() => {
      if (userId === '123') {
        resolve({ id: '123', name: 'John Doe' });
      } else {
        reject(new Error('User not found'));
      }
    }, 100);
  });
}
```
We can use `fromPromise` to create a function that can be called with a callback:
```js
import {fromPromise} from "@diotoborg/dolores-praesentium-assumenda";

const getUserCallback = fromPromise(getUser);

getUserCallback('123', (err, user) => {
  if (err) {
    console.error(err);
  } else {
    console.log(user); // { id: '123', name: 'John Doe' }
  }
});
```
In the above example, the getUserCallback function accepts a callback as its last argument. If a callback is provided, it calls the original getUser function with the provided arguments and passes the result or error to the callback. If no callback is provided, it returns a promise.

We can also call getUserCallback without a callback to get a promise:
```js
getUserCallback('123')
  .then(user => console.log(user)) // { id: '123', name: 'John Doe' }
  .catch(err => console.error(err));
```

# License
@diotoborg/dolores-praesentium-assumenda is licensed under the MIT License.