# JavaScript Style Guide

This is an introduction. Insert introduction here.

## Table of contents

* [Characters](#characters)
	* [Indents](#indents)
	* [Newlines](#newlines)
	* [Whitespace](#whitespace)
	* [Semicolons](#semicolons)
	* [Single and Double Quotes](#single-and-double-quotes)
	* [Braces](#braces)
	* [Line Length](#line-length)
* [Naming Conventions](#naming-conventions)
	* [Variables, Properties, and Functions](#variables-properties-and-functions)
	* [Classes](#classes)
	* [Constants](#constants)
	* [Conditions](#conditions)
* [Operators](#operators)
	* [Double and Triple Equals](#double-and-triple-equals)
	* [Ternary Operator](#ternary-operator)
* [Declarations](#declarations)
	* [Vars](#vars)
	* [Objects / Arrays](#objects--arrays)
* [Functions](#functions)
	* [Write Small Functions](#write-small-functions)
	* [Return Early From Functions](#return-early-from-functions)
	* [Name Your Closures](#name-your-closures)
	* [Avoid Nesting Closures](#avoid-nesting-closures)
	* [Method Chaining](#method-chaining)
* [Prototypes](#prototypes)
	* [Avoid Extending Native Prototypes](#avoid-extending-native-prototypes)
* [Comments](#comments)
	* [Use Slashes for Comments](#use-slashes-for-comments)
* [Misc.](#misc.)
	* [Object.freeze, Object.preventExtensions, Object.seal, with, eval](#objectfreeze-objectpreventextensions-objectseal-with-eval)
	* [Getters and Setters](#getters-and-setters)

## Characters

### Indents

Use 2 spaces for indenting your code and swear an oath to never mix tabs and
spaces - a special kind of hell is awaiting you otherwise.

### Newlines

Use UNIX-style newlines (`\n`), and a newline character as the last character
of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.

### Whitespace

Just like you brush your teeth after every meal, you clean up any trailing
whitespace in your JS files before committing. Otherwise the rotten smell of
careless neglect will eventually drive away contributors and/or co-workers.

### Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
a core value of our community. Consider the points of [the opposition][], but
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

### Single and Double Quotes

Use single quotes, unless you are writing JSON.

*Preferred:*

```js
var foo = 'bar';
```

*Not Preferred:*

```js
var foo = "bar";
```

### Braces

Your opening braces go on the same line as the statement.

*Preferred:*

```js
if (true) {
  console.log('winning');
}
```

*Not Preferred:*

```js
if (true)
{
  console.log('losing');
}
```

Also, notice the use of whitespace before and after the condition statement.

### Line Length

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

## Naming Conventions

### Variables, Properties, and Functions

Variables, properties and function names should use `lowerCamelCase`.  They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Preferred:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*Not Preferred:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

### Classes

Class names should be capitalized using `UpperCamelCase`.

*Preferred:*

```js
function BankAccount() {
}
```

*Not Preferred:*

```js
function bank_Account() {
}
```

### Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

Node.js / V8 actually supports mozilla's [const][const] extension, but
unfortunately that cannot be applied to class members, nor is it part of any
ECMA standard.

*Preferred:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Not Preferred:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

### Conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Preferred:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Not Preferred:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## Operators

### Double and Triple Equals

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Preferred:*

```js
var a = 0;
if (a !== '') {
  console.log('winning');
}

```

*Not Preferred:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### Ternary Operator

The ternary operator should not be used on a single line. Split it up into multiple lines instead.

*Preferred:*

```js
var foo = (a === b)
  ? 1
  : 2;
```

*Not Preferred:*

```js
var foo = (a === b) ? 1 : 2;
```

## Declarations

### Vars

Declare one variable per var statement, it makes it easier to re-order the
lines. However, ignore [Crockford][crockfordconvention] when it comes to
declaring variables deeper inside a function, just put the declarations wherever
they make sense.

*Preferred:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (keys.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*Not Preferred:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

### Objects / Arrays

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Preferred:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Not Preferred:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Functions

### Write Small Functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

### Return Early From Functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Preferred:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Not Preferred:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

### Name Your Closures

Feel free to give your closures a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Preferred:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*Not Preferred:*

```js
req.on('end', function() {
  console.log('losing');
});
```

### Avoid Nesting Closures

Use closures, but don't nest them. Otherwise your code will become a mess.

*Preferred:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Not Preferred:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```

### Method Chaining

One method per line should be used if you want to chain methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Preferred:*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });
```

*Not Preferred:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' }).populate('bar')
  .exec(function(err, user) {
    return true;
  });
```

## Prototypes

### Avoid Extending Native Prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Preferred:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*Not Preferred:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```

## Comments

### Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.

*Preferred:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Not Preferred:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## Misc.

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

### Getters and Setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)
