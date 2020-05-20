# JSX Codeguide

Opinionated guidelines that promote JSX code maintainability via:
- Code qualities: Improve code maintainability (promoted by all code rules)
- Code logic rules: Reduce unexpected code behaviours
- Code style rules: Improve code consistency and readability

- [JSX Codeguide](#jsx-codeguide)
    - [Code Qualities](#code-qualities)
    - [JS Logic Rules](#js-logic-rules)
        - [Immutable Variables](#immutable-variables)
        - [Implicit Boolean Conditionals](#implicit-boolean-conditionals)
        - [Simple Conditionals](#simple-conditionals)
        - [Simple Control Paths](#simple-control-paths)
        - [Unused Code](#unused-code)
    - [JS Styles](#js-styles)
        - [Comments](#comments)
        - [Unary Operator Spacing](#unary-operator-spacing)
        - [Binary Operator Spacing](#binary-operator-spacing)
        - [Operator Linebreaks](#operator-linebreaks)
        - [Trailing Commas](#trailing-commas)
        - [Comma Spacing](#comma-spacing)
        - [Semicolon Presence](#semicolon-presence)
        - [Parentheses Presence](#parentheses-presence)
        - [Curly Bracket Style](#curly-bracket-style)
        - [Curly Bracket Presence](#curly-bracket-presence)
        - [Object Curly Bracket Spacing](#object-curly-bracket-spacing)
        - [Object Colon Spacing](#object-colon-spacing)
        - [Quote Presence](#quote-presence)
        - [Arrow Function Parentheses](#arrow-function-parentheses)
        - [Arrow Function Body](#arrow-function-body)
        - [Arrow Function Arrow Spacing](#arrow-function-arrow-spacing)
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

[Go to top](#-table-of-contents)
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

## JS Styles

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

### Arrow Function Parentheses

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

### Arrow Function Body

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

### Arrow Function Arrow Spacing

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
