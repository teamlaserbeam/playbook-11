# `JavaScript styleguide`

Some rules to follow when writing JavaScript for AMARO projects.

## Introduction

- Remember: **code like it's 2020**.
- We use the ES2015 syntax.
- We follow Airbnb's styleguide.
- Examples use ES2015 syntax when applicable.
- Want to learn more JavaScript? Please!

## Logs

- We encourage you to log important app events and changes in development mode.
- Only errors should be shown in production to make it easier to debug.
- Use the correct console method to log information. It makes it easier to find the correct log message.

        console.log('A normal message');
        console.warn('A warning message');
        console.error('An error message');
        console.info('Some relevant information');

## General definitions

- Do not use the single `var` definition.
- Always define each variable in a new line.
- Variables names should always be in :camel: `camelCase`.
- Do **not** follow "comma first" style.

        const companyName = 'AMARO';
        let coffeeCup = 999;

## `const`

- Use `const` for all of your references. Avoid using `var`.
- **eslint:** [`prefer-const`](http://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](http://eslint.org/docs/rules/no-const-assign.html)

> Why? This ensures that you can't reassign you references, which can lead to bugs and difficult to comprehend code.

        const a = 1;
        const b = 2;

## `let`

- If you must reassign references, use `let` instead of `var`.
- **eslint:** [`no-var`](http://eslint.org/docs/rules/no-var.html)
- **jscs:** [`no-const-assign`](http://jscs.info/rule/disallowVar)

> Why? `let` is block-scoped rather than function-scope like `var`

        let count = 1;
        if (true) {
          count += 1;
        }

### Block-scope

- Note that both `const` and `let` are block-scoped.

        // const and let only exist in the blocks they are defined in.
        {
          let a = 1;
          const b = 1;
        }
        console.log(a); // ReferenceError
        console.log(b); // ReferenceError

## Objects

### Literal syntax

- Use the literal syntax for object creation.
- **eslint:** [`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)

        // bad
        const item = new Object();

        // good
        const item = {};

### Reserved words

- Don't use [reserved words](http://es5.github.io/#x7.6.1) as keys.
- Use readable synonyms in place of reserved words.
- **jscs:** [`disallowIdentifierNames`](http://jscs.info/rule/disallowIdentifierNames)

        // bad
        const superman = {
          default: { clark: 'kent' },
          class: 'alien',
          private: true,
        };

        // good
        const superman = {
          defaults: { clark: 'kent' },
          type: 'alien', // Don't use clas; klas; klass.
          hidden: true,
        };

### Computed property names

- Use computed property names when creating objects with dynamic property names.

> Why? They allow you to define all the properties of an object in one place.

        function getKey(k) {
          return `a key named ${k}`;
        }

        // bad
        const obj = {
          id: 5,
          name: 'San Francisco',
        };
        obj[getKey('enabled')] = true;

        // good
        const obj = {
          id: 5,
          name: 'San Francisco',
          [getKey('enabled')]: true,
        };

### Object method shorthand

- Use object method shorthand.
- **eslint:** [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html)
- **jscs:** [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

        // bad
        const atom = {
          value: 1,

          addValue: function (value) {
            return atom.value + value;
          },
        };

        // good
        const atom = {
          value: 1,

          addValue(value) {
            return atom.value + value;
          },
        };

### Property value shorthand

- Use property value shorthand.
- **eslint:** [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html)
- **jscs:** [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

> Why? It is shorter to write and descriptive.

        const lukeSkywalker = 'Luke Skywalker';

        // bad
        const obj = {
          lukeSkywalker: lukeSkywalker,
        };

        // good
        const obj = {
          lukeSkywalker,
        };

### Group shorthand properties

- Group your shorthand properties at the beginning of your object declaration.

> Why? It's easier to tell which properties are using the shorthand.

        const anakinSkywalker = 'Anakin Skywalker';
        const lukeSkywalker = 'Luke Skywalker';

        // bad
        const obj = {
          episodeOne: 1,
          twoJediWalkIntoACantina: 2,
          lukeSkywalker,
          episodeThree: 3,
          mayTheFourth: 4,
          anakinSkywalker,
        };

        // good
        const obj = {
          lukeSkywalker,
          anakinSkywalker,
          episodeOne: 1,
          twoJediWalkIntoACantina: 2,
          episodeThree: 3,
          mayTheFourth: 4,
        };

### Quotes

- Only quote properties that are invalid identifiers.
- **eslint:** [`quote-props`](http://eslint.org/docs/rules/quote-props.html)
- **jscs:** [`disallowQuotedKeysInObjects`](http://jscs.info/rule/disallowQuotedKeysInObjects)

> Why? In general we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engineers.

        // bad
        const bad = {
          'foo': 3,
          'bar': 4,
          'data-blah': 5,
        };

        // good
        const good = {
          foo: 3,
          bar: 4,
          'data-blah': 5,
        };

## Arrays

### Literal syntax

- Use the literal syntax for array creation.
- **eslint:** [`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor.html)

        // bad
        const items = new Array();

        // good
        const items = [];

### Use `Array.push()`

- Use [`Array.push()`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) instead of direct assignment to add items to an array.

        const someStack = [];

        // bad
        someStack[someStack.length] = 'abracadabra';

        // good
        someStack.push('abracadabra');

### Use spreads

- Use array spreads `...` to copy arrays.

        // bad
        const len = items.length;
        const itemsCopy = [];
        let i;

        for (i = 0; i < len; i++) {
          itemsCopy[i] = items[i];
        }

        // good
        const itemsCopy = [...items];

### Use `Array.from()`

- Use [`Array.from()`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) to convert an array-like object to an array.

        const foo = document.querySelectorAll('.foo');
        const nodes = Array.from(foo);

### Use return statements

- Use return statements in array method callbacks.
- It's ok to omit the return if the function body consists of a single statement.
- **eslint:** [`array-callback-return`](http://eslint.org/docs/rules/array-callback-return)

        // good
        [1, 2, 3].map((x) => {
          const y = x + 1;
          return x * y;
        });

        // good
        [1, 2, 3].map(x => x + 1);

        // bad
        const flat = {};
        [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
          const flatten = memo.concat(item);
          flat[index] = flatten;
        });

        // good
        const flat = {};
        [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
          const flatten = memo.concat(item);
          flat[index] = flatten;
          return flatten;
        });

        // bad
        inbox.filter((msg) => {
          const { subject, author } = msg;
          if (subject === 'Mockingbird') {
            return author === 'Harper Lee';
          } else {
            return false;
          }
        });

        // good
        inbox.filter((msg) => {
          const { subject, author } = msg;
          if (subject === 'Mockingbird') {
            return author === 'Harper Lee';
          }

          return false;
        });

## Destructuring

### Object destructuring

- Use object destructuring when accessign and using multiple properties of an object.
- **jscs:** [`requireObjectDestructuring`](http://jscs.info/rule/requireObjectDestructuring)

> Why? Destructuring saves you from creating temporary references for those properties.

        // bad
        function getFullName(user) {
          const firstName = user.firstName;
          const lastName = user.lastName;

          return `${firstName} ${lastName}`;
        }

        // good
        function getFullName(user) {
          const { firstName, lastName } = user;
          return `${firstName} ${lastName}`;
        }

        // best
        function getFullName({ firstName, lastName }) {
          return `${firstName} ${lastName}`;
        }

### Array destructuring

- Use array destructuring.
- **jscs:** [`requireArrayDestructuring`](http://jscs.info/rule/requireArrayDestructuring)

        const arr = [1, 2, 3, 4];

        // bad
        const first = arr[0];
        const second = arr[1];

        // good
        const [first, second] = arr;

### Use object destructuring

- Use object destructuring for multiple return values, not array destructuring.
- **jscs:** [`disallowArrayDestructuringReturn`](http://jscs.info/rule/disallowArrayDestructuringReturn)

> Why? You can add new properties over time or change the order of things without breaking call sites.

        // bad
        function processInput(input) {
          // then a miracle occurs
          return [left, right, top, bottom];
        }

        // the caller needs to think about the order of return data
        const [left, __ , top] = processInput(input);

        // good
        function processInput(input) {
          // then a miracle occurs
          return { left, right, top, bottom };
        }

        // the caller selects only the data they need
        const { left, top } = processInput(input);

## Strings

### Quotes

- Use single quotes `'` for strings.
- **eslint:** [`quotes`](http://eslint.org/docs/rules/quotes.html)
- **jscs:** [`validateQuoteMarks`](http://jscs.info/rule/validateQuoteMarks)

        // bad
        const name = "Capt. Janeway";

        // good
        const name = 'Capt. Janeway';

### Line size

- Strings that cause the line to go over 100 characters should be written across multiple lines using string concatenation.
- **NOTE:** If overused, long strings with concatenation could impact performance.[jsPerf](http://jsperf.com/ya-string-concat), [discussion](https://github.com/airbnb/javascript/issues/40)

        // bad
        const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

        // bad
        const errorMessage = 'This is a super long error that was thrown because \
        of Batman. When you stop to think about how Batman had anything to do \
        with this, you would get nowhere \
        fast.';

        // good
        const errorMessage = 'This is a super long error that was thrown because ' +
          'of Batman. When you stop to think about how Batman had anything to do ' +
          'with this, you would get nowhere fast.';

### Use template strings

- When programmatically building up strings, use template strings instead of concatenation.
- **Never** use `eval()` on a string, it opens too many vulnerabilities.
- **eslint:** [`prefer-template`](http://eslint.org/docs/rules/prefer-template.html), [`template-curly-spacing`](http://eslint.org/docs/rules/template-curly-spacing)
- **jscs:** [`requireTemplateStrings`](http://jscs.info/rule/requireTemplateStrings)

> Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

        // bad
        function sayHi(name) {
          return 'How are you, ' + name + '?';
        }

        // bad
        function sayHi(name) {
          return ['How are you, ', name, '?'].join();
        }

        // bad
        function sayHi(name) {
          return `How are you, ${ name }?`;
        }

        // good
        function sayHi(name) {
          return `How are you, ${name}?`;
        }

### Unnecessary escape

- Do not unnecessarily escape characters in strings.
- **eslint:** [`no-useless-escape`](http://eslint.org/docs/rules/no-useless-escape)

> Why? Backslashes harm readability, thus they should only be present when necessary.

        // bad
        const foo = '\'this\' \i\s \"quoted\"';

        // good
        const foo = '\'this\' is "quoted"';
        const foo = `'this' is "quoted"`;

## Functions

- Use function declarations instead of function expressions.
- **jscs:** [`requireFunctionDeclarations`](http://jscs.info/rule/requireFunctionDeclarations)

> Why? Function declarations are named, so they're easier to identify in call stacks. Also, the whole body of a function declaration is hoisted, whereas only the reference of a function expression is hoisted. This rule makes it possible to always use Arrow Functions in place of function expressions.

        // bad
        const foo = function () {
        };

        // good
        function foo() {
        }

### IIFE

- Wrap immediately invoked function expressions in parentheses.
- **eslint:** [`wrap-iife`](http://eslint.org/docs/rules/wrap-iife.html)
- **jscs:** [`requireParenthesesAroundIIFE`](http://jscs.info/rule/requireParenthesesAroundIIFE)

> Why? An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.

        // immediately-invoked function expression (IIFE)
        (function () {
          console.log('Welcome to the Internet. Please follow me.');
        }());

### Function declaration

- Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead.
- Browsers will allow you to do it, but they all interpret it differently, which is bad news.
- **eslint:** [`no-loop-func`](http://eslint.org/docs/rules/no-loop-func.html)

        // bad
        if (currentUser) {
          function test() {
            console.log('Nope.');
          }
        }

        // good
        let test;
        if (currentUser) {
          test = () => {
            console.log('Yup.');
          };
        }

### Arguments

- Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

        // bad
        function nope(name, options, arguments) {
          // ...stuff...
        }

        // good
        function yup(name, options, args) {
          // ...stuff...
        }

- Never use `arguments`, opt to use rest syntax `...` instead.
- **eslint:** [`prefer-rest-params`](http://eslint.org/docs/rules/prefer-rest-params)

> Why? `...` is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like `arguments`.

        // bad
        function concatenateAll() {
          const args = Array.prototype.slice.call(arguments);
          return args.join('');
        }

        // good
        function concatenateAll(...args) {
          return args.join('');
        }

### Parameters

- Use default parameter syntax rather than mutating function arguments.

        // really bad
        function handleThings(opts) {
          // No! We shouldn't mutate function arguments.
          // Double bad: if opts is falsy it'll be set to an object which may
          // be what you want but it can introduce subtle bugs.
          opts = opts || {};
          // ...
        }

        // still bad
        function handleThings(opts) {
          if (opts === void 0) {
            opts = {};
          }
          // ...
        }

        // good
        function handleThings(opts = {}) {
          // ...
        }

### Default parameters

- Avoid side effects with default parameters.

> Why? They are confusing to reason about.

        var b = 1;
        // bad
        function count(a = b++) {
          console.log(a);
        }
        count();  // 1
        count();  // 2
        count(3); // 3
        count();  // 3

- Always put default parameters last.

        // bad
        function handleThings(opts = {}, name) {
          // ...
        }

        // good
        function handleThings(name, opts = {}) {
          // ...
        }

### Creating Functions

- Never use the Function constructor to create a new function.

> Why? Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.

        // bad
        var add = new Function('a', 'b', 'return a + b');

        // still bad
        var subtract = Function('a', 'b', 'return a - b');

### Spacing

- Spacing in a function signature.

> Why? Consistency is good, and you shouldn't have to add or remove a space when adding or removing a name.

        // bad
        const f = function(){};
        const g = function (){};
        const h = function() {};

        // good
        const x = function () {};
        const y = function a() {};

### Immutable parameters

- Never mutate or reassign parameters.
- **eslint:** [`no-param-reassign`](http://eslint.org/docs/rules/no-param-reassign.html)

> Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

> Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

        // bad
        function f1(obj) {
          obj.key = 1;
        };

        // good
        function f2(obj) {
          const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
        };

## Arrow functions

- When you must use function expressions (as when passing an anonymous function), use arrow function notation.
- **eslint:** [`prefer-arrow-callback`](http://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](http://eslint.org/docs/rules/arrow-spacing.html)
- **jscs:** [`requireArrowFunctions`](http://jscs.info/rule/requireArrowFunctions)

> Why? It creates a version of the function that executes in the context of this, which is usually what you want, and is a more concise syntax.

> Why not? If you have a fairly complicated function, you might move that logic out into its own function declaration.

        // bad
        [1, 2, 3].map(function (x) {
          const y = x + 1;
          return x * y;
        });

        // good
        [1, 2, 3].map((x) => {
          const y = x + 1;
          return x * y;
        });

- If the function body consists of a single expression, omit the braces and use the implicit return.
- Otherwise, keep the braces and use a `return` statement.
- **eslint:** [`arrow-parens`](http://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](http://eslint.org/docs/rules/arrow-body-style.html)
- **jscs:** [`disallowParenthesesAroundArrowParam`](http://jscs.info/rule/disallowParenthesesAroundArrowParam), [`requireShorthandArrowFunctions`](http://jscs.info/rule/requireShorthandArrowFunctions)

> Why? Syntactic sugar. It reads well when multiple functions are chained together.

        // bad
        [1, 2, 3].map(number => {
          const nextNumber = number + 1;
          `A string containing the ${nextNumber}.`;
        });

        // good
        [1, 2, 3].map(number => `A string containing the ${number}.`);

        // good
        [1, 2, 3].map((number, index) => ({
          index: number
        }));

- In case the expression spans over multiple lines, wrap it in parentheses for better readability.

> Why? It shows clearly where the function starts and ends.

        // bad
        [1, 2, 3].map(number => 'As time went by, the string containing the ' +
          `${number} became much longer. So we needed to break it over multiple ` +
          'lines.'
        );

        // good
        [1, 2, 3].map(number => (
          `As time went by, the string containing the ${number} became much ` +
          'longer. So we needed to break it over multiple lines.'
        ));

- If your function takes a single argument and doesn’t use braces, omit the parentheses.
- Otherwise, always include parentheses around arguments
- **eslint:** [`arrow-parens`](http://eslint.org/docs/rules/arrow-parens.html)
- **jscs:** [`disallowParenthesesAroundArrowParam`](http://jscs.info/rule/disallowParenthesesAroundArrowParam)

        // bad
        [1, 2, 3].map((x) => x * x);

        // good
        [1, 2, 3].map(x => x * x);

        // bad
        [1, 2, 3].map(x => {
          const y = x + 1;
          return x * y;
        });

        // good
        [1, 2, 3].map((x) => {
          const y = x + 1;
          return x * y;
        });

- Avoid confusing arrow function syntax (`=>`) with comparison operators (`<=`, `>=`).
- **eslint:** [`no-confusing-arrow`](http://eslint.org/docs/rules/no-confusing-arrow)

        // bad
        const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

        // bad
        const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;

        // good
        const itemHeight = (item) => { return item.height > 256 ? item.largeSize : item.smallSize; };

## Classes & Constructors

- Always use `class`. Avoid manipulating `prototype` directly.

> Why? `class` syntax is more concise and easier to reason about.

        // bad
        function Queue(contents = []) {
          this.queue = [...contents];
        }
        Queue.prototype.pop = function () {
          const value = this.queue[0];
          this.queue.splice(0, 1);
          return value;
        };

        // good
        class Queue {
          constructor(contents = []) {
            this.queue = [...contents];
          }
          pop() {
            const value = this.queue[0];
            this.queue.splice(0, 1);
            return value;
          }
        }

- Use `extends` for inheritance

> Why? It is a built-in way to inherit prototype functionality without breaking `instanceof`.

        // bad
        const inherits = require('inherits');
        function PeekableQueue(contents) {
          Queue.apply(this, contents);
        }
        inherits(PeekableQueue, Queue);
        PeekableQueue.prototype.peek = function () {
          return `this._queue[0];`
        }

        // good
        class PeekableQueue extends Queue {
          peek() {
            return `this._queue[0];`
          }
        }

- Methods can return `this` to help with method chaining.

        // bad
        Jedi.prototype.jump = function () {
          this.jumping = true;
          return true;
        };

        Jedi.prototype.setHeight = function (height) {
          this.height = height;
        };

        const luke = new Jedi();
        luke.jump(); // => true
        luke.setHeight(20); // => undefined

        // good
        class Jedi {
          jump() {
            this.jumping = true;
            return this;
          }

          setHeight(height) {
            this.height = height;
            return this;
          }
        }

        const luke = new Jedi();

        luke
          .jump()
          .setHeight(20);

- It's okay to write a custom `toString()` method, just make sure it works successfully and causes no side effects.

        class Jedi {
          constructor(options = {}) {
            this.name = options.name || 'no name';
          }

          getName() {
            return this.name;
          }

          toString() {
            return `Jedi - ${this.getName()}`;
          }
        }

- Classes have a default constructor if one is not specified. An empy constructor function or one that just delegates to a parent class is unnecessary.
- **eslint:** [`no-useless-constructor`](http://eslint.org/docs/rules/no-useless-constructor)

        // bad
        class Jedi {
          constructor() {}

          getName() {
            return this.name;
          }
        }

        // bad
        class Rey extends Jedi {
          constructor(...args) {
            super(...args);
          }
        }

        // good
        class Rey extends Jedi {
          constructor(...args) {
            super(...args);
            this.name = 'Rey';
          }
        }

- Avoid duplicate class members.
- **eslint:** [`no-dupe-class-members`](http://eslint.org/docs/rules/no-dupe-class-members)

> Why? Duplicate class member declarations will silently prefer the last one - having duplicates is almost certainly a bug.

        // bad
        class Foo {
          bar() { return 1; }
          bar() { return 2; }
        }

        // good
        class Foo {
          bar() { return 1; }
        }

        // good
        class Foo {
          bar() { return 2; }
        }

## Modules

- Always use modules(`import`/`export`) over a non-standard module system.

> Why? Modules are the future, let's start using the future now.

        // bad
        const AirbnbStyleGuide = require('./AirbnbStyleGuide');
        module.exports = AirbnbStyleGuide.es6;

        // ok
        import AirbnbStyleGuide from './AirbnbStyleGuide';
        export default AirbnbStyleGuide.es6;

        // best
        import { es6 } from './AirbnbStyleGuide';
        export default es6;

- Do **not** use wildcard imports.

> Why? This makes sure you have a single default export.

        // bad
        import * as AirbnbStyleGuide from './AirbnbStyleGuide';

        // good
        import AirbnbStyleGuide from './AirbnbStyleGuide';

- Do **not** export directly from an import.

> Why? Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.

        // bad
        // filename es6.js
        export { es6 as default } from './airbnbStyleGuide';

        // good
        // filename es6.js
        import { es6 } from './AirbnbStyleGuide';
        export default es6;

- Only import from a path in one place.
- **eslint:** [`no-duplicate-imports`](http://eslint.org/docs/rules/no-duplicate-imports)

> Why? Having multiple lines that import from the same path can make code harder to maintain.

        // bad
        import foo from 'foo';
        // … some other imports … //
        import { named1, named2 } from 'foo';

        // good
        import foo, { named1, named2 } from 'foo';

        // good
        import foo, {
          named1,
          named2,
        } from 'foo';

- Do **not** export mutable bindings.
- **eslint:** [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)

> Why? Mutation should be avoided in general, but in particular when exporting mutable bindings. While this technique may be needed for some special cases, in general, only constant references should be exported.

        // bad
        let foo = 3;
        export { foo }

        // good
        const foo = 3;
        export { foo }

- In modules with a single export, prefer default export over named export.
- **eslint:** [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)

        // bad
        export function foo() {}

        // good
        export default function foo() {}

- Put all `import`s above non-import statements
- **eslint:** [`import/imposts-first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/imports-first.md)

> Why? Since `import`s are hoisted, keeping them all at the top prevents surprising behavior.

        // bad
        import foo from 'foo';
        foo.init();

        import bar from 'bar';

        // good
        import foo from 'foo';
        import bar from 'bar';

        foo.init();

## Iterators and Generators

### Iterators

- Don't use iterators. Prefer JavaScript´s higher-order functions like `map()` and `reduce()` instead of loops like `for-of`.
- **eslint:** [`no-iterator`](http://eslint.org/docs/rules/no-iterator.html)

> Why? This enforces our immutable rule. Dealing with pure functions that return values is easier to reason about than side effects.

        const numbers = [1, 2, 3, 4, 5];

        // bad
        let sum = 0;
        for (let num of numbers) {
          sum += num;
        }

        sum === 15;

        // good
        let sum = 0;
        numbers.forEach(num => sum += num);
        sum === 15;

        // best (use the functional force)
        const sum = numbers.reduce((total, num) => total + num, 0);
        sum === 15;

### Generators

- Don't use generators for now.

> Why? They don't transpile well to ES5.

- If you must use generators, or if you disregard [our advice](https://github.com/airbnb/javascript#generators--nope), make sure their function signature is spaced properly.
- **eslint:** [`generator-star-spacing`](http://eslint.org/docs/rules/generator-star-spacing)

> Why? function and * are part of the same conceptual keyword - * is not a modifier for function, function* is a unique construct, different from function.

        // bad
        function * foo() {
        }

        const bar = function * () {
        }

        const baz = function *() {
        }

        const quux = function*() {
        }

        function*foo() {
        }

        function *foo() {
        }

        // very bad
        function
        *
        foo() {
        }

        const wat = function
        *
        () {
        }

        // good
        function* foo() {
        }

        const foo = function* () {
        }

## Properties

- Use dot notation when accessing properties.
- **eslint:** [`dot-notation`](http://eslint.org/docs/rules/dot-notation.html)
- **jscs:** [`requireDotNotation`](http://jscs.info/rule/requireDotNotation)

        const luke = {
          jedi: true,
          age: 28,
        };

        // bad
        const isJedi = luke['jedi'];

        // good
        const isJedi = luke.jedi;

- Use bracket notation `[]` when accessing properties with a variable.

        const luke = {
          jedi: true,
          age: 28,
        };

        function getProp(prop) {
          return luke[prop];
        }

        const isJedi = getProp('jedi');

## Variables

- Always use `const` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that.

        // bad
        superPower = new SuperPower();

        // good
        const superPower = new SuperPower();

- Use one `const` declaration per variable.
- **eslint:** [`one-var`](http://eslint.org/docs/rules/one-var.html)
- **jscs:** [`disallowMultipleVarDecl`](http://jscs.info/rule/disallowMultipleVarDecl)

> Why? It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs. You can also step through each declaration with the debugger, instead of jumping through all of them at once.

        // bad
        const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

        // bad
        // (compare to above, and try to spot the mistake)
        const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

        // good
        const items = getItems();
        const goSportsTeam = true;
        const dragonball = 'z';

- Group all your `const`s and then group all your `let`s

> Why? This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

        // bad
        let i, len, dragonball,
          items = getItems(),
          goSportsTeam = true;

        // bad
        let i;
        const items = getItems();
        let dragonball;
        const goSportsTeam = true;
        let len;

        // good
        const goSportsTeam = true;
        const items = getItems();
        let dragonball;
        let i;
        let length;

- Assign variables where you need them, but place them in a reasonable place.

> Why? `let` and `const` are block scoped and not function scoped.

        // bad - unnecessary function call
        function checkName(hasName) {
          const name = getName();

          if (hasName === 'test') {
            return false;
          }

          if (name === 'test') {
            this.setName('');
            return false;
          }

          return name;
        }

        // good
        function checkName(hasName) {
          if (hasName === 'test') {
            return false;
          }

          const name = getName();

          if (name === 'test') {
            this.setName('');
            return false;
          }

          return name;
        }

## Hoisting

- `var` declarations get hoisted to the top of their scope, their assignment does not.
- `const` and `let` declarations are blessed with a new concept called [Temporal Dead Zones (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let).
-  It's important to know why [typeof is no longer safe](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).

        // we know this wouldn't work (assuming there
        // is no notDefined global variable)
        function example() {
          console.log(notDefined); // => throws a ReferenceError
        }

        // creating a variable declaration after you
        // reference the variable will work due to
        // variable hoisting. Note: the assignment
        // value of `true` is not hoisted.
        function example() {
          console.log(declaredButNotAssigned); // => undefined
          var declaredButNotAssigned = true;
        }

        // the interpreter is hoisting the variable
        // declaration to the top of the scope,
        // which means our example could be rewritten as:
        function example() {
          let declaredButNotAssigned;
          console.log(declaredButNotAssigned); // => undefined
          declaredButNotAssigned = true;
        }

        // using const and let
        function example() {
          console.log(declaredButNotAssigned); // => throws a ReferenceError
          console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
          const declaredButNotAssigned = true;
        }

- Anonymous function expressions hoist their variable name, but not the function assignment.

        function example() {
          console.log(anonymous); // => undefined

          anonymous(); // => TypeError anonymous is not a function

          var anonymous = function () {
            console.log('anonymous function expression');
          };
        }

- Named function expressions hoist the variable name, not the function name or the function body.

        function example() {
          console.log(named); // => undefined

          named(); // => TypeError named is not a function

          superPower(); // => ReferenceError superPower is not defined

          var named = function superPower() {
            console.log('Flying');
          };
        }

        // the same is true when the function name
        // is the same as the variable name.
        function example() {
          console.log(named); // => undefined

          named(); // => TypeError named is not a function

          var named = function named() {
            console.log('named');
          }
        }

- Function declarations hoist their name and the function body

        function example() {
          superPower(); // => Flying

          function superPower() {
            console.log('Flying');
          }
        }

- For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html) by [Ben Cherry](http://www.adequatelygood.com/).

## Comparison Operators && Equality

- Use `===` and `!==` over `==` and `!=`.
- **eslint:** [`eqeqeq`](http://eslint.org/docs/rules/eqeqeq.html)

- Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:
    - **Objects** evaluate to **true**
    - **Undefined** evaluates to **false**
    - **Null** evaluates to **false**
    - **Booleans** evaluate to **the value of the boolean**
    - **Numbers** evaluate to **false** if **+0**, **-0**, or **NaN**, otherwise **true**
    - **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

            if ([0] && []) {
              // true
              // an array (even an empty one) is an object, objects will evaluate to true
            }

- Use shortcuts.

        // bad
        if (name !== '') {
          // ...stuff...
        }

        // good
        if (name) {
          // ...stuff...
        }

        // bad
        if (collection.length > 0) {
          // ...stuff...
        }

        // good
        if (collection.length) {
          // ...stuff...
        }

- For more information see [Truth Equality and JavaScript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

- Use braces to create blocks in `case` and `default` clauses that contain lexical declarations (e.g. `let`, `const`, `function`, and `class`).
- **eslint:** [`no-case-declarations`](http://eslint.org/docs/rules/no-case-declarations.html)

> Why? Lexical declarations are visible in the entire `switch` block but only get initialized when assigned, which only happens when its `case` is reached. This causes problems when multiple `case` clauses attempt to define the same thing.

        // bad
        switch (foo) {
          case 1:
            let x = 1;
            break;
          case 2:
            const y = 2;
            break;
          case 3:
            function f() {}
            break;
          default:
            class C {}
        }

        // good
        switch (foo) {
          case 1: {
            let x = 1;
            break;
          }
          case 2: {
            const y = 2;
            break;
          }
          case 3: {
            function f() {}
            break;
          }
          case 4:
            bar();
            break;
          default: {
            class C {}
          }
        }

- Ternaries should not be nested and generally be single line expressions.
- **eslint:** [`no-nested-ternary`](http://eslint.org/docs/rules/no-nested-ternary.html)

        // bad
        const foo = maybe1 > maybe2
          ? "bar"
          : value1 > value2 ? "baz" : null;

        // better
        const maybeNull = value1 > value2 ? 'baz' : null;

        const foo = maybe1 > maybe2
          ? 'bar'
          : maybeNull;

        // best
        const maybeNull = value1 > value2 ? 'baz' : null;

        const foo = maybe1 > maybe2 ? 'bar' : maybeNull;

- Avoid unneeded ternary statements.
- **eslint:** [`no-unneeded-ternary`](http://eslint.org/docs/rules/no-unneeded-ternary.html)

        // bad
        const foo = a ? a : b;
        const bar = c ? true : false;
        const baz = c ? false : true;

        // good
        const foo = a || b;
        const bar = !!c;
        const baz = !c;

## Blocks

- Use braces with all multi-line blocks.

        // bad
        if (test)
          return false;

        // good
        if (test) return false;

        // best
        if (test) {
          return false;
        }

        // bad
        function foo() { return false; }

        // good
        function bar() {
          return false;
        }

- If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your `if` block's closing brace.
- **eslint:** [`brace-style`](http://eslint.org/docs/rules/brace-style.html)
- **jscs:** [`disallowNewlineBeforeBlockStatements`](http://jscs.info/rule/disallowNewlineBeforeBlockStatements)

        // bad
        if (test) {
          thing1();
          thing2();
        }
        else {
          thing3();
        }

        // good
        if (test) {
          thing1();
          thing2();
        } else {
          thing3();
        }

## Comments

- Use `/** ... */` for multi-line comments. Include a description, specify types and values for all parameters and return values.

        `// bad
         // make() returns a new element
         // based on the passed in tag name
         //
         // @param {String} tag
         // @return {Element} element
         function make(tag) {

           // ...stuff...

           return element;
         }

         // good
         /**
          * make() returns a new element
          * based on the passed in tag name
          *
          * @param {String} tag
          * @return {Element} element
          */
          function make(tag) {

            // ...stuff...

            return element;
          }`

- Use `//` for single line comments.
- Place single line comments on a newline above the subject of the comment.
- Put an empty line before the comment unless it's on the first line of a block.

        `// bad
        const active = true;  // is current tab

        // good
        // is current tab
        const active = true;

        // bad
        function getType() {
          console.log('fetching type...');
          // set the default type to 'no type'
          const type = this._type || 'no type';

          return type;
        }

        // good
        function getType() {
          console.log('fetching type...');

          // set the default type to 'no type'
          const type = this._type || 'no type';

          return type;
        }

        // also good
        function getType() {
          // set the default type to 'no type'
          const type = this._type || 'no type';

          return type;
        }`

- Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME: -- need to figure this out` or `TODO: -- need to implement`.

- Use `// FIXME:` to annotate problems.

        class Calculator extends Abacus {
          constructor() {
            super();

            // FIXME: shouldn't use a global here
            total = 0;
          }
        }

- Use `// TODO:` to annotate solutions to problems.

        class Calculator extends Abacus {
          constructor() {
            super();

            // TODO: total should be configurable by an options param
            this.total = 0;
          }
        }

## Whitespace

- Use soft tabs set to 2 spaces.
- **eslint:** [`indent`](http://eslint.org/docs/rules/indent.html)
- **jscs:** [`validateIndentation`](http://jscs.info/rule/validateIndentation)

        // bad
        function foo() {
        ∙∙∙∙const name;
        }

        // bad
        function bar() {
        ∙const name;
        }

        // good
        function baz() {
        ∙∙const name;
        }

- Place 1 space before the leading brace.
- **eslint:** [`space-before-blocks`](http://eslint.org/docs/rules/space-before-blocks.html)
- **jscs:** [`requireSpaceBeforeBlockStatements`](http://jscs.info/rule/requireSpaceBeforeBlockStatements)

        // bad
        function test(){
          console.log('test');
        }

        // good
        function test() {
          console.log('test');
        }

        // bad
        dog.set('attr',{
          age: '1 year',
          breed: 'Bernese Mountain Dog',
        });

        // good
        dog.set('attr', {
          age: '1 year',
          breed: 'Bernese Mountain Dog',
        });

- Place 1 space before the opening parenthesis in control statements (`if`, `while`, etc.).
- Place no space between the argument list and the function name in function calls and declarations.
- **eslint:** [`keyword-spacing`](http://eslint.org/docs/rules/keyword-spacing.html)
- **jscs:** [`requireSpaceAfterKeywords`](http://jscs.info/rule/requireSpaceAfterKeywords)

        // bad
        if(isJedi) {
          fight ();
        }

        // good
        if (isJedi) {
          fight();
        }

        // bad
        function fight () {
          console.log ('Swooosh!');
        }

        // good
        function fight() {
          console.log('Swooosh!');
        }

- Set off operators with spaces.
- **eslint:** [`space-infix-ops`](http://eslint.org/docs/rules/space-infix-ops.html)
- **jscs:** [`requireSpaceBeforeBinaryOperators`](http://jscs.info/rule/requireSpaceBeforeBinaryOperators), [`requireSpaceAfterBinaryOperators`](http://jscs.info/rule/requireSpaceAfterBinaryOperators)

        // bad
        const x=y+5;

        // good
        const x = y + 5;

- End files with a single newline character.

        // bad
        (function (global) {
          // ...stuff...
        })(this);

        // bad
        (function (global) {
          // ...stuff...
        })(this);↵
        ↵

        // good
        (function (global) {
          // ...stuff...
        })(this);↵

- Use indentation when making long method chains (more than 2 method chains).
- Use a leading dot, which emphasizes that the line is a method call, not a new statement.
- eslint: [`newline-per-chained-call`](http://eslint.org/docs/rules/newline-per-chained-call), [`no-whitespace-before-property`](http://eslint.org/docs/rules/no-whitespace-before-property)

          // bad
          $('#items').find('.selected').highlight().end().find('.open').updateCount();

          // bad
          $('#items').
            find('.selected').
              highlight().
              end().
            find('.open').
              updateCount();

          // good
          $('#items')
            .find('.selected')
              .highlight()
              .end()
            .find('.open')
              .updateCount();

          // bad
          const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
              .attr('width', (radius + margin) * 2).append('svg:g')
              .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
              .call(tron.led);

          // good
          const leds = stage.selectAll('.led')
              .data(data)
            .enter().append('svg:svg')
              .classed('led', true)
              .attr('width', (radius + margin) * 2)
            .append('svg:g')
              .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
              .call(tron.led);

          // good
          const leds = stage.selectAll('.led').data(data);

- Leave a blank line after blocks and before the next statement.
- **jscs:** [`requirePaddingNewLinesAfterBlocks`]()

        // bad
        if (foo) {
          return bar;
        }
        return baz;

        // good
        if (foo) {
          return bar;
        }

        return baz;

        // bad
        const obj = {
          foo() {
          },
          bar() {
          },
        };
        return obj;

        // good
        const obj = {
          foo() {
          },

          bar() {
          },
        };

        return obj;

        // bad
        const arr = [
          function foo() {
          },
          function bar() {
          },
        ];
        return arr;

        // good
        const arr = [
          function foo() {
          },

          function bar() {
          },
        ];

        return arr;

- Do not pad your blocks with blank lines.
- **eslint:** [`padded-blocks`](http://eslint.org/docs/rules/padded-blocks.html)
- **jscs:** [`disallowPaddingNewlinesInBlocks`](http://jscs.info/rule/disallowPaddingNewlinesInBlocks)

        // bad
        function bar() {

          console.log(foo);

        }

        // also bad
        if (baz) {

          console.log(qux);
        } else {
          console.log(foo);

        }

        // good
        function bar() {
          console.log(foo);
        }

        // good
        if (baz) {
          console.log(qux);
        } else {
          console.log(foo);
        }

- Do not add spaces inside parentheses.
- **eslint:** [`space-in-parens`](http://eslint.org/docs/rules/space-in-parens.html)
- **jscs:** [`disallowSpacesInsideParentheses`](http://jscs.info/rule/disallowSpacesInsideParentheses)

        // bad
        function bar( foo ) {
          return foo;
        }

        // good
        function bar(foo) {
          return foo;
        }

        // bad
        if ( foo ) {
          console.log( foo );
        }

        // good
        if (foo) {
          console.log(foo);
        }

- Do not add spaces inside brackets.
- **eslint:** [`array-bracket-spacing`](http://eslint.org/docs/rules/array-bracket-spacing.html)
- **jscs:** [`disallowSpacesInsideArrayBrackets`](http://jscs.info/rule/disallowSpacesInsideArrayBrackets)

        // bad
        const foo = [ 1, 2, 3 ];
        console.log(foo[ 0 ]);

        // good
        const foo = [1, 2, 3];
        console.log(foo[0]);

- Add spaces inside curly braces.
- **eslint:** [`object-curly-spacing`](http://eslint.org/docs/rules/object-curly-spacing.html)
- **jscs:** [`disallowSpacesInsideObjectBrackets`](http://jscs.info/rule/disallowSpacesInsideObjectBrackets)

        // bad
        const foo = {clark: 'kent'};

        // good
        const foo = { clark: 'kent' };

- Avoid having lines of code that are longer than 100 characters (including whitespace).
- **eslint:** [`max-len`](http://eslint.org/docs/rules/max-len.html)
- **jscs:** [`maximumLineLength`](http://jscs.info/rule/maximumLineLength)

> Why? This ensures readability and maintainability.

        // bad
        const foo = 'Whatever national crop flips the window. The cartoon reverts within the screw. Whatever wizard constrains a helpful ally. The counterpart ascends!';

        // bad
        $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

        // good
        const foo = 'Whatever national crop flips the window. The cartoon reverts within the screw. ' +
          'Whatever wizard constrains a helpful ally. The counterpart ascends!';

          // good
          $.ajax({
            method: 'POST',
            url: 'https://airbnb.com/',
            data: { name: 'John' },
          })      
            .done(() => console.log('Congratulations!'))
            .fail(() => console.log('You have failed this city.'));

## Commas

- Leading commas: **Nope**.
- **eslint:** [`comma-style`](http://eslint.org/docs/rules/comma-style.html)
- **jscs:** [`requireCommaBeforeLineBreak`](http://jscs.info/rule/requireCommaBeforeLineBreak)

        // bad
        const story = [
            once
          , upon
          , aTime
        ];

        // good
        const story = [
          once,
          upon,
          aTime,
        ];

        // bad
        const hero = {
            firstName: 'Ada'
          , lastName: 'Lovelace'
          , birthYear: 1815
          , superPower: 'computers'
        };

        // good
        const hero = {
          firstName: 'Ada',
          lastName: 'Lovelace',
          birthYear: 1815,
          superPower: 'computers',
        };

- Additional trailing comma: **Yup**.
- **eslint:** [`comma-dangle`](http://eslint.org/docs/rules/comma-dangle.html)
- **jscs:** [`requireTrailingComma`](http://jscs.info/rule/requireTrailingComma)

> Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don't have to worry about the trailing comma problem in legacy browsers.

        // bad - git diff without trailing comma
        const hero = {
             firstName: 'Florence',
        -    lastName: 'Nightingale'
        +    lastName: 'Nightingale',
        +    inventorOf: ['coxcomb graph', 'modern nursing']
        };

        // good - git diff with trailing comma
        const hero = {
             firstName: 'Florence',
             lastName: 'Nightingale',
        +    inventorOf: ['coxcomb chart', 'modern nursing'],
        };

        // bad
        const hero = {
          firstName: 'Dana',
          lastName: 'Scully'
        };

        const heroes = [
          'Batman',
          'Superman'
        ];

        // good
        const hero = {
          firstName: 'Dana',
          lastName: 'Scully',
        };

        const heroes = [
          'Batman',
          'Superman',
        ];

## Semicolons

- **Yup**.
- **eslint:** [`semi`](http://eslint.org/docs/rules/semi.html)
- **jscs:** [`requireSemicolons`](http://jscs.info/rule/requireSemicolons)

        // bad
        (function () {
          const name = 'Skywalker'
          return name
        })()

        // good
        (function () {
          const name = 'Skywalker';
          return name;
        }());

        // good, but legacy (guards against the function becoming an argument when two files with IIFEs are concatenated)
        ;(() => {
          const name = 'Skywalker';
          return name;
        }());

## Type Casting & Coercion

- Perform type coercion at the beginning of the statement.
- Strings:

        // => this.reviewScore = 9;

        // bad
        const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

        // bad
        const totalScore = this.reviewScore.toString(); // isn't guaranteed to return a string

        // good
        const totalScore = String(this.reviewScore);

- Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings.
- **eslint:** [`radix`](http://eslint.org/docs/rules/radix)

        const inputValue = '4';

        // bad
        const val = new Number(inputValue);

        // bad
        const val = +inputValue;

        // bad
        const val = inputValue >> 0;

        // bad
        const val = parseInt(inputValue);

        // good
        const val = Number(inputValue);

        // good
        const val = parseInt(inputValue, 10);

- Booleans:

        const age = 0;

        // bad
        const hasAge = new Boolean(age);

        // good
        const hasAge = Boolean(age);

        // best
        const hasAge = !!age;

## Naming conventions

- Avoid single letter names. Be descriptive with your naming.

        // bad
        function q() {
          // ...stuff...
        }

        // good
        function query() {
          // ..stuff..
        }

- Use camelCase when naming objects, functions, and instances.
- **eslint:** [`camelcase`](http://eslint.org/docs/rules/camelcase.html)
- **jscs:** [`requireCamelCaseOrUpperCaseIdentifiers`](http://jscs.info/rule/requireCamelCaseOrUpperCaseIdentifiers)

        // bad
        const OBJEcttsssss = {};
        const this_is_my_object = {};
        function c() {}

        // good
        const thisIsMyObject = {};
        function thisIsMyFunction() {}

- Use PascalCase only when naming constructors or classes.
- **eslint:** [`new-cap`](http://eslint.org/docs/rules/new-cap.html)
- **jscs:** [`requireCapitalizedConstructors`](http://jscs.info/rule/requireCapitalizedConstructors)

        // bad
        function user(options) {
          this.name = options.name;
        }

        const bad = new user({
          name: 'nope',
        });

        // good
        class User {
          constructor(options) {
            this.name = options.name;
          }
        }

        const good = new User({
          name: 'yup',
        });

- Do not use trailing or leading underscores.
- **eslint:** [`no-underscore-dangle`](http://eslint.org/docs/rules/no-underscore-dangle.html)
- **jscs:** [`disallowDanglingUnderscores`](http://jscs.info/rule/disallowDanglingUnderscores)

> Why? JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean “private”, in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won't count as breaking, or that tests aren't needed. tl;dr: if you want something to be “private”, it must not be observably present.

        `// bad
        this.__firstName__ = 'Panda';
        this.firstName_ = 'Panda';
        this._firstName = 'Panda';

        // good
        this.firstName = 'Panda';`

- Don't save references to this.
- Use arrow functions or `Function#bind`.
- **jscs:** [`disallowNodeTypes`](http://jscs.info/rule/disallowNodeTypes)

        // bad
        function foo() {
          const self = this;
          return function () {
            console.log(self);
          };
        }

        // bad
        function foo() {
          const that = this;
          return function () {
            console.log(that);
          };
        }

        // good
        function foo() {
          return () => {
            console.log(this);
          };
        }

- A base filename should exactly match the name of its default export.

        // file 1 contents
        class CheckBox {
          // ...
        }
        export default CheckBox;

        // file 2 contents
        export default function fortyTwo() { return 42; }

        // file 3 contents
        export default function insideDirectory() {}

        // in some other file
        // bad
        import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
        import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
        import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

        // bad
        import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
        import forty_two from './forty_two'; // snake_case import/filename, camelCase export
        import inside_directory from './inside_directory'; // snake_case import, camelCase export
        import index from './inside_directory/index'; // requiring the index file explicitly
        import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

        // good
        import CheckBox from './CheckBox'; // PascalCase export/import/filename
        import fortyTwo from './fortyTwo'; // camelCase export/import/filename
        import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
        // ^ supports both insideDirectory.js and insideDirectory/index.js

- Use camelCase when you export-default a function.
- Your filename should be identical to your function's name.

        function makeStyleGuide() {
        }

        export default makeStyleGuide;

- Use PascalCase when you export a constructor / class / singleton / function library / bare object.

        const AirbnbStyleGuide = {
          es6: {
          }
        };

        export default AirbnbStyleGuide;

## Accessors

- Accessor functions for properties are not required.
- Do not use JavaScript getters/setters as they cause unexpected side effects and are harder to test, maintain, and reason about.
- Instead, if you do make accessor functions, use `getVal()` and `setVal('hello')`.

        // bad
        dragon.age();

        // good
        dragon.getAge();

        // bad
        dragon.age(25);

        // good
        dragon.setAge(25);

- If the property/method is a `boolean`, use `isVal()` or `hasVal()`.

        // bad
        if (!dragon.age()) {
          return false;
        }

        // good
        if (!dragon.hasAge()) {
          return false;
        }

- It's okay to create `get()` and `set()` functions, but be consistent.

        class Jedi {
          constructor(options = {}) {
            const lightsaber = options.lightsaber || 'blue';
            this.set('lightsaber', lightsaber);
          }

          set(key, val) {
            this[key] = val;
          }

          get(key) {
            return this[key];
          }
        }

## Events

- When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

        // bad
        $(this).trigger('listingUpdated', listing.id);
        ...
        $(this).on('listingUpdated', (e, listingId) => {
          // do something with listingId
        });

        // prefer
        $(this).trigger('listingUpdated', { listingId: listing.id });
        ...
        $(this).on('listingUpdated', (e, data) => {
          // do something with data.listingId
        });

## jQuery

- Prefix jQuery object variables with a `$`.
- **jscs:** [`requireDollarBeforejQueryAssignment`](http://jscs.info/rule/requireDollarBeforejQueryAssignment)

        // bad
        const sidebar = $('.sidebar');

        // good
        const $sidebar = $('.sidebar');

        // good
        const $sidebarBtn = $('.sidebar-btn');

- Cache jQuery lookups.

        // bad
        function setSidebar() {
          $('.sidebar').hide();

          // ...stuff...

          $('.sidebar').css({
            'background-color': 'pink'
          });
        }

        // good
        function setSidebar() {
          const $sidebar = $('.sidebar');
          $sidebar.hide();

          // ...stuff...

          $sidebar.css({
            'background-color': 'pink'
          });
        }

- For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`.[jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
- Use `find` with scoped jQuery object queries.

        // bad
        $('ul', '.sidebar').hide();

        // bad
        $('.sidebar').find('ul').hide();

        // good
        $('.sidebar ul').hide();

        // good
        $('.sidebar > ul').hide();

        // good
        $sidebar.find('ul').hide();
