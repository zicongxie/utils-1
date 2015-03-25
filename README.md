# utils [![NPM version](https://badge.fury.io/js/utils.svg)](http://badge.fury.io/js/utils)  [![Build Status](https://travis-ci.org/jonschlinkert/utils.svg)](https://travis-ci.org/jonschlinkert/utils) 

> Fast, generic JavaScript/node.js utility functions.

**Goals**

- Fastest implementation of each method, without too much compromise. Covering uncommon cases is fine, but don't go overboard.
- Clean well-documented, commented code.
- [When it makes sense](#adding-utils), external libraries are used and exposed instead of writing new code. 
- Focus on node.js usage and projects that are likely to use a number of these utils in one project. If you only need one or two of these in a small project, don't use this. Use small modules that do only one thing.

## Install with [npm](npmjs.org)

```bash
npm i utils --save
```

## TOC

<!-- toc -->

- [Usage](#usage)
- [Code links](#code-links)
- [API](#api)
- [Code coverage](#code-coverage)
- [Running tests](#running-tests)
- [Contributing](#contributing)
  * [Adding utils](#adding-utils)

<!-- tocstop -->

## Usage

**Utils grouped by collection**

The top level export gives you an object with utils grouped into collections, like `array`, `object`, `math`, etc:

```js
var utils = require('utils');
//=> {array: {flatten: [function], ...}, collection: {...}}
```

See [example.md](./example.md) for visual representation of the object.


**Get all utils on one object**

If you want all utils on a single object (e.g. not grouped by collection):

```js
// all utils are on the `_` property
var utils = require('utils')._;
```

**Only get a specific collection**

If you just want the `string` or `object` utils:

```js
var string = require('utils').string;
var object = require('utils').object;
```


## Code links 
These links take you to the code for each function. There are currently 0 utils in 7 sub-categories:



## API
### [.after](./lib/array/after.js#L19)

Returns all of the items in an array after the specified index.

* `array` **{Array}**: Collection    
* `n` **{Number}**: Starting index (number of items to exclude)    
* `returns` **{Array}**: Array exluding `n` items.  

```js
after(['a', 'b', 'c'], 1)
//=> ['c']
```

### [.arrayify](./lib/array/arrayify.js#L20)

Cast the give `value` to an array.

* `val` **{*}**    
* `returns`: {Array}  

```js
arrayify('abc')
//=> ['abc']

arrayify(['abc'])
//=> ['abc']
```

### [.before](./lib/array/before.js#L20)

Returns all of the items in an array up to the specified number Opposite of `<%= after() %`.

* `array` **{Array}**    
* `n` **{Number}**    
* `returns` **{Array}**: Array excluding items after the given number.  

```js
before(['a', 'b', 'c'], 2)
//=> ['a', 'b']
```

### [.compact](./lib/array/compact.js#L17)

Remove all falsey values from an array.

* `arr` **{Array}**    
* `returns`: {Array}  

```js
compact([null, a, undefined, 0, false, b, c, '']);
//=> [a, b, c]
```

### [.difference](./lib/array/difference.js#L24)

Return the difference between the first array and additional arrays.

* `a` **{Array}**    
* `b` **{Array}**    
* `returns`: {Array}  

```js
var a = ['a', 'b', 'c', 'd'];
var b = ['b', 'c'];

diff(a, b);
//=> ['a', 'd']
```

### [.first](./lib/array/first.js#L20)

Returns the first item, or first `n` items of an array.

* `array` **{Array}**    
* `n` **{Number}**: Number of items to return, starting at `0`.    
* `returns`: {Array}  

```js
first(['a', 'b', 'c', 'd', 'e'], 2)
//=> ['a', 'b']
```

### [.flatten](./lib/array/flatten.js#L18)

Recursively flatten an array or arrays. Uses the fastest implementation of array flatten for node.js

* `array` **{Array}**    
* `returns` **{Array}**: Flattened array  

```js
flatten(['a', ['b', ['c']], 'd', ['e']]);
//=> ['a', 'b', 'c', 'd', 'e']
```

### [.forEach](./lib/array/forEach.js#L27)

Loop over each item in an array and call the given function on every element.

* `array` **{Array}**    
* `fn` **{Function}**    
* `thisArg` **{Object}**: Optionally pass a `thisArg` to be used as the context in which to call the function.    
* `returns`: {Array}  

```js
forEach(['a', 'b', 'c'], function (ele) {
  return ele + ele;
});
//=> ['aa', 'bb', 'cc']

forEach(['a', 'b', 'c'], function (ele, i) {
  return i + ele;
});
//=> ['0a', '1b', '2c']
```





### [.isArray](./lib/array/isArray.js#L19)

Returns true if the given `value` is an array.

* `value` **{Array}**: Value to test.    

```js
isArray(1);
//=> 'false'

isArray([1]);
//=> 'true'
```

### [.last](./lib/array/last.js#L20)

Returns the last item, or last `n` items of an array.

* `array` **{Array}**    
* `n` **{Number}**: Number of items to return, starting with the last item.    
* `returns`: {Array}  

```js
last(['a', 'b', 'c', 'd', 'e'], 2)
//=> ['d', 'e']
```

### [.map](./lib/array/map.js#L27)

Returns a new array with the results of calling the given function on every element in the array. This is a faster, node.js focused alternative to JavaScript's native array map.

* `array` **{Array}**    
* `fn` **{Function}**    
* `returns`: {Array}  

```js
map(['a', 'b', 'c'], function (ele) {
  return ele + ele;
});
//=> ['aa', 'bb', 'cc']

map(['a', 'b', 'c'], function (ele, i) {
  return i + ele;
});
//=> ['0a', '1b', '2c']
```



### [.union](./lib/array/union.js#L19)

Return an array free of duplicate values. Fastest ES5 implementation.

* `array` **{Array}**: The array to uniquify    
* `returns` **{Array}**: With all union values.  

```js
union(['a', 'b', 'c', 'c']);
//=> ['a', 'b', 'c']
```

### [.unique](./lib/array/unique.js#L19)

Return an array free of duplicate values. Fastest ES5 implementation.

* `array` **{Array}**: The array to uniquify    
* `returns` **{Array}**: With all unique values.  

```js
unique(['a', 'b', 'c', 'c']);
//=> ['a', 'b', 'c']
```

### [.any](./lib/collection/any.js#L14)

* `value` **{*}**    
* `target` **{*}**    
* `options` **{Object}**    

Returns `true` if `value` exists in the given string, array
or object. See [any] for documentation.

### [.contains](./lib/collection/contains.js#L17)

* `collection` **{Array|Object}**    
* `string` **{*}**    
* `returns`: {Boolean}  

Return true if `collection` contains `value`





### [.tryReaddir](./lib/fs/tryReaddir.js#L16)

* `dir` **{String}**: Starting directory    
* `returns` **{Array}**: Array of files.  

Try to read the given `directory`. Wraps `fs.readdirSync()` with
a try/catch, so it fails silently instead of throwing when the
directory doesn't exist.

### [.tryRequire](./lib/fs/tryRequire.js#L15)

* `fp` **{String}**: File path of the file to require    
* `returns` **{*}**: Returns the module function/object, or `null` if not found.  

Try to require the given file, returning `null` if not successful
instead of throwing an error.



### [.hasValues](./lib/lang/hasValues.js#L34)

Returns true if any value exists, false if empty. Works for booleans, functions, numbers, strings, nulls, objects and arrays.

* `object` **{Object}**: The object to check for `value`    
* `value` **{*}**: the value to look for    
* `returns` **{Boolean}**: True if any values exists.  

```js
utils.lang.hasValues('a');
//=> true

utils.lang.hasValues('');
//=> false

utils.lang.hasValues(1);
//=> true

utils.lang.hasValues({a: 'a'}});
//=> true

utils.lang.hasValues({}});
//=> false

utils.lang.hasValues(['a']);
//=> true
```



### [.isArguments](./lib/lang/isArguments.js#L18)

Return true if the given `value` is an arguments object.

* `value` **{*}**: The value to check.    
* `returns`: {Boolean}  

```js
isArguments(arguments)
//=> 'true'
```

### [.isEmpty](./lib/lang/isEmpty.js#L37)

Returns true if the given value is empty, false if any value exists. Works for booleans, functions, numbers, strings, nulls, objects and arrays.

* `object` **{Object}**: The object to check for `value`    
* `value` **{*}**: the value to look for    
* `returns` **{Boolean}**: False if any values exists.  

```js
utils.lang.isEmpty('a');
//=> true

utils.lang.isEmpty('');
//=> false

utils.lang.isEmpty(1);
//=> true

utils.lang.isEmpty({a: 'a'}});
//=> true

utils.lang.isEmpty({}});
//=> false

utils.lang.isEmpty(['a']);
//=> true
```

### [.isObject](./lib/lang/isObject.js#L22)

Return true if the given `value` is an object with keys.

* `value` **{Object}**: The value to check.    
* `returns`: {Boolean}  

```js
isObject(['a', 'b', 'c'])
//=> 'false'

isObject({a: 'b'})
//=> 'true'
```

### [.isPlainObject](./lib/lang/isPlainObject.js#L23)

Return true if the given `value` is an object with keys.

* `value` **{Object}**: The value to check.    
* `returns`: {Boolean}  

```js
isPlainObject(Object.create({}));
//=> true
isPlainObject(Object.create(Object.prototype));
//=> true
isPlainObject({foo: 'bar'});
//=> true
isPlainObject({});
//=> true
```



### [.sum](./lib/math/sum.js#L20)

Returns the sum of all numbers in the given array.

* `array` **{Array}**: Array of numbers to add up.    
* `returns`: {Number}  

```js
sum([1, 2, 3, 4, 5])
//=> '15'
```

### [.extend](./lib/object/extend.js#L16)

* `o` **{Object}**: The target object. Pass an empty object to shallow clone.    
* `objects` **{Object}**    
* `returns`: {Object}  

Extend `o` with properties of other `objects`.







### [.functions](./lib/object/functions.js#L20)

Returns a copy of the given `obj` filtered to have only enumerable properties that have function values.

* `obj` **{Object}**    
* `returns`: {Object}  

```js
functions({a: 'b', c: function() {}});
//=> {c: function() {}}
```

### [.hasOwn](./lib/object/hasOwn.js#L18)

Return true if `key` is an own, enumerable property of the given `obj`.

* `key` **{String}**    
* `obj` **{Object}**: Optionally pass an object to check.    
* `returns`: {Boolean}  

```js
hasOwn(obj, key);
```



### [.keys](./lib/object/keys.js#L15)

* `obj` **{Object}**    
* `returns` **{Array}**: Array of keys.  

Return an array of keys for the given `obj`. Uses `Object.keys`
when available, otherwise falls back on `forOwn`.

### [merge](./lib/object/merge.js#L23)

* `o` **{Object}**: The target object. Pass an empty object to shallow clone.    
* `objects` **{Object}**    
* `returns`: {Object}  

Recursively combine the properties of `o` with the
properties of other `objects`.

### [.methods](./lib/object/methods.js#L15)

* `obj` **{Object}**    
* `returns`: {Array}  

Returns a list of all enumerable properties of `obj` that have function
values









### [.camelcase](./lib/string/camelcase.js#L20)

camelCase the characters in `string`.

* `string` **{String}**: The string to camelcase.    
* `returns`: {String}  

```js
camelcase("foo bar baz");
//=> 'fooBarBaz'
```

### [.centerAlign](./lib/string/centerAlign.js#L21)

Center align the characters in a string using non-breaking spaces.

* `str` **{String}**: The string to reverse.    
* `returns` **{String}**: Centered string.  

```js
centerAlign("abc");
```

### [.chop](./lib/string/chop.js#L26)

Like trim, but removes both extraneous whitespace and non-word characters from the beginning and end of a string.

* `string` **{String}**: The string to chop.    
* `returns`: {String}  

```js
chop("_ABC_");
//=> 'ABC'

chop("-ABC-");
//=> 'ABC'

chop(" ABC ");
//=> 'ABC'
```

### [.count](./lib/string/count.js#L21)

Count the number of occurrances of a substring within a string.

* `string` **{String}**    
* `substring` **{String}**    
* `returns` **{Number}**: The occurances of `substring` in `string`  

```js
count("abcabcabc", "a");
//=> '3'
```

### [.dashcase](./lib/string/dashcase.js#L22)

dash-case the characters in `string`. This is similar to [slugify], but [slugify] makes the string compatible to be used as a URL slug.

* `string` **{String}**    
* `returns`: {String}  

```js
dashcase("a b.c d_e");
//=> 'a-b-c-d-e'
```

### [.dotcase](./lib/string/dotcase.js#L20)

dot.case the characters in `string`.

* `string` **{String}**    
* `returns`: {String}  

```js
dotcase("a-b-c d_e");
//=> 'a.b.c.d.e'
```

### [.ellipsis](./lib/string/ellipsis.js#L23)

Truncate a string to the specified `length`, and append it with an elipsis, `…`.

* `str` **{String}**    
* `length` **{Number}**: The desired length of the returned string.    
* `ch` **{String}**: Optionally pass custom characters to append. Default is `…`.    
* `returns` **{String}**: The truncated string.  

```js
ellipsis("<span>foo bar baz</span>", 7);
//=> 'foo bar…'
```

### [.hyphenate](./lib/string/hyphenate.js#L20)

Replace spaces in a string with hyphens. This

* `string` **{String}**    
* `returns`: {String}  

```js
hyphenate("a b c");
//=> 'a-b-c'
```



### [.isString](./lib/string/isString.js#L20)

Returns true if the value is a string.

* `val` **{String}**    
* `returns` **{Boolean}**: True if the value is a string.  

```js
isString('abc');
//=> 'true'

isString(null);
//=> 'false'
```

### [.pascalcase](./lib/string/pascalcase.js#L20)

PascalCase the characters in `string`.

* `string` **{String}**    
* `returns`: {String}  

```js
pascalcase("foo bar baz");
//=> 'FooBarBaz'
```

### [.pathcase](./lib/string/pathcase.js#L20)

path/case the characters in `string`.

* `string` **{String}**    
* `returns`: {String}  

```js
pathcase("a-b-c d_e");
//=> 'a/b/c/d/e'
```

### [.replace](./lib/string/replace.js#L21)

Replace occurrences of `a` with `b`.

* `str` **{String}**    
* `a` **{String|RegExp}**: Can be a string or regexp.    
* `b` **{String}**    
* `returns`: {String}  

```js
replace("abcabc", /a/, "z");
//=> 'zbczbc'
```

### [.reverse](./lib/string/reverse.js#L19)

Reverse the characters in a string.

* `str` **{String}**: The string to reverse.    
* `returns`: {String}  

```js
reverse("abc");
//=> 'cba'
```

### [.rightAlign](./lib/string/rightAlign.js#L21)

Right align the characters in a string using non-breaking spaces.

* `str` **{String}**: The string to reverse.    
* `returns` **{String}**: Right-aligned string.  

```js
rightAlign(str);
```

### [.sentencecase](./lib/string/sentencecase.js#L19)

Sentence-case the characters in `string`.

* `string` **{String}**    
* `returns`: {String}  

```js
sentencecase("foo bar baz.");
//=> 'Foo bar baz.'
```



### [.snakecase](./lib/string/snakecase.js#L20)

snake_case the characters in `string`.

* `string` **{String}**    
* `returns`: {String}  

```js
snakecase("a-b-c d_e");
//=> 'a_b_c_d_e'
```



### [.truncate](./lib/string/truncate.js#L21)

Truncate a string by removing all HTML tags and limiting the result to the specified `length`.

* `str` **{String}**    
* `length` **{Number}**: The desired length of the returned string.    
* `returns` **{String}**: The truncated string.  

```js
truncate("<span>foo bar baz</span>", 7);
//=> 'foo bar'
```

### [.wordwrap](./lib/string/wordwrap.js#L21)

Wrap words to a specified width using [word-wrap].

* `string` **{String}**: The string with words to wrap.    
* `object` **{Options}**: Options to pass to [word-wrap]    
* `returns` **{String}**: Formatted string.  

```js
wordwrap("a b c d e f", {width: 5, newline: '<br>  '});
//=> '  a b c <br>  d e f'
```

## Code coverage
-----------------------|-----------|-----------|-----------|-----------|
File                   |   % Stmts |% Branches |   % Funcs |   % Lines |
-----------------------|-----------|-----------|-----------|-----------|
   array/              |     76.24 |     67.19 |     85.71 |     77.32 |
      after.js         |       100 |        75 |       100 |       100 |
      arrayify.js      |       100 |       100 |       100 |       100 |
      before.js        |       100 |        75 |       100 |       100 |
      compact.js       |       100 |       100 |       100 |       100 |
      difference.js    |       100 |       100 |       100 |       100 |
      first.js         |     88.89 |     83.33 |       100 |     88.24 |
      flatten.js       |       100 |       100 |       100 |       100 |
      forEach.js       |      12.5 |         0 |         0 |     14.29 |
      indexOf.js       |      7.69 |         0 |         0 |      8.33 |
      isArray.js       |       100 |       100 |       100 |       100 |
      last.js          |     88.89 |     83.33 |       100 |     88.24 |
      map.js           |       100 |       100 |       100 |       100 |
      sort.js          |     90.91 |      87.5 |       100 |     90.91 |
      union.js         |       100 |       100 |       100 |       100 |
      unique.js        |       100 |       100 |       100 |       100 |
   collection/         |        50 |         0 |         0 |        50 |
      any.js           |       100 |       100 |       100 |       100 |
      contains.js      |     42.86 |         0 |         0 |     42.86 |
   fs/                 |        80 |       100 |       100 |        80 |
      tryReaddir.js    |        80 |       100 |       100 |        80 |
      tryRequire.js    |        80 |       100 |       100 |        80 |
   lang/               |        75 |        50 |        25 |        75 |
      hasValues.js     |       100 |       100 |       100 |       100 |
      isArguments.js   |        50 |        25 |         0 |        50 |
      isEmpty.js       |     66.67 |       100 |         0 |     66.67 |
      isObject.js      |       100 |       100 |       100 |       100 |
      isPlainObject.js |       100 |       100 |       100 |       100 |
   math/               |       100 |       100 |       100 |       100 |
      sum.js           |       100 |       100 |       100 |       100 |
   object/             |     69.57 |     54.55 |     27.27 |     68.66 |
      extend.js        |       100 |     83.33 |       100 |       100 |
      filter.js        |       100 |       100 |       100 |       100 |
      forIn.js         |       100 |       100 |       100 |       100 |
      forOwn.js        |       100 |       100 |       100 |       100 |
      functions.js     |     28.57 |         0 |         0 |     28.57 |
      hasOwn.js        |       100 |       100 |       100 |       100 |
      keys.js          |     33.33 |        50 |         0 |     33.33 |
      merge.js         |       100 |        75 |       100 |       100 |
      methods.js       |     28.57 |         0 |         0 |     28.57 |
      omit.js          |       100 |       100 |       100 |       100 |
      pick.js          |       100 |       100 |       100 |       100 |
      reduce.js        |       100 |       100 |       100 |       100 |
      some.js          |        30 |         0 |         0 |        30 |
   string/             |     99.27 |     96.77 |        96 |     99.09 |
      camelcase.js     |       100 |       100 |       100 |       100 |
      centerAlign.js   |       100 |       100 |       100 |       100 |
      chop.js          |       100 |       100 |       100 |       100 |
      count.js         |       100 |       100 |       100 |       100 |
      dashcase.js      |       100 |       100 |       100 |       100 |
      dotcase.js       |       100 |       100 |       100 |       100 |
      ellipsis.js      |       100 |       100 |       100 |       100 |
      hyphenate.js     |       100 |       100 |       100 |       100 |
      index.js         |       100 |       100 |       100 |       100 |
      isString.js      |       100 |       100 |       100 |       100 |
      pascalcase.js    |       100 |       100 |       100 |       100 |
      pathcase.js      |       100 |       100 |       100 |       100 |
      replace.js       |       100 |       100 |       100 |       100 |
      reverse.js       |       100 |       100 |       100 |       100 |
      rightAlign.js    |       100 |       100 |       100 |       100 |
      sentencecase.js  |       100 |       100 |       100 |       100 |
      slugify.js       |       100 |       100 |       100 |       100 |
      snakecase.js     |       100 |       100 |       100 |       100 |
      toString.js      |        50 |         0 |         0 |        50 |
      truncate.js      |       100 |       100 |       100 |       100 |
      wordwrap.js      |       100 |       100 |       100 |       100 |
-----------------------|-----------|-----------|-----------|-----------|
All files              |     84.15 |     75.95 |     72.88 |     83.12 |
-----------------------|-----------|-----------|-----------|-----------|


## Running tests
Install dev dependencies.

```bash
npm i -d && npm test
```

## Contributing
Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/utils/issues)

### Adding utils

> Pull requests are always welcome, whether it's for fixing typos, improving docs, or anything else.

If you want to do a PR to add a util, please read the following first:
 
- follow the same coding style as the rest of the library, same with code comments
- add sufficient unit tests
- Install dev dependencies and run `verb` 
- Look over the README to make sure that verb rendered out the docs with your method and code comments.

**Adding external modules as dependencies**

- External modules will only be considered if they meet the same quality and coding standards as the rest of the library. At minimum this includes documentation, code comments, and unit tests. Benchmarks are also strongly preferred.

## Author

**Jon Schlinkert**
 
+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert) 

## License
Copyright (c) 2015 Jon Schlinkert  
Released under the MIT license

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on March 25, 2015._

[assemble]: https://github.com/assemble/assemble
[verb]: https://github.com/assemble/verb
[template]: https://github.com/jonschlinkert/template
[word-wrap]: https://github.com/jonschlinkert/word-wrap
[helper-concat]: https://github.com/helpers/helper-concat
[path]: https://nodejs.org/api/path.html
<!-- deps:mocha jshint-stylish -->

{%= reflinks('') %}