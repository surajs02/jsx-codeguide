# JSX Codeguide

Opinionated code guidelines that promote JS/JSX & TS/JSX (builds on JS/JSX rules) code maintainability via:
1. Code qualities: Improves code maintainability (promoted by all code rules)
1. Code logic rules: Reduces unexpected code behaviours
1. Code style rules: Improves code consistency and readability

N.B.: These guidelines are designed to promote best practices for code logic/style, however, they can be ignored on a case-by-case basis if this promotes the Code Qualities, which should always be followed.

# Table of Contents

- [JSX Codeguide](#jsx-codeguide)
- [Table of Contents](#table-of-contents)
  - [Code Qualities](#code-qualities)
  - [JS Logic](#js-logic)
    - [Immutable Variables](#immutable-variables)
    - [Magic Numbers](#magic-numbers)
    - [Predictable Initial Values](#predictable-initial-values)
    - [Useful Variables](#useful-variables)
    - [Implicit Boolean Conditionals](#implicit-boolean-conditionals)
    - [Simple Conditionals](#simple-conditionals)
    - [Explicit Conditionals](#explicit-conditionals)
    - [Query First Conditionals](#query-first-conditionals)
    - [Simple Control Paths](#simple-control-paths)
    - [Pure Control Paths](#pure-control-paths)
    - [Loop Labels](#loop-labels)
    - [Pure Iteration](#pure-iteration)
    - [Useful Iteration](#useful-iteration)
    - [Pure Functions](#pure-functions)
    - [Graceful Async](#graceful-async)
    - [Async Contains Await](#async-contains-await)
    - [Simple Async](#simple-async)
    - [Unused Code](#unused-code)
    - [Optional Parameters Last](#optional-parameters-last)
    - [Useful Constructors](#useful-constructors)
    - [Unique Class Members](#unique-class-members)
    - [Unique Imports](#unique-imports)
    - [Throw Errors](#throw-errors)
  - [JS Styles](#js-styles)
    - [Naming](#naming)
    - [Comments](#comments)
    - [Useful Docs](#useful-docs)
    - [Essential Console Logs](#essential-console-logs)
    - [Useful Production Console Logs](#useful-production-console-logs)
    - [Conditional Debugger](#conditional-debugger)
    - [End Files With Empty Line](#end-files-with-empty-line)
    - [Unary Operator Spacing](#unary-operator-spacing)
    - [Binary Operator Spacing](#binary-operator-spacing)
    - [Operator Linebreaks](#operator-linebreaks)
    - [Trailing Commas](#trailing-commas)
    - [Comma Spacing](#comma-spacing)
    - [Semicolon Presence](#semicolon-presence)
    - [Parentheses Presence](#parentheses-presence)
    - [Indentation](#indentation)
    - [Function Parentheses Placement](#function-parentheses-placement)
    - [Curly Bracket Style](#curly-bracket-style)
    - [Consistent Spacing](#consistent-spacing)
    - [Keyword Spacing](#keyword-spacing)
    - [Curly Bracket Presence](#curly-bracket-presence)
    - [Object Curly Bracket Spacing](#object-curly-bracket-spacing)
    - [Object Colon Spacing](#object-colon-spacing)
    - [Object Dot Notation](#object-dot-notation)
    - [Quote Presence](#quote-presence)
    - [Arrow Parentheses Presence](#arrow-parentheses-presence)
    - [Arrow Body Brackets Presence](#arrow-body-brackets-presence)
    - [Arrow Spacing](#arrow-spacing)
    - [Simple Null Coalescing](#simple-null-coalescing)
    - [Simple Optional Chaining](#simple-optional-chaining)
  - [JSX Logic](#jsx-logic)
    - [Useful JSX Files](#useful-jsx-files)
    - [Attribute Types](#attribute-types)
    - [Default Types](#default-types)
    - [Recursive Updates](#recursive-updates)
    - [Indirect State Mutation](#indirect-state-mutation)
    - [Safe Attributes](#safe-attributes)
  - [JSX Styles](#jsx-styles)
    - [Component Names](#component-names)
    - [File Structure](#file-structure)
    - [Tag Spacing](#tag-spacing)
    - [Implicit Boolean Attribute](#implicit-boolean-attribute)
    - [Attribute Quotes](#attribute-quotes)
    - [JSX Curly Bracket Spacing](#jsx-curly-bracket-spacing)
    - [Attribute Curly Bracket Spacing](#attribute-curly-bracket-spacing)
    - [Attribute Curly Brackets Presence](#attribute-curly-brackets-presence)
    - [Attribute Indentation](#attribute-indentation)
    - [Unique Attributes](#unique-attributes)
    - [Unique Key Attribute](#unique-key-attribute)
    - [Closing Tag Presence](#closing-tag-presence)
    - [Ordered Lifecycle Methods](#ordered-lifecycle-methods)
    - [Explicit Fragments](#explicit-fragments)
  - [TS Logic](#ts-logic)
    - [TS Imports](#ts-imports)
    - [Explicit Any](#explicit-any)
    - [Useful Type Cast](#useful-type-cast)
    - [TS Graceful Async](#ts-graceful-async)
    - [Explicit Catches](#explicit-catches)
    - [Useful Inference](#useful-inference)
    - [Abstract Interfaces](#abstract-interfaces)
    - [Immutable Members](#immutable-members)
    - [Graceful Nil Assertion](#graceful-nil-assertion)
  - [TS Styles](#ts-styles)
    - [Type Spacing](#type-spacing)

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
|9|**Essential**|Is there unused code?|
|10|**Pure**|Are there unpredictable functions or obsolete mutations?|

[Go to top](#table-of-contents)

## JS Logic

### Immutable Variables
Variables should be `const` unless logic requires mutation (where `let` is used instead but avoid `var`).

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
let a = 1; // Obsolete since immutable.
console.log(a);
```

[Go to top](#table-of-contents)

### Magic Numbers
Magic numbers and other unclear yet often used values should be descriptive reusable constants.

Good:
```js
// In constants.js.
const CLICKS_TO_WIN = 3;
const SUCCESS_COLOR = '#34A853';

// In main.js.
if (clickCount >= CLICKS_TO_WIN) { // Descriptive reusable constant number.
    buttonColor = SUCCESS_COLOR; // Descriptive reusable constant string.
    textColor = SUCCESS_COLOR;
}

```

Bad:
```js
if (clickCount >= 3) { // Unclear purpose of a specific number.
    buttonColor = '#34A853'; // Unclear purpose of color string.
    textColor = '#34A853';
}
```

[Go to top](#table-of-contents)

### Predictable Initial Values

**All** uninitialized variables should have predicatable initial values based on their type (e.g., all reference types start as `null`).

The `undefined` and `null` values represent unset variables and are treated as the same value (i.e., nullish) hence can be caught via nullish conditionals (e.g., `x == null`).

Primitive type initial values:

|Type|Initial Value|Existence Conditional
|---|---|---|
|`boolean`|`false`|`a`|
|`number`|`0`|`!isNan(a)`|

Reference type initial values:

|Type|Initial Value|Existence Conditional|
|---|---|---|
|`string`|nullish|`a != null && typeof a === 'string'`|
|`object`|nullish|`a != null`|
|`object` (Array)|nullish or `[]`|`a != null && Array.isArray(a)`|
|`function`|nullish|`a != null && typeof a === 'function'`|

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

### Useful Variables

All variables should be declared with an initial value & in use unless their preservation is required (e.g., for reference, future work, etc.). In some cases, an unused variable must be included to access other useful data (e.g., accessing subsequent function parameters), in which case the required but unused variables should be prefixed with a double underscore (i.e., `__`, which is the prefix used to indicate variables that should be ignored by linters).

Good:
```js
const nums = [10, 20, 30]
const arrToIndexes = nums.map((__, i) => i); // Fine as `nums` is used, & unused `value` (indicated by `__`) is required to access `i`.
// ... Code where `arrToIndexes` is used.
```

Bad:
```js
const undeclaredVar; // Bad as undeclared.
const unusedVar = ''; // Bad as never used;

const nums = [10, 20, 30]
const arrToIndexes = nums.map((num, i) => i); // Bad as unused `num` is not indicated by `__`.
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
const a = 1;
const b = a > 0;
const c = a > 0; // `a > 0 === true` is also fine.
```

Bad:
```js
const a = 1;
const b = a > 0 ? true : false;
const c = a > 0 !== false; // Never use inverted complex booleans like `x !== false`.
```

[Go to top](#table-of-contents)

### Explicit Conditionals

**NOTE**: This rule builds on [Predictable Initial Values](#predictable-initial-values), & continues to allow implicit booleans via [Implicit Boolean Conditionals](#implicit-boolean-conditionals).

Conditionals should be explicit (e.g., directly compare values via `===`, avoid relying on implicit truthy/falsy values like `if (string)`, separate type & value comparisons using `typeof` & `===` respectively)

Good:
```js
// Nullish (usually applies to reference types like objects/arrays/strings).
const input = undefined;
if (input == null) console.log('is null'); // Good as `==` can be used to test coalesced null (i.e., undefined | null).

// Objects.
const target = { hello: 'hello' };
const input = 'hello';
const inputExists = typeof input === 'object'; // Good as existance checked accordingly for type.
if (inputExists) console.log('exists');
if (inputExists && /* ... Compare keys/values */) console.log('matches target');

// Arrays.
const target = [1, 2, 3];
const input = [1, 2, 3];
const inputExists = Array.isArray(input); // Good as existance checked accordingly for type.
if (inputExists) console.log('exists');
if (inputExists && target.every(v => inputArr.includes(v))) console.log('matches target');

// Booleans.
const target = true;
const input = true;
const inputExists = typeof input === 'boolean'; // Good as existance checked accordingly for type.
if (inputExists) console.log('exists'); // Fine as booleans are the only type to be implicitly checked.
if (inputExists && input === target) console.log('matches target');

// Numbers.
const target = 0;
const input = 0;
const inputExists = typeof input === 'number'; // Good as existance checked accordingly for type.
if (inputExists) console.log('exists');
if (inputExists && input === target) console.log('matches target');

// Strings.
const target = 'hello';
const input = 'hello';
const inputExists = typeof input === 'string'; // Good as existance checked accordingly for type.
if (inputExists) console.log('exists');
if (inputExists && input === targetStr) console.log('matches target');
```

Bad:
```js
const input = undefined;
if (!input) console.log('is null'); // Bad as doesn't check type & cannot distinguish between `null` & `undefined`.

// Objects.
const target = { hello: 'hello' };
const input = 'hello';
if (inputExists) console.log('exists'); // Bad as doesn't check type.
if (input == target) console.log('matches target'); // Bad as doesn't check type.

// Arrays.
const targetArr = [1, 2, 3];
const inputArr = [1, 2, 3];
if (inputExists) console.log('exists'); // Bad as doesn't check type.
if (inputArr == targetArr) console.log('matches target'); // Bad as doesn't check type.

// Booleans.
const targetBool = true;
const inputBool = true;
if (inputBool == targetBool) console.log('matches target'); // Bad as doesn't check type.

// Numbers.
const targetNum = 0;
const inputNum = 0;
if (inputExists) console.log('exists'); // Bad as doesn't check type.
if (inputNum == targetNum) console.log('matches target');  // Bad as doesn't check type.

// Strings.
const targetStr = 'hello';
const inputStr = 'hello';
if (inputExists) console.log('exists'); // Bad as doesn't check type.
if (inputStr == targetStr) console.log('matches target'); // Bad as doesn't check type.
```

[Go to top](#table-of-contents)

### Query First Conditionals

Prefer the query value first (higher readability) then compare against the target value rather than vice-vera.

Good:
```js
if ('red' === color) /* ... */ // Good as query boolean is first compared against the target boolean.
```

Bad:
```js
if (color === 'red') /* ... */ // Bad as target boolean is first compared.
```

[Go to top](#table-of-contents)

### Simple Control Paths

Control paths should be simple hence should not have complexities (e.g., `return` in `else` when `if` contains `return`). Similarly, ternaries should also be simple (e.g., avoid `a ? true : false`).

Good:
```js
if (a) return n;

return m;

const isA = a;
```

Bad:
```js
if (a) return n;
else return m;

const isA = a ? true : false;
```

[Go to top](#table-of-contents)

### Pure Control Paths

Prefer expressions in control paths (e.g., using ternary instead of `if/else`);

Good:
```js
const buttonColor = isComplete // Pure immutable value.
    ? 'green'
    : hasWarnings
        ? 'orange'
        : hasErrors
            ? 'red'
            : 'grey'; // Prefer 3 as max for inline ternaries (if necessary, use a separate ternary or if/else after this point).
```

Bad:
```js
let buttonColor; // Impure obsolete variable and subsequent mutations.
if (isComplete) buttonColor = 'green';
else if (hasWarnings) buttonColor = 'orange';
else if (hasErrors) buttonColor = 'red';
else buttonColor = 'grey';
```

[Go to top](#table-of-contents)

### Loop Labels

Loop labels (e.g., `break`, `continue`) are iterative `GOTO`s hence should be avoided, however `return` is fine & encouraged.

Good:
```js
const findFirstEven = nums => nums.find(n => n % 2 === 0); // No loop labels.
```

Bad:
```js
const findFirstEven = nums => {
    let firstEven = nums[0];
    for (const i = 0; i < nums.length; i++) {
        if (nums[i] % 2 === 0) {
            firstEven = nums[i];
            break; // Loop label.
        }
    }
    return firstEven;
}
```

[Go to top](#table-of-contents)

### Pure Iteration

Prefer iterative functions (e.g., `map`) that accept higher-order functions (ideally pure) for iterative actions.

Good:
```js
const doubleNums = nums => nums.map(n => n * 2); // Iterative function applying pure higher-order function.
```

Bad:
```js
const doubleNums = nums => {
    let total = 0; // Obsolete variable.
    for (const i = 0; i < nums.length; i++) { // Impure loop.
        total += num[i]; // Impure obsolete mutation.
    }
    return total;
}
```

### Useful Iteration

If `for` loops are required, prefer utility iteration via `for-of` over `for-in` (reserved for objects but often mistakenly used on arrays) for iterating array values.

Prefer `.forEach` when iterating **both** array values & indexs.

Standard impure  `for` loops should only be used as a last resort when pure iteration & utility iteration cannot fulfill a requirement (very rare).

Good:
```js
const nums = [1, 2, 3];
nums.forEach((num, index) => /* ... Code using value & index */); // Good as both value & index are used via `.forEach`.
for (const num of nums) { /* ... Code using value */ } // Good as only value used.
```

Bad:
```js
const nums = [1, 2, 3];
for (const num in nums) { /* ... Code using value */ } // Bad as attempted to only use value but `for-in` provides index first.
for (let i = 0; i < nums.length; i++) { /* ... Code using value */ } // Bad as only value is used hence `for-of` would be better.
```

[Go to top](#table-of-contents)

### Pure Functions

**NOTE**: This rule builds on [Pure Iteration](#pure-iteration).

Prefer using pure functions that focus on providing a non-mutative output from inputs with minimal logic & side effects.

Pure functions should promote reusability & readability whilst reducing impure states & verbocity.

Fully pure functions are naturally unbounded (i.e., have no binding or `this` scoping) hence are easily passable & composable hence are preferred over impure & likely bound functions

Good:
```js
// Reduced state/logic.
const array = [1, 2, 3];
const hasOne = array.includes(1); // Good as doesn't introduce obsolete state/logic to provide an output.

// Unbounded class function works correctly
class User {
    public log = () => console.log(this); // Fine as bound to the instance.
    public toString() { return `${firstName} ${lastName}`; } // Good as impure bound state is exposed as purer controlled state.
}
const user = new User();
const log = user.log;
log(); // Fine as correctly logs `user`.
const logUser = user => console.log(user.toString());
logUser(user); // Good as pure composable function correctly logs `user`.

// Passing unbounded function works correctly.
const nums = [1, 2, 3];
const mapNums = (arr, mapper) => arr.map(mapper); // Good as pure hence composable.
const doubledNums = mapNums(num => num * 2); // Good as works correctly.
```

Bad:
```js
// Increased state/logic.
const array = [1, 2, 3];
const INVALID_INDEX = -1;
const hasOne = array.indexOf(1) !== INVALID_INDEX; // Bad as requires obsolete state & comparison logic.

// Bounded function works incorrectly.
class User {
  public log() {
    console.log(this);
  }
  public getOrderKeys(orders) {
      Object.keys(orders)
  }
}
const user = new User();
const log = user.log;
log(); // Bad as incorrectly logs global object (e.g., `window`) instead of `user`.

// Passing unbounded function works correctly.
const nums = [1, 2, 3];
const mapNums = nums.map
const doubledNums = mapNums(num => num * 2); // Bad as errors since bound scope was lost.
```

[Go to top](#table-of-contents)

### Graceful Async

Async operations should handle expected errors.

Good:
```js
const whenGotError = () => Promise.reject();
const handleError = e => console.error(e);

// With promise.
whenGotError.catch(handleError); // Handled error.

// With async/await.
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

whenGotError(); // Unhandled promise error.

(async () => await whenGotError())(); // Unhandled async/await error.
```

[Go to top](#table-of-contents)

### Async Contains Await

`async` functions should contain at least 1 `await` to simplify handling.

Good:
```js
const sleep = async () => await nativeSleep(); // Fine as contains `await`.
```

Bad:
```js
const sleep = async () => nativeSleep(); // Bad as doesn't contain `await`.
```

### Simple Async

Prefer `Promise`'s for simple async operations and optionally use `async/await` for complex async operations.

Good:
```js
const handleError = e => console.error(e);
// Independent async actions.
const whenFetchedCodeRules = () => Promise.resolve('...');
const whenFetchedCodeStyles = () => Promise.resolve('...');
// Dependent async action.
const whenLogged = data => new Promise(res => res(console.log(data)));

Promise.all([whenFetchedCodeRules, whenFetchedCodeStyles]) // Unblocked independent async actions.
    // Reduced promise nesting.
    .then(results => Promise.all(results.map(whenLogged)))
    .catch(handleError);
```

Bad:
```js
const handleError = e => console.error(e);
// Independent async actions.
const whenFetchedCodeRules = () => Promise.resolve('...');
const whenFetchedCodeStyles = () => Promise.resolve('...');
// Dependent async action.
const whenLogged = data => new Promise(res => {
    console.log(res);
    res();
});

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

Unused code should be removed. If the code may be required at a later date, it should be commented with an explanation.

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

### Optional Parameters Last

Optional parameters should all be preceeded by all non-optional parameters as this improves signature readability whilst reducing the verbocity & complexity of calls.

Good:
```js
const createUser = (firstName, lastName, active = false) => /* ... */;
const activeUser = createUser('hello', 'world', true);
const inactiveUser = createUser('hello', 'world'); // Clean & readable.
```

Bad:
```js
const createUser = (firstName, active = false, lastName) => /* ... */;
const activeUser = createUser('hello', true, 'world');
const inactiveUser = createUser('hello', null, 'world'); // Verbose & low readability.
```

[Go to top](#table-of-contents)

### Useful Constructors

Classes must have useful non-empty constructors.

Good:
```js
class User {} // Fine as constructor obsolete.

class User {
    constructor (options) {
        setup(options); // Fine as constructor runs setup.
    }
}

class Admin extends User {
    constructor (options) {
      super(options);
    }
}
```

Bad:
```js
class User {
    constructor () {} // Bad as empty constructor.
}

class Admin extends User {
    constructor (options) {
      super(options);
    }
}
```

### Unique Class Members

Classes must have unique members hence no duplicates.

Good:
```js
class User {
    _firstName;
    _lastName;

    constructor { /* ... */ }
}
```

Bad:
```js
class User {
    _firstName;
    _firstName; // Bad as duplicate member.
    _lastName;

    constructor { /* ... */ }
}
```

[Go to top](#table-of-contents)

### Unique Imports

Imports must be unique hence no duplicates.

Good:
```js
import User from 'user';
import { first, last } from 'util';
```

Bad:
```js
import User from 'user';
import { first } from 'util';
import { first, last } from 'util'; // Bad as duplicate import.
```

[Go to top](#table-of-contents)

### Throw Errors

Only errors should be thrown to improve consistency & readability hence avoid throwing literals.

Good:
```js
try {
    // ...
} catch (e) {
    throw new Error(e); // Good as throwing error.
}
```

Bad:
```js
try {
    // ...
} catch {
    throw 'error'; // Bad as throwing literal string.
}
```

[Go to top](#table-of-contents)

## JS Styles

### Naming

All names should be concise and descriptive where possible, and abide the following rules:
- Casing:
    - File names should be `camelCase` unless representing a class
    - Variable, function, and instance names should be `camelCase`
    - Class names should be `PascalCase`
- Semantics:
    - Variable and class names should be nouns relevant to their value
    - Boolean variable names should indicate a toggleable state
    - Acronyms should remain `camelCased`
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

### Useful Docs

Docs like `JSDoc` is not required but may be included if useful (e.g., useful for signatures but not useful for showing types in `*.ts` files as TS already provides typing hence obsoletes `JSDoc` types).

Good:
```typescript
// index.js
/**
 * Adds 2 numbers.
 * @param {number} a // Good as type & param info is useful in js files.
 * @param {number} b
 * @returns {number} The sum.
 */
const add = (a, b) => a + b;

// index.ts
/**
 * Adds 2 numbers.
 * @param a // Good as type info is obsolete in TS files but param info remains useful.
 * @param b
 * @returns The sum.
 */
const add = (a, b) => a + b;
```

Bad:
```typescript
// index.ts
/**
 * Adds 2 numbers.
 * @param {number} a // Bad as type info is obsolete in TS files.
 * @param {number} b
 * @returns {number} The sum.
 */
const add = (a, b) => a + b;
```

[Go to top](#table-of-contents)

### Essential Console Logs

Avoid leaving generic non-essential console logs (e.g., `console.log`) as these reduce readability by polluting the codebase & logging outputs.

Useful console logs with essential purposes (e.g., `info`, `debug`, `warn`, `error`) may be preserved.

Good:
```js
// Useful console logs.
console.info(initialState);
console.debug(globalState);
console.warn(unexpectedState);
console.error(thrownError);
```

Bad:
```js
// Obsolete console logs.
console.log('test');
console.log(temporaryVar);
```

[Go to top](#table-of-contents)

### Useful Production Console Logs

Production console logs are essential console logs (e.g., `info`, `warn`, & `error`) that are preserved to aid resolving issues. Where possible, these should provide useful information including at least the log level, issue, action, & details to help identify & resolve the issue. This information should follow a template such as `log-level: message - action. details` where `details` may be a list of key-value pairs where values are enclosed with `<<>>`, e.g., `e: User has no nickname, defaulting to defaultDisplayName=<<${getDefaultDisplayName()}>> - Please check this is expected. defaultDisplayName=<<${getDefaultDisplayName()}>>.`

Good:
```js
console.info(`i: Fetching user. userId=<<${userId}>>.`); // Fine as shows level/message/details (could optionally convert to debug log or remove).
const user = await fetchUser(userId);
if (DEBUG) console.debug(`d: Fetched user. user=<<${user}>>.`); // Good as debug log is omitted from production & shows level/message/details.
if (!user) {
    // Good as error log occurs for an unexpected situation & shows level/issue/action/details.
    const errorMessage = `e: No user was fetched - This is unexpected, please investigate. userId=<<${userId}>>, user=<<${user}>>.`
    console.error(errorMessage);

    throw new Error(errorMessage);
}
if (!user.displayName) {
    // Good as warning log for potentially unexpected but recoverable situation & shows level/issue/details.
    console.warn(`e: User has no nickname, defaulting to defaultDisplayName - Please check this is expected. userId=<<${userId}>>, defaultDisplayName<<${getDefaultDisplayName()}>>.`);
    user.displayName = getDefaultDisplayName();
}
```

Bad:
```js
console.log('test'); // Bad as non-production log in production & shows no level/action/detail.
console.info('Fetching user'); // Bad as no log level or details.
const user = await fetchUser(userId);
console.debug(user); // Bad as debug log is in production & shows no level/message.
if (!user) throw new Error('No user'); // Bad as no log/level/action/details.
if (!user.displayName) {
    console.warn('Using default user name'); // Bad as no level/action/detail.
    user.displayName = getDefaultDisplayName();
}
```

[Go to top](#table-of-contents)

### Conditional Debugger

Avoid leaving `debugger` or development tools in production code. If development tools are required, ensure they only run in the development environment;

Good:
```js
if (isDev) debugger; // Good as exclusive to development environment.
```

Bad:
```js
// ...
debugger; // Bad as will run in all environments.
// ...
```

### End Files With Empty Line

Files should end with an empty line

Good:
```js
// index.js
// ... // Good as empty line below:

```

Bad:
```js
// index.js
// ... // Bad as no empty line at end of file
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

Non-trailing commas should be appended with a space.

Good:
```js
const a = [1, 2];
```

Bad:
```js
const a = [1 , 2];
const b = [1 ,2];
const c = [1,2];
```

[Go to top](#table-of-contents)

### Semicolon Presence

**All** statements should end with a semicolon with no spacing on either side.

Good:
```js
const a = 1;
```

Bad:
```js
const a = 1
```

### Parentheses Presence

Parentheses should be **omitted** unless required for logic or to improve readabilty.

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

Indented code should have 4 spaces (can be soft `TAB`s, i.e., input via `TAB` key but **must** be saved as spaces).

Note the 4 space rule serves to promote readability whilst discouraging nesting hence promoting simplicity & maintainability. However, use case & consistency should always be prioritized hence this rule can be overridden if useful (e.g., set to 2 spaces to maintain consistency within an existing codebase).

Good:
```js
if (true) { // Good due to consistent indentation.
    // ...
    console.log('good'); // 4 spaces.
    console.log('good'); // 4 spaces.
}
```

Bad:
```js
if (true) {
console.log('bad'); // No spaces.
console.log('bad'); // No spaces.
}

if (true) {
   console.log('bad'); // 3 spaces.
   console.log('bad'); // 3 spaces.
}

if (true) { // Bad due to inconsistent indentation
    console.log('bad'); // 4 spaces.
console.log('bad'); // 0 spaces.
}
```

[Go to top](#table-of-contents)

### Function Parentheses Placement

Although arrow functions are preferred over `function` blocks for several reasons (e.g., hoisting, verbocity, etc.), certain situations may require `function` blocks (e.g., prototypes/binding & `this` scoping, stack traces, etc.).

Hence `function` blocks & their calls require styling such as function names being directly appended with their argument containing parentheses.

Good:
```js
function add(a, b) {
    return a + b;
}

add(1, 2);
```

Bad:
```js
function add (a, b) { // Bad as inconsistent spacing between name & opening parentheses.
    return a + b;
}

add (1, 2); // Bad as inconsistent spacing.
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

### Consistent Spacing

Spacing between tokens (e.g., keywords, variables & operators in expresssions, etc.) should be consistent hence non-excessive (e.g., avoid repeated successive spacing).

Good:
```js
if (a === 1) /* ... */ // Good as spacing is consistent.
```

Bad:
```js
if (a    ===1) /* ... */ // Bad as inconsistent spacing (excessive 4 spaces right of `===` whilst 0 spaces on the left).
```

### Keyword Spacing

Keywords should have space on either side unless otherwise required.

Good:
```js
if (a) /* ... */; // Good as keyword has spacing as needed.
else /* ... */;

if (b) {
    // ...
    // ...
}

if (c) {
    // ...
    // ...
} else if (d) {
    // ...
    // ...
} else {
    // ...
    // ...
}

switch (weekday) {
    case 'MONDAY': { // Case scoping is useful to avoid shadowing vars.
        let a = false;
        break;
    }
    // ...
    default: {
        // ...
    }
}

while (a) {
    // ...
    // ...
}

for (let i = 0; i < 10; i++) {
    // ...
    // ...
}

class Admin extends User {
    constructor(options) { // Fine as function/method names are directly followed by parentheses.
        super(options);
    }
}
```

Bad:
```js
if(a) /* ... */; // Bad as needlessly missing spacing.

switch(weekday) {
    case'MONDAY': { // Bad as missing spacing.
        let a = false;
        break;
    }
    // ...
    default: {
        // ...
    }
}

class Admin extends User{ // Bad as missing spacing
    constructor(options) {
        super(options);
    }
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

Object colons should be appended with a space.

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

### Object Dot Notation

Prefer dot notation (i.e., `obj.prop`) over bracket/index notation (i.e., `obj['prop']`) for objects unless required by exceptional cases (e.g., properties with `kebab-case` & `snake_case` keys).

Good:
```js
const cases = {
    lowercase: 1,
    UPPERCASE: 1,
    snake_case: 1,
    'kebab-case': 1,
    class: 1, // Keyword.
};

const lowercase = cases.lowercase;
const UPPERCASE = cases.UPPERCASE;
const snakeCase = cases['snake_case']; // Exceptional case.
const kebabCase = cases['kebab-case']; // Exceptional case.
const keyword = cases.class;
```

Bad:
```js
const cases = {
    lowercase: 1,
    UPPERCASE: 1,
    snake_case: 1,
    'kebab-case': 1,
    class: 1, // Keyword.
};

const lowercase = cases['lowercase']; // Obsolete & verbose usage of index notation.
const UPPERCASE = cases['UPPERCASE'];  // Obsolete & verbose usage of index notation.
const snakeCase = cases['snake_case']; // Exceptional case.
const kebabCase = cases['kebab-case']; // Exceptional case.
const keyword = cases['case'];  // Obsolete & verbose usage of index notation.
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
const b = () =>console.log('bad');
const c = ()=>console.log('bad');
```

[Go to top](#table-of-contents)

### Simple Null Coalescing

Prefer available functions when null coalescing several parameters.

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

// Operator is bad for multiple parameters.
const userName = user.userName ?? user.name ?? 'Unknown';
```

[Go to top](#table-of-contents)

### Simple Optional Chaining

Optional chaining can be used in place of complex conditionals but should:
- Remain readable
- Remain explicit for non-boolean values
- Not be overused

Good:
```js
// Complex conditionals are fine but can be simpler via optional chaining.
if (data != null && data.user != null && data.user.name) setName(data.user.name);

// Simpler and uses explicit check for non-boolean value.
if (data?.user?.name != null) setName(data.user.name);

// Simpler and no optional chaining overuse.
const hasStats = user => user?.details?.stats == null
    ? false
    : Object.entries(user.stats).every(([v]) => v > 0)
```

Bad:
```js
// Implicit checks on non-boolean values.
if (data?.user?.name) setName(data.user.name);

// Overuse of optional chaining.
const hasStats = user => (user?.details?.stats?.health
    + user?.details?.stats.attack
    + user?.details?.stats.defence) > 0;
```

[Go to top](#table-of-contents)

## JSX Logic

### Useful JSX Files

JSX should only be in relevant files (i.e., `*.jsx` or `*.tsx`) and React imports should be omitted unless required (e.g., if bundler doesn't parse JSX without the React import).

Good:
```jsx
// App.jsx or App.tsx
const App = <div>App</div>; // Good as JSX contained in `*.jsx` file.

export default App;
```

Bad:
```jsx
// index.js

// ... Code that doesn't use `React`.

console.log('bad');
```

[Go to top](#table-of-contents)

### Attribute Types

Components should specify `propTypes`.

Good:
```jsx
const A = createReactClass({
    // ...
    propTypes = {
        x: 'good',
    },
    render () {
        return this.props.x;
    },
});
```

Bad:
```jsx
const A = createReactClass({
    // ...
    render () {
        return this.props.x;
    },
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

### Component Names

Components should be stored in `PascalCase` named constant variables that serve as component variables which additionally provides the component's displayname (never pass components which a displayname).

The component variable should then be exported from its `*.jsx`/`*tsx` file as `default` (if it is the main component of the file) or as a named export (if it is not the main component of the file).

The component's file should have a `PascalCase` filename identical to the name of the main exported component.

Good:
```jsx
// App.jsx; // Good as filename is identical to main component name.

export const AppContainer = /* ... JSX */; // Good as non-main component is `PascalCase` `const` & has named export.

const App = <div>App</div>; // Good as main component is `PascalCase` `const`.
// ...
export default App; // Good as main component is exported as `default`.
```

Bad:
```jsx
// app.js; // Bad as filename is not identical to main component name.

const appContainer = /* ... JSX */; // Bad as non-main component is not `PascalCase` `const`
export default appContainer; // Bad as non-main component is is `default` export.

let app = <div>App</div>; // Bad as main component is not `PascalCase` `const`.
// ...
export App; // Bad as main component is named export.
```

[Go to top](#table-of-contents)

### File Structure

File structure should focus on allowing sharing of common code whilst grouping features & their required (potentially unique) code (hence promoting modular code where features may be relatively easily moved to new projects) whilst maintaining a flat, simple, & **consistent** file structure.

Folder/file naming should be `PascalCase` for those associated with components & `camelCase` for those not associated with components.

Component filenames should be a `PascalCase` noun identical to the name of their main associated component name (e.g., `App.jsx`). Non-component filenames should be `camelCase` & describe their purpose (e.g., `userActions.js`).

Hence file structure is flexible but a general guideline is:
```
../ReactProject/
- ... config files (e.g., `package.json`, `.gitignore`, etc.)
- build folder/ (e.g., `build`, `dist`, etc.)
- src/
    - index.js
    - index.less
    - routes.js
    - middleware.js
    - store.js (i.e., Redux store)
    - util/ (shared utilities)
        - utilMisc.js
        - utilMath.js
    - state/ (example of shared Redux state `action` & `reducers` folders are preferred as there may be many different states)
        - actions/
            - userActions.js
            - ...
        - reducers/
            - userReducer.js
            - ...
    - Components/
        - Shared/ (shared components, e.g., Button, Modal, etc.)
            - Button (example of shared component & associated file structure)
                - Button.jsx
                - Button.less
                - Button.stories.js (example of unit test file)
                - Button.test.js (example of UI test file)
                - useDrag.js (example of React hook file)
        - ContactPage/ (example of unique page/feature, i.e., not shared with other components)
            - ContactContainer.jsx
            - ContactPage.jsx
            - ContactPage.less
            - state/ (example of Redux state unique to ContactPage - can convert to `React.Context` if flat component)
                - contactActions.js
                - contactReducer.js
```

[Go to top](#table-of-contents)

### Tag Spacing

JSX tag brackets should have no spacing after the opening bracket & before closing bracket, & should have a space before any self-closing slash.

Good:
```jsx
const div = <div></div>;
const div = <div />;
```

Bad:
```jsx
const div = < div ></ div >;
const div = <div/>;

```

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

### JSX Curly Bracket Spacing

Curly brackets between JSX tags should have no spacing between the curly brackets and inner expression.

Good:
```jsx
const headline = <h1>{headline}</h1>;
```

Bad:
```jsx
const headline = <h1>{ headline }</h1>;
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
const B = [1, 2].map((_, i) => <A key={i} />);
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

### Explicit Fragments

Fragment usage is rare (& may break React < 16.2) hence the intention to use them should be made explicit.

Good:
```jsx
import React, { Fragment } from 'react';
const A = <Fragment><A /></Fragment>;
const A = <React.Fragment><A /></React.Fragment>;
```

Bad:
```jsx
const A = <><A /></>;
```

[Go to top](#table-of-contents)

## TS Logic

### TS Imports

Prefer `default` & named imports over `*` imports (e.g., avoid `import * as util from 'util';`) to maintain consistency & interoperability with JS/Node modules.

The `*` imports are avoided as they can be inconsistent & break if a module exports a non-object, furthermore, `*` imports are increasingly deprecated by encouraging `default`/named imports via the `tsc` `esModuleInterop` flag.

Node `require` imports are allowed in `*.js` files to promote JS/TS interoperability but standard `default`/named imports should preferred in TS files to preserve typing.

Good:
```typescript
import util, { first, last } from 'util'; // Good as using consistent `default` & named imports.
const util = require('util'); // Fine for JS/TS interoperability.
```

Bad:
```typescript
import * as util, { first, last } from 'util'; // Bad as using unique inconsistent `*` import.
```

[Go to top](#table-of-contents)

### Explicit Any

Primitive types (e.g., `boolean`, `number`, `string`, `unknown`, etc.), generic types (e.g., `Record<K, V>`) , & custom types (e.g., `User`) are preferred over the `any` type to ensure type safety (e.g., `boolean` is a known type, & even `unknown` offers better typeng over `any` since `unknown` cannot be reassigned).

However, if the `any` type is required (e.g., for complex type signatures or to support usage of a non-typed 3rd party library), the `any` type should be explicit to indicate it was used intentionally.

Good:
```typescript
const add = (a: number, b: number): number => a + b; // Good as explicit typing.
const add = (a: number, b: number) => a + b; // Infered return type is fine.
const add = (a = 0, b = 0) => a + b; // Obvious inference is fine.
```

### Useful Type Cast

Type casts should change the type of a value, & shouldn't be used in place of null assertions (e.g., avoid `let maybe: (number | undefined); maybe as string;`).

Good:
```typescript
// Type Cast.
const num = 3;
const castedToNum = '3' as number; // Good as cast used to ensure expected type.
function castToNum => (n: number | undefined): number => n!; // Good as cast used to ensure expected type.

// Null assertion.
const maybe = Math.random() > 0.5 ? true : undefined;
const num = maybe!; // Good as using explicit null assertion.
```

Bad:
```typescript
// Type Cast.
const num = 3;
const castedToNum = foo!;  // Bad as obsolete cast leaves type unchanged.
const castedToNum = 3 as number; // Bad as obsolete cast leaves type unchanged.
const castedToNum = 3 as <3>; // Bad as obsolete cast leaves type unchanged.
const castedToNum = 3 as num;
const castToNum = (n: number): number => n!; // Bad as obsolete cast leaves type unchanged.

// Null assertion.
const maybe = Math.random() > 0.5 ? true : undefined;
const num = maybe as string; // Bad as cast used for null assertion
```

[Go to top](#table-of-contents)

### TS Graceful Async

**NOTE**: Builds on [Graceful Async](#graceful-async)

All promise based code (i.e., `Promise`s & `async`/`await`) should be handled unless in exceptional cases (e.g., indicated by `void` type or contained in an `async` IFFE).

Good:
```typescript
const sleep = async (): void => await doSleep();
void sleep(); // Fine as `async` function indicated by `void`.
(async () => await sleep()) // Fine as `async` function contained in `async` IFFE.

void Promise.reject('test'); // // Fine as `Promise` indicated by `void`.

```

Bad:
```typescript
const sleep = async (): void => await doSleep();
sleep(); // Bad as `async` function not indicated by `void`.
(() => sleep()) // Bad as `async` function not contained in `async` IFFE.

void Promise.reject('test'); // // Bad as `Promise` not indicated by `void`.
```

[Go to top](#table-of-contents)

### Explicit Catches

Caught errors should be explicitly typed.

Good:
```typescript
try {/* ... */}
catch (e: Error) {/* ... */} // Good as explicitly & specifically typed.
catch (e: any) {/* ... */} // Fine as explicitly typed as `any`.
```

Bad:
```typescript
try {/* ... */}
catch (e) {/* ... */} // Bad as not explicitly typed.
```

[Go to top](#table-of-contents)

### Useful Inference

Typing is encouraged but may be omitted if the type is evident from the context (e.g., variable value, function parameter/return values, etc.) to reduce verbocity whilst preserving type safety.

Good:
```typescript
const num = 0; // Fine as type is evident from value.

class User {
  age = 5;  // Fine as type is evident from value.
}

const add = (a = 0, b = 0) => a + b; // Fine as typing is evident from parameters & return value.

const adduser = (id: number, name: string, active: boolean): User {/* ... */} // Good as typing is evident from parameters or return value.
```

Bad:
```typescript
let num; // Bad as type not evident from value.
let num = fetchNums().data ; // Bad as type not evident from value.

class User {
  age;  // bad as type not evident from value.
}

const add = (a, b) => {/* ... */}; // Fine as typing not evident from parameters or return value.

const adduser = (id, name, active): {/* .. */} // Bad as typing not evident from parameters or return value.
```

[Go to top](#table-of-contents)

### Abstract Interfaces

Interfaces shouldn't be instantiable hence shouldn't contain constructors but may declare construction for implementors.

Classes should only be instantiable via constructor, i.e., avoid misusing `new` & `constructor` keywords.

Good:
```typescript
class Admin {
  constructor() {/* .. */} // Good as classes can be instantiated via `constructor`.
}
interface User {
  new (): Admin; // Good as interfaces can declare construction for implementors.
}
```

Bad:
```typescript
class Admin {
  new(): Admin; // Bad as classes should only be instantiated via `constructor`.
}

interface User {
  constructor(): void; // Bad as interfaces shouldn't be instantiated.
}
```

[Go to top](#table-of-contents)

### Immutable Members

NOTE: This rule builds on [Immutable Variables](immutable-variables).

Class members that aren't mutated outside of the `constructor` should be `readonly`.

Good:
```typescript
class User {
    public name: string; // Fine as `public` members may be mutated externally.
    protected active = false; // Fine as `protected` members may be mutated by subclasses.
    private readonly id: number; // Good as `readonly` since this `private` member is only mutated in the `constructor`.

    constructor(name: string) {
        this.id = Date.now();
        this.name = name;
    }

    public setName(name: string) {
        this.name = name;
    }
}
```

Bad:
```typescript
class User {
    private id: number; // Bad as not `readonly` yet this `private` member is only mutated in the `constructor`.

    constructor() {
        this.id = Date.now();
    }
}
```

[Go to top](#table-of-contents)

### Graceful Nil Assertion

Potential `null` & `undefined` variables should only be asserted if their value is known to not cause a `null` based `TypeError`. If errors are expected, there should be usage of refactoring, error handling, & defaults.

Good:
```typescript
let numbers = [1, 2, 3];
const getRandomNumber = <T>(array: T[]): T | undefined => { /* Returns number or undefined if empty array... */ };
const r = getRandomNumber(numbers);
numbers.includes(r!); // Nil assertion here is fine since `r` is a number.

number = [];
if (randomNumber) numbers.includes(randomNumber(numbers)!) // Fine since non-nil error handling is used.
```

Bad:
```typescript
const numbers = [];
const getRandomNumber = <T>(array: T[]): T | undefined => { /* Returns number or undefined if empty array... */ };
const r = getRandomNumber(numbers);
numbers.includes(randomNumber(numbers)!); // Bad since `r` is undefined & no error handling is used.
```

[Go to top](#table-of-contents)

## TS Styles

### Type Spacing

Type declaration colons should only be appended with a space.

Good:
```typescript
let num: number; // Good spacing.
```

Bad:
```typescript
let num : number; // Bad spacing.
let num :number; // Bad spacing.
```

[Go to top](#table-of-contents)