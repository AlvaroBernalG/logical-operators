# logical-operators

> A tiny library that abstracts away logical operators with the intention of improving code readability. Ideal for composing complex validation queries. 

[![Build Status](https://travis-ci.org/AlvaroBernalG/logical-operators.svg?branch=master)](https://travis-ci.org/AlvaroBernalG/logical-operators) [![npm version](https://badge.fury.io/js/logical-operators.svg)](https://badge.fury.io/js/logical-operators) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

## [](#i-disagree-with-rule-x-can-you-change-it)

## Install
```
$ npm install logical-operators --save
```

## Usage

### every ( && )...

```js
const { every } = require('logical-operators')
const is = require('library-that-validate-stuff')

const values = [1, 9, 7,'level', 'Venezuela', 'Caracas', 'Aba', 'hola', 10, undefined, 'USA']

const palindromeCities = every(is.string, is.palindrome, is.city)

values.filter(palindromeCities) // => ['Aba']

values.every(palindromeCities) // => false
  
values.some(palindromeCities) // => true

```

### some ( || ) ...
```js

const { some } = require('logical-operators')
const between = require('in-between')
const is = require('library-that-validate-stuff')

const values = ['a','b','two', 'd', 'x', 3, undefined, null,'three']

 
values.every(some(between('w','z'), is.number, between('a','c'))) // => false

values.filter(some(between('w','z'), is.number, between('a','c'))) // => ['b', 3, 'x']

```

### or  ( || )

Same as 'some' but only accepts 2 params

```js
const { or } = require('logical-operators')
const is = require('library-that-validate-stuff')

const values = [1,2,'three']

const string_or_number = or(is.string, is.number)

values.every(string_or_number) // => true

values.filter(string_or_number) // => [1, 2, 'three']

```

### both  ( && )

Same as 'every' but only accepts 2 params
```js

const { both } = require('logical-operators')
const is = require('library-that-validate-stuff')

const values = ['a','b','two']

const string_and_singleChar = both(is.string, is.singleChar)

values.every(string_and_singleChar) // => false

values.filter(string_and_singleChar) // => ['a','b']

```

### equal  ( == ) 

```js
const { equal, greater } = require('logical-operators')
const is = require('library-that-validate-stuff')
const compose = require('lodash/compose')

var getAsciiSum = (str) => str.split('').map(char => char.charCodeAt(0)).reduce((prev, next)=> prev+ next,0)

var values = [1,2,3, 'ab', 'e', 'T', 'W', '/']

values.every(
    is.string,
    equal(getAsciiSum, compose(greater(102).than, toAscii) ),
  ) // => false

values.filter(
    is.string,
    equal(getAsciiSum, compose(greater(100).than, toAscii) ),
  ) // => ['ab', 'e']

```



<!-- ### greater  ( > ) -->
<!--  -->
<!-- ```js -->
<!--  -->
<!-- const { both } = require('logical-operators') -->
<!-- const is = require('library-that-validate-stuff') -->
<!--  -->
<!-- const values = ['a','b','two'] -->
<!--  -->
<!-- const greaterThan2 = greater(2).than -->
<!--  -->
<!-- values.every(greaterThan2) // => false -->
<!--  -->
<!-- values.filter(string_and_singleChar) // => ['a','b'] -->
<!--  -->
<!-- ``` -->


## License

MIT © [Alvaro Bernal](https://github.com/AlvaroBernalG/) 
