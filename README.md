# JSX Codeguide

Guidelines to promote JSX code maintainability.

Contents:
- [Qualities](#qualities)
- [JS Logic](#js-logic)
- [JS Styles](#js-styles)
- [JSX Logic](#jsx-styles)
- [JSX Styles](#jsx-styles)

## Qualities

Code qualities make code **easier to maintain**.

Answering **yes** to **any** of the following anti-quality questions indicates the respective quality is not met hence may need a **rethink**.

|#|Quality|Anti-quality question|
|---|---|---|
1.|**Readable**|Is the code difficult to understand?|
2.|**Explicit**|Do you have to think about what the code does?|
3.|**Simple**|Is there lots of code or is it difficult to write?|
4.|**Consistent**|Does the code look or work differently than existing code?|
5.|**Unique**|Is there repetition?|
6.|**Functional**|Does the code not work as expected?|
7.|**Graceful**|Do errors impact functionality?|
8.|**Focused**|Does the code have many responsibilities?|
9.|**Essential**|Is the code unused?|
10.|**Pure**|Are there obsolete mutations?|

## JS Logic

### Constants

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

### Implicit boolean conditionals

Implicit use of truthy/falsy conditionals should only be applied to boolean types. Other types **must** use explicit conditionals.

Good:
```js
const n = null;
const u = undefined;
const i = 0;
let b = true;

if (n == null || u == null || i === 0 || b) console.log('Good');
if (b === true) console.log('Also good'); // Explicit boolean checks are fine to avoid ambiguouity.
```

Bad:

```js
const n = null;
const u = undefined;
const i = 0;

if (n || u || !i) console.log('Bad');
```

### Simple conditionals

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

### Simple control paths

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

### Unused code

Unused code should be removed. If the code may be required at a later date, it should be commentted with an explaination.

Good:
```js
// TODO: Don't remove this code as it may be required for xyz. 
// console.log('Unused code that may be required later')
```

Bad:
```js
console.log('Unused code');
console.log('Unused code that may be required later');
```

## JS Styles

### Unary operator spacing

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

### Binary operator spacing

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

### Operator linebreaks

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

### Trailing commas

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

### Comma spacing

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

### Semicolons

**All** statements should end with a semicolon.

Good:
```js
const a = 1;
```

Bad:
```js
const a = 1
```

### Extra parentheses

Parentheses should be **omitted** unless they are required for logic or to improve readabilty.

Good:
```js
const a = (b + c);
```

Bad:
```js
const a = b + c;
```

### Curly bracket style

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

### Curly brackets

Curly brackets should only be used when required for logic or readability. E.g., curly brackets are only used with control statements (e.g., `if`, `else`, etc.) when they contain a statement block.

Good:
```js
if (a) console.log('good');
else console.log('also good');

if (b) {
    console.log('test');
    console.log('good');
}
```

Bad:
```js
if (a) {
    console.log('bad');
}
else {
    console.log('also bad');
}
```

### Object curly bracket spacing

Object curly brackets should have a space between inside content and the brackets.

Good:
```js
const a = { n: 1 };
```

Bad:
```js
const a = {n: 1};
```

### Quotes

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

### Object colon spacing

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

### Quotes

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

### Arrow function parentheses

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

### Arrow function body

Curly brackets should be omitted in arrow function bodies unless required for logic.

Good:
```js
const a = () => console.log('good');
const b = () => {
    console.log('good');
    console.log('also good');
};
```

Bad:
```js
const a = () => {
    console.log('bad');
};
```

### Arrow function arrow spacing

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

### Specify attribute types

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

### Specify default types

Components should specify `getDefaultProps` if required by logic.

Good:
```jsx
const A = createReactClass({
    getDefaultProps() {
        x: 'good',
    },
    render () {
        return this.props.x.length;
    },
    // ...
});
```

Bad:
```jsx
const A = createReactClass({
    render () {
        return this.props.x.length;
    },
    // ...
});
```

### Avoid recursive updates

Components should avoid recursive or frequent updates (e.g., uncontrolled `setState` in `componentDidUpdate`).

Good:
```jsx
const A = createReactClass({
    componentDidUpdate(prevProps, prevState) {
        if (prevProps !== this.props && prevState !== this.state) this.setState({ x: ++x });
    },
    // ...
});
```

Bad:
```jsx
const A = createReactClass({
    componentDidUpdate() {
        this.setState({ x: 'bad' });
    },
    // ...
});
```

### Indirect state mutation

Components should not directly mutate state.

Good:
```jsx
this.setState({ x: 'good' });
```

Bad:
```jsx
this.state.x = 'bad';
```

### Safe attributes

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

### Implicit boolean attribute

Boolean attributes should be implicit when the boolean evaluates to `true`.

Good:
```jsx
const A = <A x />;
```

Bad:
```jsx
const A = <A x={true} />;
```

### Attribute curly bracket spacing

Attributes should have no space between curly brackets and inner expression.

Good:
```jsx
const A = <A x={x} />;
```

Bad:
```jsx
const A = <A x={ x } />;
```

### Extra attribute curly brackets

Attribute curly brackets should be **omitted** unless they are required for logic or to improve readabilty.

Good:
```jsx
const A = <A x='good' />;
const B = <B>good</B>;
```

Bad:
```jsx
const A = <A x={'bad'} />;
const B = <B>{'also bad'}</B>;
```

### Attribute indentation

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

### Unique attributes

There should be no duplicate attributes.

Good:
```jsx
const A = <A 
    x={x}
/>;
```

Bad:
```jsx
const A = <A 
    x={x} 
    x={x} 
/>;
```

### Unique key attribute

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

### Extra closing tag

Components with empty content should be self-closing.

Good:
```jsx
const A = <A />;
```

Bad:
```jsx
const A = <A></A>;
```

### Ordered lifecycle methods

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
    getInitialState() {
        // ...
    },
    render() {
        // ...
    },
    // ...
});
```

Bad:
```jsx
const A = createReactClass({
    getInitialState() {
        // ...
    },
    render() {
        // ...
    },
    // ...
});
```
