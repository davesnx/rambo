# Rambo

> Automatic Ramda solution bot

![rambo](rambo.jpg)

Given inputs and outputs brute forces a Ramda solution.

## Example

What Ramda solution given `[1, 2, 3, 4]` returns `[5, 6, 7, 8]`?

```js
const solve = require('rambo').solve
const solution = solve([1, 2, 3, 4], [5, 6, 7, 8])
console.log(solution.name) // "R.map(R.add(4))"
// has "f" property with solution function
console.log(solution.f([1, 2, 3, 4])) // [5, 6, 7, 8]
// can apply to other inputs
console.log(solution.f([20, 30])) // [24, 34]
```

## Produce example

Some cases do not have any inputs. For example, what Ramda command produces `[50, 51, 52]`?

```js
const produce = require('rambo').produce
const solution = produce([50, 51, 52])
console.log(solution.name) // "R.range(50, 53)"
console.log(solution.f()) // [50, 51, 52]
```

## Why?

Because there are 200 functions in Ramda library, and I constantly have to look up
[which function I should use](https://github.com/ramda/ramda/wiki/What-Function-Should-I-Use%3F).
Plus there is `ram-bot` in the [Ramda Gitter channel](https://gitter.im/ramda/ramda) that given
input and Ramda code computes the output. I wanted to find Ramda code that computes the answer!

```
// ram-bot
Ramda code (inputs) ===> ?
// Rambo
Ramda ? (inputs) ===> outputs
```

## How?

The solver is **very simple** and just brute forces the solution by iterating over a bunch of
functions. Since Ramda is sooooo good at currying, we can combine multiple functions by 
providing *derived* functions as inputs to other functions, like `R.map` for example, as first
arguments. I also use the *data* to guide the solution tries. For example, `R.has(...)` tries
every string from the input and output as a property name.

```js
const solve = require('rambo').solve
const input = [{foo: 'bar'}, {name: 'alice'}, {name: 'bob'}, {foo: 42}]
const output = [{name: 'alice'}, {name: 'bob'}]
solve(input, output)
// tries R.map(R.has('foo'))
// tries R.map(R.has('name'))
// tries R.map(R.has('bar'))
// tries R.map(R.has('alice'))
// ...
```

Hope others can contribute to this effort, since I know nothing about symbolic computation and
automatic solvers. Rambo is my attempt at brute forcing a problem with a small solution set.

## Details

You can provide multiple input / output pairs

```js
const solution = solve([
  [input1, output1],
  [input2, output2],
  ...
])
```

This is useful because sometimes there might be multiple solutions for a single input / output
pair.

[![NPM][npm-icon] ][npm-url]

[![Build status][ci-image] ][ci-url]
[![semantic-release][semantic-image] ][semantic-url]
[![js-standard-style][standard-image]][standard-url]

### Small print

Author: Gleb Bahmutov &lt;gleb.bahmutov@gmail.com&gt; &copy; 2016


* [@bahmutov](https://twitter.com/bahmutov)
* [glebbahmutov.com](http://glebbahmutov.com)
* [blog](http://glebbahmutov.com/blog)


License: MIT - do anything with the code, but don't blame me if it does not work.

Support: if you find any problems with this module, email / tweet /
[open issue](https://github.com/bahmutov/rambo/issues) on Github

## MIT License

Copyright (c) 2016 Gleb Bahmutov &lt;gleb.bahmutov@gmail.com&gt;

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

[npm-icon]: https://nodei.co/npm/rambo.png?downloads=true
[npm-url]: https://npmjs.org/package/rambo
[ci-image]: https://travis-ci.org/bahmutov/rambo.png?branch=master
[ci-url]: https://travis-ci.org/bahmutov/rambo
[semantic-image]: https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg
[semantic-url]: https://github.com/semantic-release/semantic-release
[standard-image]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg
[standard-url]: http://standardjs.com/
