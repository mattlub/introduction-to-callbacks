# Introduction to callbacks in javascript

A callback is simply a function which is passed as an argument to another function. The callback function can then be *called*, or *invoked*, by the other function.

### Example
```js
function double (n) {
  return 2 * n
}

function addThenDo (x, y, callback) {
  // a function which adds its two first arguments and call its third argument with the result
  var sum = x + y
  return callback(sum)
}

// invoke our addThenDo function, passing our double function as an argument
addThenDo(3, 5, double) // returns 16
```

Of course, we could also pass any numbers and any other function as arguments to ```addThenDo```:
```js
addThenDo(3.2, 5, Math.floor) // returns 8

// passing an anonymous function
addThenDo(1, 2, function (n) {
  console.log('the sum is ' + n + '!')
}) // logs 'the sum is 3!'
```

### Important things to note and get used to:

1. The word ```callback``` used above is just a variable name in a function definition, so it could be anything- using ```callback``` is just more explicit. The same applies for the other arguments. The following function is *exactly* the same as the previous one:

```js
function addThenDo (wtf, omg, lol) {
  var sum = wtf + omg
  return lol(sum)
}
```

2. We do not know or control what **specific** function will be passed when the function is called. If this makes you uncomfortable, this is ok! Just like other variables in function definitions, we cannot make sure they are of the right type. So for example, in the ```addThenDo``` example:

```js
addThenDo(3, 4, 7) // will cause an error, because 7 is not a function
```

This is as a result of javascript being very relaxed about types. We could manage this by, for example, checking that the supplied arguments are of the correct type.

For this reason, and especially if the function is to be used by other people (or your future self), it might be useful to re-write the function specifying expected arguments:

```js
function addThenDo (x, y, callback) {
  // a function which adds its two first arguments and call its third argument with the result
  // input arguments
  //   x: number
  //   y: number
  //   callback: function which takes one number as input
  var sum = x + y
  return callback(sum)
}
```

3. you invoke a function using parentheses, ```myFunction()```, and the value of this statement is the return value of the function. When you pass a function as an argument to a function, it will be without parentheses. To return to the previous example, and writing the `double` function slightly differently:

```js
var double = function (n) {
  return 2 * n
}

typeof double // function
typeof double(2) // number
```



