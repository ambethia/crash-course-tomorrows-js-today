build-lists: true
autoscale: true
slidenumbers: true

![fit](tiy-standard-logo.png)

---

# Tomorrow's JavaScript,
# [fit] Today.

^ In this Crash Course we're going to be talking about the features of that are both upcoming and recently added to the **JavaScript** language. The changes we are going to be discussing are the first _major_ changes to the language in over 15 years.

---

## Audience

^ This Crash Course is meant for folks with at least an intermediate level of JavaScript knowledge and some understanding of things like **prototypes**, **scopes**, **bindings**, and `this`.

---

## What is "ECMAScript?"

^ **ECMAScript** is the standardized specification of the programming language we commonly know as "JavaScript". The last version of JavaScript was ECMAScript 3, formalized in 1999 only a few years after it was first created by Brendan Eich at Netscape in 1995.

![](http://www.commdiginews.com/wp-content/uploads/2014/04/brendan-eich.jpg)

---

### Ecma International

^ **Ecma International** is a non-profit standards organization. ECMA originally stood for "European Computer Manufacturers Association", but later abandoned the meaning of the acronym and changed it's name to Ecma International, similar to "Aol." and "KFC".

---

^ What we've been using since the 90s is basically ECMAScript 3. ES 4 failed to be ratified and was mostly abandoned. Some of the work on continued under the code name "Harmony", and you'll often see references to **ES.Harmony** still.

^ ES5 was finalized in 2009, but browser support wasn't realistic until 2012, when older versions of Internet Explorer started dying off. Still, ES5 was not a huge change. We got native support for JSON parsing a few other things.

^ "**ECMA International Technical Committee 39**" is the group responsible for drafting and finalizing the specification of ECMAScript specifications. In 2015 they decided to move to a yearly schedule for defining standards. ES6 was actually renamed to ES2015 before being published.

^ What were previously referred to as **ES.Next** and **ES7** are now known as **ES2016** which is still being written, although many of the proposals are available to use today. We'll talk about that in a bit.

![](https://m.popkey.co/1aa97b/pJvNr.gif)

---

### Other implementations and dialects

- ActionScript
- UnityScript
- JerryScript

^ **ActionScript**, used in Flash development. Originally by Macromedia and eventually Adobe.
^ **UnityScript**, used in the Unity Game engine, often marketed as "JavaScript", but does not have prototypal inheritance. It's built on the .Net/Mono CLR.
^ **JerryScript**, Samsung's implementation of JavaScript for embedded systems and The Internet of Things, running on devices with under 64KB of RAM. Neat!

---

# Features

^ Let's start getting into some of the features of ES2015 now.

![](https://m.popkey.co/d2dce5/MwbyL.gif)

---

## `let` & `const`

### Forget `var`.

^ You'll never need to use it again. `let` replaces `var`, with tighter block level scoping. This can help reduce bugs related to _variable hoisting_. With `var`, `i` is scoped the the entire **function** it is defined in.

---

^ In this case, `i` leaks outside of the for loop:

```js
(function() {
  for (var i = 0; i < 2; i++) {
    // ...
  }
  console.log(i);
})();

// > 2
```

^ Strange.

---

^ In this case, `i` is sensibly scoped to the inside of the for loop:

```js
(function() {
  for (let i = 0; i < 2; i++) {
    // ...
  }
  console.log(i);
})();

// ! Uncaught ReferenceError: i is not defined
```

---

^ `const` for single-assignment constants. You must define it when you declare it, and the value cannot be changed.

```js
const PHI = 1.618;
```

---

![](https://m.popkey.co/d10a8e/DyNbe.gif)

---

## Assignment Destructuring

^ **Destructuring** is a convenient way to bind values from nested data, especially when you might only care about naming variables from some of the values.

---

^ Then:

```js
var numbers = [42, Math.PI * 2];

var life = numbers[0];
var tau = numbers[1];
```

---

^ Now:

```js
const [life, ταυ] = [42, Math.PI * 2];

// life === 42
// ταυ === 6.283185
```

---

^ You can destructure objects too:

```js
const numbers = { life: 42, ταυ: Math.PI * 2 };
let { life, ταυ } = numbers;

// life === 42
// ταυ === 6.283185
```

---

![](https://m.popkey.co/76d137/5MokO.gif)

---

^ You don't have to keep the object's keys as the names either.

```js
const numbers = { life: 42, ταυ: Math.PI * 2 };
let { universe, τ } = numbers;

// universe === 42
// τ === 6.283185
```

---

## Template Literals

^ In JavaScript we delimit literal strings with `'single quotes'` or `"double quotes"`. Now we get a new type of **string literal** with <code>\`backticks\`</code>.
^ So what does this give us?

---

```
'single'
"double"

`backticks`
```

---

### String Interpolation

---

^ We can now embed data right in a string. _Very_ convenient!

```js
const q = 'questions';
const a = 'answers';

let s = `Sometimes the ${q} are complicated and the ${a} are simple.`;
```

^ The value of `s` is: `Sometimes the questions are complicated and the answers are simple.`

---

![](https://m.popkey.co/6f30a3/9y7Z6.gif)

---

^ Before this would have looked like:

```js
var q = 'questions';
var a = 'answers';

var s = 'Sometimes the ' + q + ' are complicated and the ' + a + ' are simple.';
```

---

![fit](https://m.popkey.co/2d606a/dWKyz.gif)

---

### Multiline Strings

---

```js
const l = `Unless someone like you cares a whole awful lot,
    Nothing is going to get better.
  It's not.`
```

---

^ Before, this would have either have to have include new line escape sequences:

```js
var l = 'Unless someone like you cares a whole awful lot,\n    Nothing is going to get better.\n  It\'s not.';
```

^ Notice how we didn't event need to escape the apostrophe in "It's" in the template literal.

---

^ If you wanted it on multiple lines, you've have to break it up and concatenate it back together:

```js
var l = 'Unless someone like you cares a whole awful lot,\n' +
        '    Nothing is going to get better.\n' +
        "  It's not.";
```

---

![](https://m.popkey.co/b508a9/0eNv.gif)

---

## Spread Operator (`...`)

---

^ The new **spread operator**, `...`, allows you to expand an _iterable_ value (such as an **Array** or **Object**) into a list where multiple items are expected, e.g. an **Array literal** or **function** arguments. This is similar to destructuring.

```js
let colors = ['Red', 'Blue'];
let words = ['One', 'Two', ...colors];
```

^ The value of `words` here will be: `['One', 'Two', 'Red', 'Blue']`.

---

^ Now, using `...` expand our array into **function** arguments:

```js
function fish() {
  for (var i = 0; i < arguments.length; i++) {
    console.log(arguments[i], 'fish.');
  }
}

fish(...words);
```

^ This results in printing:

```js
// > One fish.
// > Two fish.
// > Red fish.
// > Blue fish.
```
---

![](https://m.popkey.co/ea0b80/0m7br.gif)

---

^ This a great alternative to using `Function.prototype.apply()`, which would look like:

```js
fish.apply(null, words);
```

---

![](https://m.popkey.co/1f5107/JLAd9.gif)

---

## Arrow Functions

---

^ In ES2015 we have a new syntax for defining **anonymous functions**:

```js
const numbers = [42, 665];

numbers.map((n) => {
  return n * ταυ;
});
```
---

^ The curly braces are even optional for single line functions!

```js
numbers.map(n => n * ταυ);
```

^ Checkout the implicit return!

---

^ Using our previous example again, in JavaScript we can define a **function** without a name, and use it as a callback like this:

```js
function fish(words) {
  this.subject = 'fish.';

  words.forEach(function (word) {
    console.log(word, this.subject);
  }.bind(this));
}
```

---

^ Notice how we have to handle `this` and bind it to the **anonymous function**. Let's refactor it with the new syntax to look like this:

```js
function fish(words) {
  this.subject = 'fish.';
  words.forEach((word) => console.log(word, this.subject));
}
```

^ _Woah_... Right?

---

![](https://m.popkey.co/2acfaa/qxXob.gif)

^ The new arrow function syntax preserves the binding of `this` to the lexical scope where the function is defined. This can _great_ simplify a lot of the code we write everyday. I know we could also pass this as a second argument to `forEach`, but this is a contrived example, why are we even using `this` at all, _am I right_?

---

## Default Parameter Values

^ We can specify default values for function parameters in now.

---

^ Before, we might have some code like this:

```js
function increase(number, increment) {
  increment = increment || 1;
  return number + increment;
}

increase(41, 624); // 665
increase(41);      // 42
```

^ If we didn't guard for `increment` in the first line of that **function** it would be a problem for us, when it's value was `undefined`, since we only passed one argument in the second call.

---

^ Let's look at that refactored with a default value for the second parameter:

```js
function increase(number, increment = 1) {
  return number + increment;
}

increase(41, 624); // 665
increase(41);      // 42
```

^ Much cleaner _and_ clearer! Welcome to the 21st Century JavaScript!

---

## Rest Parameters (...)

^ Related to default parameters, and similar using the **spread operator** (`...`) to expand an **Array** when call a **function**, we can also use `...` to give a **function** a variable number of arguments.

---

```js
const feed = (monster, ...numnums) {
  nomnoms.forEach((nom) => monster.eat(nom));
};
```

---

^ Without rest parameters, in ES5, it would look like:

```js
function feed(monster) {
  var nomnoms = Array.prototype.slice.call(arguments, feed.length);
  nomnoms.forEach(function (nom) {
    monster.eat(nom);
  });
};
```

^ _Yeesh_. Which one do you prefer?

---

## New String APIs

^ In ES2015, we also get a ton of convenience functions added to the built in classes, er... **function prototypes**. For example, but not limited to:

---

Including, but not limited to:

- `String.prototype.startsWith()`
- `String.prototype.endsWith()`
- `String.prototype.contains()`
- `String.prototype.repeat()`
- `String.prototype.normalize()`

---

## New Array APIs

---

Including, but not limited to:

- `Array.prototype.find()`
- `Array.prototype.findIndex()`
- `Array.prototype.fill()`
- `Array.prototype.includes()` (ES2016)

---

### `Array.from()`

^ In JavaScript's built-in classes, and in the **DOM** API, there are a number of objects that are _**Array**-like_. For example, when we look for elements in an HTML page, we get back a `NodeList` which has a `length` property and can be indexed like an array, but we can't use enumeration functions like `Array.prototype.forEach` or even `for`..`in` loops.

---

```js
  let inputs = document.querySelectorAll('form input');
  for (var i = 0; i < inputs.length; i++) {
    inputs[i].disable = true;
  }
```

---

^ Let's use `Array.from()`:

```js
  let inputs = document.querySelectorAll('form input');
  Array.from(inputs).forEach((el) => el.disable = true);
```

^ **Nice!**

---

![](https://m.popkey.co/8accb0/g3mzZ.gif)

---

### `Array.of()`

^ Let's say we want to make an **Array** with some data, but we don't know if it's already an **Array** or some other scalar value.

---

^ `data` is an array:

```js
let data = [42, 665];
let copy = new Array(...data);

copy // [42, 665]
```

---

^ `data` is a scalar value:

```js
let data = 42;
let copy = new Array(...data);

copy // []
```

---

![](https://m.popkey.co/038905/3RLZb.gif)

^ _Wat_? The API for **Array** constructor is different with just a single argument.

---

^ Let's use `Array.of` instead!

```js
let data = 42;
let copy = Array.of(...data);

copy // [42]
```

^ Yay!

---

## Binary and Octal Literal Notation

---

^ We already had **hexadecimal** (`0x`) notation:

```js
console.log(0x10, 0x2A);
// > 16 42
```

---

^ Now we can do **binary** (`0b`) and **octal** (`0o`) notation as well!

```js
console.log(0b10, 0b101010);
// > 2 42
```

```js
console.log(0o10, 0o52);
// > 8 42
```

---

## Object Literals

^ In the same vein as **destructuring** and the **spread operator** we've already talked about there are some enhancements to the syntax for **Object literals**:

---

```js
let data = '.uǝɹpןıɥɔ ǝʇǝןosqo ǝɹɐ sʇןnpɐ';
let msg = { id: 42, data }
```

^ That results in an **Object** that looks like:

```js
{ id: 42, data: '.uǝɹpןıɥɔ ǝʇǝןosqo ǝɹɐ sʇןnpɐ' }
```

---

^ We can use this shorthand for functions too!

```js
let msg = {
  id: 42,
  data,
  read() {
    this.data.flip()
  }
}
```

---

## Classes

^ In JavaScript, classes are really just "special" functions and we use a prototype-based inheritance to extend their behaviors. In ES2016 we get some new syntactic sugar around describing these that more closely resembles an Object-oriented approach.

---

^ Here's a quick example:

```js

class Member extends Person {

  constructor(givenName, familyName, rank = 1) {
    super();
    this.rank = rank;
  }

  promote() {
    this.rank++;
  }

  get displayName() {
    return `${this.givenName} ${this.familyName} (${'*'.repeat(rank)})`;
  }
}

let member = new Member('Jason', 'Perry');

member.promote();
console.log(member.displayName);
// > "Jason Perry (**)"

```

---

## Modules

^ If you've used **AMD** or **Common.js** modules before with **Browserify**, **require.js**, etc. you might be happy to know ES2015 standardizes a module syntax. It's not currently supported in any browser so you'll still need to use some thing to bundle up your modules, e.g. **Webpack** or **Browserify**.

---

```js
import React from 'react';

const App = React.createClass({
  propTypes: {
    title: React.PropTypes.string
  },
  // ...
});

export default App;
```

---

^ You can also import only parts of a namespace and export several values:

```js
import { Component, PropTypes } from 'react';

class App extends Component {
  static propTypes = {
    title: PropTypes.string
  }
  // ...
}

class Menu extends Component {
  // ...
}

export { App, Menu };
```

```js
import ReactDOM from 'react-dom';
import { App } from './components';

ReactDom.render(App, document.findElementById('root'));
```

---

# [fit] Making Use of ES2015, in, er... 2016.

![](https://m.popkey.co/0f2f27/XggDo.gif)

---

## [fit] Current Browser Support

^ Current browser support is not really where we want it to be. Most of the things we've talked about aren't in yet, and even where they are it's only in the latest browsers and there's still a ton of users out there who haven't updated their browsers in years. _**Why**???_

---

## Transpilers

^ Fortunately, we still have a way we can use these features in today's browser environments. Using **polyfills** and **transpilled** code, we can write the code that _we_ want to write, and generate current generation ES5 code that will run in the user's browser client.

---

^ Some examples of Transpilers that handle some ES2015 and ES2016 features:

- Babel
- Traceur
- TypeScript
- CoffeeScript
- JSX Transformer

---

## Babel

^ We're going to primarily talk about **Babel**, as the other options are either less-complete or of a more niche purpose than we need for general web development.

---

^ Babel can be install through `npm`:

```sh
npm install -g babel-cli
```

---

^ Babel's command line interface has two primary commands we might want to use. The `babel` command itself is used to generate ES2015 javascript files from given input files:

```sh
babel index.js -o public/main.js
```

^ You'd most likely configure this to be part of your build process, either with npm scripts or something like **Gulp** or **Webpack**.

---

^ You can also use `babel-node` to run a script in **node.js** and have it transpile and execute on-the-fly. It's important to note that while this is great in development, it's really to slow to be using in a production environment.

```sh
babel-node --presets es2015 app.js
```

^ Oh _shoot_, what's that `presets` thing there?

---

### Configuring Babel 6

^ Out of the box, Babel transpiles _nothing_. You need to tell it which features you want to include. Every feature of ES6 is packaged up into separate plugins, and published as libraries on **npm**. Conveniently thought, the fine folks at Babel have packaged up common "presets" for us that we can use. The official presets include `es2015`, `react` (with JSX transformation), and a number of `stage-n` presets that reflect features at various stages of adoption for ES2016. You need to have the relevant npm packages installed, such as: `babel-preset-es2015`. You don't have to list them all on the command line. Babel will look for a `.babelrc` configuration file. Here's an example I used on a recent project:

---

```JSON
{
  "presets": ["es2015", "react", "stage-0"],
  "env": {
    "development": {
      "plugins": [
        ["react-transform", {
          "transforms": [{
            "transform": "react-transform-hmr",
            "imports": ["react"],
            "locals": ["module"]
          }]
        }]
      ]
    }
  }
}
```

^ As you can see, I'm using `es2015`, `react` and `stage-0` to get the most bleeding edge JavaScript features. I've also enabled a plugin that gives me Hot Module Reloading for my React components. This lets code changes I make get reloading in the browser without a full page refresh. [It's an amazing way to work](https://vimeo.com/36579366), but that's a topic for another day!

---

![](https://m.popkey.co/4a21e4/rzXL3.gif)

---

# What didn't we cover?

![](https://m.popkey.co/eba5fc/bgWxr.gif)

^ There are some things I've skipped in this tutorial either because they were minor, or their complexity was outside the scope of the audience I've intended:

---

- `for`...`of` iteration
- **Promise**
- **Symbol**
- **Map** & **Set** Collections
- Comprehensions
- Module loaders
- Proxy & Reflection APIs
- Subclassable Built-ins
- `async`/`await` (ES2016)
- Generators (ES2016)
- Decorators (ES2016)
- Better Unicode support
- New **Math** & **Number** APIs

---

# Resources

- http://exploringjs.com
- https://babeljs.io/docs/learn-es2015/
- https://nodejs.org/en/docs/es6/
- http://kangax.github.io/compat-table
- http://www.2ality.com/2015/04/numbers-math-es6.html

---

![inline fit](SDG-Logo.png)

### @ambethia

---

![](https://m.popkey.co/55014f/oGKbJ.gif)
