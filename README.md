# JSX Codeguide

Opinionated guidelines that promote JSX code maintainability via:
- Code qualities: Improve code maintainability (promoted by all code rules)
- Code logic rules: Reduce unexpected code behaviours
- Code style rules: Improve code consistency and readability

## Table of Contents

- [JSX Codeguide](#jsx-codeguide)
    - [Table of Contents](#table-of-contents)
    - [Code Qualities](#code-qualities)
    - [JS Logic Rules](#js-logic-rules)
        - [Immutable Variables](#immutable-variables)
        - [Predictable Initial Values](#predictable-initial-values)
        - [Implicit Boolean Conditionals](#implicit-boolean-conditionals)
        - [Simple Conditionals](#simple-conditionals)
        - [Simple Control Paths](#simple-control-paths)
        - [Graceful Async](#graceful-async)
        - [Simple Async](#simple-async)
        - [Unused Code](#unused-code)
    - [JS Styles](#js-styles)
        - [Naming](#naming)
        - [Comments](#comments)
        - [Unary Operator Spacing](#unary-operator-spacing)
        - [Binary Operator Spacing](#binary-operator-spacing)
        - [Operator Linebreaks](#operator-linebreaks)
        - [Trailing Commas](#trailing-commas)
        - [Comma Spacing](#comma-spacing)
        - [Semicolon Presence](#semicolon-presence)
        - [Parentheses Presence](#parentheses-presence)
        - [Indentation](#indentation)
        - [Curly Bracket Style](#curly-bracket-style)
        - [Curly Bracket Presence](#curly-bracket-presence)
        - [Object Curly Bracket Spacing](#object-curly-bracket-spacing)
        - [Object Colon Spacing](#object-colon-spacing)
        - [Quote Presence](#quote-presence)
        - [Arrow Parentheses Presence](#arrow-parentheses-presence)
        - [Arrow Body Brackets Presence](#arrow-body-brackets-presence)
        - [Arrow Spacing](#arrow-spacing)
        - [Arrow Body Brackets Presence](#arrow-body-brackets-presence-1)
        - [Simple Null Coalescing](#simple-null-coalescing)
        - [Simple Optional Chaining](#simple-optional-chaining)
    - [JSX Logic](#jsx-logic)
        - [Attribute Types](#attribute-types)
        - [Default Types](#default-types)
        - [Recursive Updates](#recursive-updates)
        - [Indirect State Mutation](#indirect-state-mutation)
        - [Safe Attributes](#safe-attributes)
    - [JSX Styles](#jsx-styles)
        - [Implicit Boolean Attribute](#implicit-boolean-attribute)
        - [Attribute Quotes](#attribute-quotes)
        - [Attribute Curly Bracket Spacing](#attribute-curly-bracket-spacing)
        - [Attribute Curly Brackets Presence](#attribute-curly-brackets-presence)
        - [Attribute Indentation](#attribute-indentation)
        - [Unique Attributes](#unique-attributes)
        - [Unique Key Attribute](#unique-key-attribute)
        - [Closing Tag Presence](#closing-tag-presence)
        - [Ordered Lifecycle Methods](#ordered-lifecycle-methods)

## Code Qualities

Answering **yes** to **any** of the following anti-quality questions indicates the respective quality is not met hence may need a **rethink**.

|#|Quality|Anti-quality question|
|---|---|---|
|1|**Readable**|Is the code difficult to understand?|
|2|**Explicit**|Do you have to think about what the code does?|
|3|**Simple**|Is there lots of code or is it difficult to write?|
|4|**Consistent**|Does the code look or work differently than existing code?|
|5|**Unique**|Is there repetition?|
|6|**Functional**|Does the code not work as expected?|
|7|**Graceful**|Do errors impact functionality?|
|8|**Focused**|Does the code have many responsibilities?|
|9|**Essential**|Is the code unused?|
|10|**Pure**|Are there obsolete mutations?|

[Go to top](#table-of-contents)

## JS Logic Rules

### Immutable Variables
Variables should be `const` unless logic requires mutation.

Good:
```js
const a = 1; // Immutable.
console.log(a);

let b; // Uninitilized.
b = 2;
console.log(b);

let c = 3;
console.log(c);
c = a + b; // Requires mutation.
console.log(c);
```

Bad:
```js
let a = 1; // Obsolete since its immutable.
console.log(a);

let b = 2; // Obsolete since its immutable.
console.log(b);
```

[Go to top](#table-of-contents)

### Predictable Initial Values

**All** uninitialized variables should have predicatable initial values based on their type (e.g., all reference types start as `null`).

The `undefined` and `null` values represent unset variables and are treated as the same value (i.e., nullish) hence can be caught via nullish conditionals (e.g., `x == null`).

Primitive type initial values:
|Type|Initial Value|
|---|---|
|`boolean`|`false`|
|`number`|`0`|

Reference type initial values:
|Type|Initial Value|
|---|---|
|`string`|nullish|
|`object`|nullish|
|Array (`object`)|nullish or `[]`|
|`function`|nullish|

Good:
```js
// Primitive types start with their respective values.
const isLoggedIn = false; // Booleans start as `false`.
const totalUsers = 0; // Numbers start as `0`.

// Reference types start as nullish.
let userName; // Strings start as nullish.
let user; // Objects start as nullish.
let newUsers; // Arrays start as nullish.
let allUsers; // Arrays can start as `[]` if required.
```

Bad:

```js
// Primitives shouldn't be nullish.
const isLoggedIn; // Boolean.
const totalUsers; // Number.

// Non-nullish references cannot be caught by nullish conditionals.
let userName = ''; 
let user = {};
```

[Go to top](#table-of-contents)

### Implicit Boolean Conditionals

Implicit use of truthy/falsy conditionals should only be applied to boolean types. Other types **must** use explicit conditionals.

Good:
```js
const n = null;
const u = undefined;
const i = 0;
let b = true;

if (n == null || u == null || i === 0 || b) console.log('good');
if (b === true) console.log('good'); // Explicit boolean checks are fine to avoid ambiguouity.
```

Bad:

```js
const n = null;
const u = undefined;
const i = 0;

if (n || u || !i) console.log('bad');
```

[Go to top](#table-of-contents)

### Simple Conditionals

Conditionals should be simple, explicit, and readable hence should not include complexities (e.g., expanding a boolean expression into a ternary).

Good:
```js
a = 1;
const b = a > 0;
const c = a > 0; // `a > 0 === true` is also fine.
```

Bad:

```js
a = 1;
const b = a > 0 ? true : false;
const c = a > 0 !== false; // Never use inverted complex booleans like `x !== false`.
```

[Go to top](#table-of-contents)

### Simple Control Paths

Conditional paths should be simple hence should not have complexities (e.g., `return` in `else` when `if` contains `return`).

Good:
```js
if (a) return n;

return m;
```

Bad:

```js
if (a) return n;
else return m;
```

[Go to top](#table-of-contents)

### Graceful Async

Async operations should include handle expected errors.

Good:
```js
const whenGotError = () => Promise.reject();
const handleError = e => console.error(e);

// With `Promise`.
whenGotError.catch(handleError); // Handled error.

// With `async/await`.
(async () => { // Closure for brevity.
    try {
        // Other complex async ... (otherwise this async/await would be obsolete).

        return await whenGotError();
    } catch (e) {
        handleError(e); // Handled error.
    }
})();
```

Bad:
```js
const whenGotError = () => Promise.reject();

whenAction1(); // Unhandled promise error.

(async () => await whenGotError())(); // Unhandled async/await error.
```

[Go to top](#table-of-contents)

### Simple Async

Prefer `Promise`'s for simple async operations and optionally use `async/await` for complex async operations.

Good:
```js
// Independent async actions.
const whenFetchedCodeRules = () => Promise.resolve('...');
const whenFetchedCodeStyles = () => Promise.resolve('...');
// Dependent async actions.
const whenLogged = data => new Promise(res => {
    console.log(res);
    res();
});

const handleError = e => console.error(e);

Promise.all([whenFetchedCodeRules, whenFetchedCodeStyles]) // Unblocked independent async actions.
    // No promise nesting.
    .then(whenLogged)
    .catch(handleError);
```

Bad:
```js
// Independent async actions.
const whenFetchedCodeRules = () => Promise.resolve('...');
const whenFetchedCodeStyles = () => Promise.resolve('...');
// Dependent async actions.
const whenLogged = data => new Promise(res => {
    console.log(res);
    res();
});

const handleError = e => console.error(e);

// With promises.
whenFetchedCodeRules()
    .then(rules => {
        whenFetchedCodeStyles().then(styles => { // Blocked independent async action.
            whenLogged(rules).then(() => whenLogged(styles)) // Nested promises.
        })
    })
    .catch(handleError);

// With async/await.
(async () => { // Obsolete async/await since handling simple async actions.
    try {
        const rules = await whenFetchedCodeRules();
        const styles = await whenFetchedCodeRules(); // Blocked independent async action.
        await whenLogged(rules);
        await whenLogged(styles);
    } catch (e) {
        handleError(e);
    }
})();
```

[Go to top](#table-of-contents)

### Unused Code

Unused code should be removed. If the code may be required at a later date, it should be commentted with an explaination.

Good:
```js
// TODO: Don't remove this code since it may be required for xyz. 
// console.log('Unused code that may be required later')
```

Bad:
```js
console.log('Unused code');
console.log('Unused code that may be required later');
```

[Go to top](#table-of-contents)

## JS Styles

### Naming

All names should be concise and descriptive where possible, and abide the following rules:
- Casing:
    - File names should be camelCase unless representing a class
    - Variable, function, and instance names should be camelCase
    - Class names should be PascalCase
- Semantics:
    - Variable and class names should be nouns relevant to their value
    - Boolean variable names should indicate a toggleable state
    - Acronyms should remain camelCased
    - Function names should be prepended with a verb indicating their action
    - Async functions names should be prepended with `when`

Good:
```js
// In file `loadCodeRules.js`. // File name describes its purpose.

const isCodeRulesLoaded = false; // Name indicates the toggleable state.
const codeRulesTitle = 'Code Rules'; // Noun name relevant to variable's value.

const getCodeRulesTitle = () => { /* ... */ }; // Verb name indicates function's action.

const httpHeaders = [/* ... */]; // Acronym maintains camelCase.
httpHeaders.forEach(h => console.log(h)); // Short variable names are fine for local variables in short functions.

// Prepending `when` indicates async functions.
const whenFetchedCodeRules = () => { /* Returns promise. */ };
const whenFetchedCodeRulesCount = async () => { /* Returns promise via `await`. */ };
```

Bad:
```js
// In file `loadRules.js`. // Doesn't describe the file's purpose.
const loaded = false; // Doesn't describe what the state affects.
const t = 'Code Rules'; // Doesn't describe what the value represents.

const codeRulesTitle = () => { /* ... */ }; // Doesn't indicate the function's action.

const HTTPHeaders = [/* ... */]; // Inconsistent and breaks variable camelCasing.
httpHeaders.forEach(h => console.log(h)); // Short variable names are fine for local variables in short functions.

// These names don't indicate the functions are async.
const getCodeRules = () => { /* Returns promise. */ };
const getCodeRulesCount = async () => { /* Returns promise via `await`. */ };
```

[Go to top](#table-of-contents)

### Comments

Comments describe *what* the nature of a problem is, shouldn't impact readability, and should be:
- Concise
- Prepended with a `TODO:` tag if the comment requires review
- Single line
- Sentence-cased
- End with a period

Good:
```js
// Good.

if (true) return true; // Good since doesn't impact readability.
```

Bad:
```js
// bad
/* bad */

if (true)
// Bad since impacts readability.
return true;
```

[Go to top](#table-of-contents)

### Unary Operator Spacing

Word unary operators (e.g., `typeof`) should have a space either side of the operator whilst nonword unary operators (e.g., `++`) should be prepended with a space.

Good:
```js
const a = typeof {};
const b = ++[].length;
```

Bad:
```js
const a = typeof{};
const b =++[].length;
```

[Go to top](#table-of-contents)

### Binary Operator Spacing

Binary operators should have a space either side of the operator.

Good:
```js
const a = 1 + 2;
const b = 3 + ++4;
```

Bad:
```js
const a = 1+2;
const b = 3+++4;
```

[Go to top](#table-of-contents)

### Operator Linebreaks

Operators should prepend an expression when separated into a newline.

Good:
```js
const a = 1
    + 2;
const b = a === 1
    || a > 0
const c = a === 1
    ? 1
    : 2;
```

Bad:
```js
const a = 1 +
    2;
const b = a === 1 || 
    a > 0;
const c = a === 1 ? 1
    : 2;
```

[Go to top](#table-of-contents)

### Trailing Commas

Commas should only trail in **multiline** structures such as objects and arrays.

Good:
```js
const o1 = { n: 1 };
const o2 = {
    n: 1,
};
const a1 = [ 1 ];
const a2 = [
    1,
];
```

Bad:
```js
const o1 = { n: 1, };
const o2 = {
    n: 1
};
const a1 = [ 1, ];
const a2 = [
    1
];
```

[Go to top](#table-of-contents)

### Comma Spacing

Non-trailing commas should be followed by a space.

Good:
```js
const a = 1, b = 2;
const c = { n: 1, m: 2 };
```

Bad:
```js
const a = 1 ,b = 2;
const c = { n: 1 , m: 2 };
```

[Go to top](#table-of-contents)

### Semicolon Presence

**All** statements should end with a semicolon.

Good:
```js
const a = 1;
```

Bad:
```js
const a = 1
```

[Go to top](#table-of-contents)

### Parentheses Presence

Parentheses should be **omitted** unless they are required for logic or to improve readabilty.

Good:
```js
const a = (b + c);
```

Bad:
```js
const a = b + c;
```

[Go to top](#table-of-contents)

### Indentation

Indented code should have 4 spaces.

Good:
```js
if (true) {
    // ...
    console.log('good')
}
```

Bad:
```js
if (true) { 
// ...
console.log('bad'); // No spaces.
}

if (true) {
  // ...
  console.log('bad'); // 2 spaces.
}
```

[Go to top](#table-of-contents)

### Curly Bracket Style

Control statements with curly brackets should follow K&R-1TBS indentation (i.e., space separated opening brackets on the same line as control statement where curly brackets can be omitted if not required by logic).

Good:
```js
if (a)  {
    // ...
} else {
    // ...
}
```

Bad:
```js
if (a) 
{
    // ...
}
else 
{
    // ...
}
```

### Curly Bracket Presence

Curly brackets should only be used when required for logic or readability. E.g., curly brackets are only used with control statements (e.g., `if`, `else`, etc.) when they contain a statement block.

Good:
```js
if (a) console.log('good');
else console.log('good');

if (b) {
    // ...
    console.log('good');
}
```

Bad:
```js
if (a) {
    console.log('bad');
}
else {
    console.log('bad');
}
```

[Go to top](#table-of-contents)

### Object Curly Bracket Spacing

Object curly brackets should have a space between inside content and the brackets.

Good:
```js
const a = { n: 1 };
```

Bad:
```js
const a = {n: 1};
```

[Go to top](#table-of-contents)

### Object Colon Spacing

Object colons should be prepended with a space.

Good:
```js
const a = { n: 1 };
```

Bad:
```js
const a = { n:1 };
const b = { n :1 };
```

[Go to top](#table-of-contents)

### Quote Presence

Prefer single quotes for all strings and only used backticks if required for logic or readability.

Good:
```js
const a = 'good';
const b = `also [${a}]`;
```

Bad:
```js
const a = "bad";
const b = `bad`;
```

[Go to top](#table-of-contents)

### Arrow Parentheses Presence

Arrow function parentheses should be omitted unless required for logic (e.g., 2+ parameters).

Good:
```js
const a = x => {};
const b = (x, y) => {};
const c = ({ x }) => {};
const d = ([ x ]) => {};
```

Bad:
```js
const a = (x) => {};
```

[Go to top](#table-of-contents)

### Arrow Body Brackets Presence

Curly brackets should be omitted in arrow function bodies unless required for logic.

Good:
```js
const a = () => console.log('good');
const b = () => {
    // ...
    console.log('good');
};
```

Bad:
```js
const a = () => {
    console.log('bad');
};
```

[Go to top](#table-of-contents)

### Arrow Spacing

An arrow function arrow should have space either side.

Good:
```js
const a = () => console.log('good');
```

Bad:
```js
const a = ()=> console.log('bad');
const a = () =>console.log('bad');
const a = ()=>console.log('bad');
```

[Go to top](#table-of-contents)

### Arrow Body Brackets Presence

Curly brackets should be omitted in arrow function bodies unless required for logic.

Good:
```js
const a = () => console.log('good');
const b = () => {
    // ...
    console.log('good');
};
```

Bad:
```js
const a = () => {
    console.log('bad');
};
```

[Go to top](#table-of-contents)

### Simple Null Coalescing

Prefer functions (if available) when null coalescing several parameters.

Good:
```js
const coalesce = (...a) => a.find(v => != null); // Existing coalesce function.
const user;

const userName = coalesce(user.userName, user.name, 'Unknown'); // Function is good for several parameters.
const userName = user.userName ?? 'Unknown'; // Operator is fine for 1 parameter.
```

Bad:
```js
const coalesce = (...a) => a.find(v => != null); // Existing coalesce function.
const user;

// Operator is bad for multiple parameters
const userName = user.userName ?? user.name ?? 'Unknown';
```

[Go to top](#table-of-contents)

### Simple Optional Chaining

Optional chaining can be used in place of complex null conditionals but should:
- remain readable
- remain explicit for non-boolean values
- not be overused

Good:
```js
// Complex conditionals are fine but can be simpler via optional chaining.
if (data != null && data.user != null && data.user.name) setName(data.user.name);

// Simpler and uses explicit check for non-boolean value.
if (data?.user?.name != null) setName(data.user.name);

// Simpler and no optional chaining overuse.
const hasStats = user => user?.details?.stats == null
    ? false
    : Object.entries(user.stats).every(s => s > 0)
```

Bad:
```js
// Shouldn't use implicit checks on non-boolean values.
if (data?.user?.name) setName(data.user.name);

// Overuse of optional chaining.
const hasStats = user => (user?.details?.stats?.health
    + user?.details?.stats.attack
    + user?.details?.stats.defence) > 0;
```

[Go to top](#table-of-contents)

## JSX Logic

### Attribute Types

Components should specify `propTypes`.

Good:
```jsx
const A = createReactClass({
    propTypes = {
        x: 'good',
    },
    render () {
        return this.props.x;
    },
    // ...
});
```

Bad:
```jsx
const A = createReactClass({
    render () {
        return this.props.x;
    },
    // ...
});
```

[Go to top](#table-of-contents)

### Default Types

Components should specify `getDefaultProps` if required by logic.

Good:
```jsx
const A = createReactClass({
    // ...
    getDefaultProps() {
        x: 'good',
    },
    render () {
        return this.props.x.length;
    },
});
```

Bad:
```jsx
const A = createReactClass({
    // ...
    render () {
        return this.props.x.length;
    },
});
```

[Go to top](#table-of-contents)

### Recursive Updates

Components should avoid recursive or frequent updates (e.g., uncontrolled `setState` in `componentDidUpdate`).

Good:
```jsx
const A = createReactClass({
    // ...
    componentDidUpdate(prevProps, prevState) {
        if (prevProps !== this.props && prevState !== this.state) this.setState({ x: ++x });
    },
});
```

Bad:
```jsx
const A = createReactClass({
    // ...
    componentDidUpdate() {
        this.setState({ x: 'bad' });
    },
});
```

[Go to top](#table-of-contents)

### Indirect State Mutation

Components should not directly mutate state.

Good:
```jsx
this.setState({ x: 'good' });
```

Bad:
```jsx
this.state.x = 'bad';
```

[Go to top](#table-of-contents)

### Safe Attributes

Components should not use dangerous attributes (e.g., `dangerouslySetInnerHTML`).

Good:
```jsx
const A = <A>good</A>>;
```

Bad:
```jsx
const A = <A dangerouslySetInnerHTML={{ __html: 'bad' }} />;
```

[Go to top](#table-of-contents)

## JSX Styles

### Implicit Boolean Attribute

Boolean attributes should be implicit when the boolean evaluates to `true`.

Good:
```jsx
const A = <A x />;
```

Bad:
```jsx
const A = <A x={true} />;
```

[Go to top](#table-of-contents)

### Attribute Quotes

Attributes should use single quotes.

Good:
```jsx
const A = <A x='good' />;
```

Bad:
```jsx
const A = <A x="bad" />;
```

[Go to top](#table-of-contents)

### Attribute Curly Bracket Spacing

Attributes should have no space between curly brackets and inner expression.

Good:
```jsx
const A = <A x={x} />;
```

Bad:
```jsx
const A = <A x={ x } />;
```

[Go to top](#table-of-contents)

### Attribute Curly Brackets Presence

Attribute curly brackets should be **omitted** unless they are required for logic or to improve readabilty.

Good:
```jsx
const A = <A x='good' />;
const B = <B>good</B>;
```

Bad:
```jsx
const A = <A x={'bad'} />;
const B = <B>{'bad'}</B>;
```

[Go to top](#table-of-contents)

### Attribute Indentation

When there are 2+ attributes, they should be separated onto newlines with consistent indentation.

Good:
```jsx
const A = <A 
    x={x} 
    y={y} 
/>;
```

Bad:
```jsx
const A = <A x={x} y={y} />;
const B = <B x={x} 
y={y} />;
```

[Go to top](#table-of-contents)

### Unique Attributes

There should be no duplicate attributes.

Good:
```jsx
const A = <A x={x} />;
```

Bad:
```jsx
const A = <A 
    x={x} 
    x={x} 
/>;
```

[Go to top](#table-of-contents)

### Unique Key Attribute

Iterable components (e.g., array) should have a unique `key` attribute.

Good:
```jsx
const A = [<A key={0} />, <A key={1} />];
const B = [1, 2].map((a, i) => <A key={i} />);
```

Bad:
```jsx
const A = [<A />, <A />];
const B = [1, 2].map(a => <A />);
```

[Go to top](#table-of-contents)

### Closing Tag Presence

Components with empty content should be self-closing.

Good:
```jsx
const A = <A />;
```

Bad:
```jsx
const A = <A></A>;
```

[Go to top](#table-of-contents)

### Ordered Lifecycle Methods

Lifecycle methods should be in the following order:
1. `propTypes`
1. `getDefaultProps`
1. `getInitialState`
1. `componentDidMount`
1. `componentDidUpdate`
1. Custom methods
1. `render`

Good:
```jsx
const A = createReactClass({
    // ...
    getInitialState() {
        // ...
    },
    render() {
        // ...
    },
});
```

Bad:
```jsx
const A = createReactClass({
    // ...
    getInitialState() {
        // ...
    },
    render() {
        // ...
    },
});
```

[Go to top](#table-of-contents)
