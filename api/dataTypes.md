# Data Types

---

<p style="font: italic 1em sans-serif; color: #78909C">This chapter is pending supplementation or improvement...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Feb 22, 2023.</p>

---

Data types are used to constrain the interpretation of data.  
The data types in this chapter include [number / void / any / object / generics / intersection types], etc.

> Note: The type concepts in this chapter may differ from JavaScript data types (e.g., [Primitive Types](https://developer.mozilla.org/en-US/docs/Glossary/Primitive/)) and TypeScript data types (e.g., [Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)). They are only intended to aid understanding of the documentation content and are not suitable for strict conceptual reference.

---

## Boolean

Boolean type.

**foo(bar)**

- **bar** { [boolean](#boolean) }

```js
foo(true); /* As expected. */
foo(false); /* As expected. */
foo(3); /* Not as expected. */
```

Be aware of JavaScript's short-circuit evaluation:

```js
/* As expected, equivalent to foo(false). */
foo(3 > 4);

/* Not as expected, equivalent to foo("hello"). */
foo(3 > 4 || "hello");

/* As expected, equivalent to foo(false). */
foo(3 > 4 && "hello");

/* Not as expected, equivalent to foo("hello"). */
foo(3 > 2 && "hello");
```

## Number

Number type.

Common representations:

- `3` - Integer
- `+3` - Integer
    - Same result as 3, usually only used to emphasize positivity
    - The "+" here is not a sign but a unary operator
- `-3` - Negative number
- `3.1` - Decimal
    - JS uses the IEEE 754 double-precision format to store numbers
    - See: [0.1 + 0.2 !== 0.3](https://github.com/HXWfromDJTU/blog/issues/20)
- `3.0` - Integer
    - Same result as 3; JS does not have Double or similar types
- `.1` - Decimal, omitting the leading 0, equivalent to 0.1
- `2e3` - Scientific notation, equivalent to 2 × 10^3, i.e., 2000
    - The letter e represents the power of 10; the numbers before and after e are called the significand and the exponent respectively
    - The significand can be an integer or decimal literal:
        - `1e2`, `3.1e2`, `-9e2`, `0e2`, `.1e2` are all valid
    - The exponent must be an integer literal:
        - `1e2`, `1e-2` are valid
    - Variables, parentheses, or other symbols cannot appear before or after e:
        - `let num = 3;`
        - `nume2`, `(num)e2`, `(3)e(2)`, `3e(num)` are all invalid
- `0x23` - Hexadecimal
- `0b101` - Binary
- `0o307` - Octal
- `NaN` - Special numeric value
    - See: [NaN](glossaries#nan)
- `Infinity` - Positive infinity
- `-Infinity` - Negative infinity
- `Number.XXX` - Constants on the Number object
    - Such as [Number\.EPSILON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/EPSILON), [Number.MAX_VALUE](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_VALUE), etc.
- `Math.XXX` - Constants on the Math object
    - Such as [Math.PI](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/PI), [Math.SQRT2](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/SQRT2), [Math.LN2](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/LN2), etc.

**foo(bar)**

- **bar** { [number](#number) }

```js
foo(3); /* As expected. */
foo(3.3); /* As expected. */
foo(3e3); /* As expected. */
foo(NaN); /* As expected. */
```

All numbers in JavaScript are floating-point, so the number type makes no distinction between Double, Float, Long, Integer, Short, etc.

```js
3.0 === 3; // true
typeof new java.lang.Double(5.23).doubleValue(); // "number"
```

> Note: To represent a very large number (exceeding `2^53 - 1`), you need to use [BigInt](glossaries#bigint).  
> The `bigint` type rarely appears in the documentation, including [union type](#union-type) data such as `number | bigint`.

## String

String type.

Common representations:

- `"hello"` — Paired double quotes (`"`)
- `'hello'` — Paired single quotes (`'`)
- `` `hello` `` — Paired backticks (`` ` ``)
    - See: [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
- Escape characters
    - Such as `\n`, `\r`, `\uXXXX`, `\xXX`, etc.
    - See: [Escape Characters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String#escape_notation)

**foo(bar)**

- **bar** { [string](#string) }

```js
foo("3"); /* As expected. */
foo('3.3'); /* As expected. */
foo(`3e3 equals to ${3000}`); /* As expected. */
foo(NaN.toString()); /* As expected. */
```

## Array

Array type.

The suffix "[]" represents the array type.  
For example, `number[]` represents an array whose elements are all of type [number](#number), with no limit on the number of elements (including 0, i.e., an empty array).

> Note: `number[]` is different from `[number]`. The latter represents a [tuple type](#tuple).

> Note: Using generic notation such as `Array<T>` can also represent array types, but the documentation usually only uses the suffix notation.

**foo(bar)**

- **bar** { [string[]](#array) }

```js
foo([ "3" ]); /* As expected. */
foo([ 3 ]); /* Not as expected. */
foo([ "3", 3 ]); /* Not as expected. */
foo([]); /* As expected. */
```

## Tuple

Tuple type.

The tuple type strictly limits the corresponding types and number of elements in an array.  
For example, `[ number, number, string, number ]` has the following constraints:  
- The array must have exactly 4 elements;  
- The element types are number, number, string, number in that order.

> Note: Pay special attention to the similarities and differences between tuple types and JSDoc array representations.  
> Additionally, JavaScript itself has no concept of tuples.

**foo(bar)**

- **bar** { [ [string](#string), [number](#number) ] }

```js
foo([ "3" ]); /* Not as expected. */
foo([ 3 ]); /* Not as expected. */
foo([ "3", 3 ]); /* As expected. */
foo([]); /* Not as expected. */
```

## Function

Function type.

The documentation uses [arrow function syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) to represent a function parameter.

**foo(bar)**

- **bar** { [() =>](#function) [number](#number) }

In the [method signature](documentation#method-signature) above, `bar` is a function parameter. The function takes no parameters and returns a value of type number.

```js
foo(Math.random()); /* Not as expected. */

foo(function () {
    return Math.random();
}); /* As expected. */

foo(function () {
    return 'hello';
}); /* Not as expected. */
```

**foo(bar)**

- **bar** { [(a: ](#function)[string](#string)[, b: ](#function)[any](#any)[) => ](#function)[string](#string) }

In the [method signature](documentation#method-signature) above, `bar` is a function parameter. The function takes two parameters and returns a value of type string.

```js
/* Parameter a is of type string, b is of type any. */
foo(function (a, b) {
    return a + String(b); /* String concatenation. */
}); /* As expected. */
```

## RegExp

Regular expression type.

**foo(bar)**

- **bar** { [RegExp](#regexp) }

In the [method signature](documentation#method-signature) above, `bar` is a regular expression parameter, which is the standard JavaScript RegExp type:

1. Literal

   `foo(/hello.+world?/)`

2. RegExp constructor

   `new RegExp('hello.+world?')`

> See: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)

## Any

Any type.

The any type is compatible with all types.

**foo(bar)**

- **bar** { [any](#any) }

```js
foo(3); /* As expected. */
foo([]); /* As expected. */
foo({}); /* As expected. */
foo(null); /* As expected. */
```

Although any is compatible with all types, a concrete type must still be provided — it cannot be omitted:

```js
foo(); /* Not as expected. */
foo(undefined); /* As expected. */
```

## Void

This type is used to indicate that a function has no return value.

### As a function body return type

**foo(bar)**

- **bar** { [any](#any) }
- <ins>**returns**</ins> { [void](#void) }

Void as the return type of the foo function body means that the foo function does not return a value:

```js
function foo() {
    console.log("hello");
} /* As expected. */

function foo() {
    return "hello";
} /* Not as expected. */
```

### As a parameter return type

**foo(bar)**

- **bar** { [() =>](#function) [void](#void) }

In the [method signature](documentation#method-signature) above, `bar` is a function parameter that is a function returning void.
`void` does not mean that the return value must be of type `void`.  
It means that all values returned by `bar` are ignored (i.e., not cared about).

```js
let arr = [];
foo(() => arr.push(Math.random())); /* As expected. */
console.log(arr);
```

### Void vs Undefined

**foo(bar)**

- **bar** { [string](#string) }
- <ins>**returns**</ins> { [void](#void) }

In JavaScript, a function without a `return` statement will implicitly return [undefined](#undefined).  
Therefore, for function bodies, a return type of `void` is equivalent to `undefined`:

```js
foo(() => {
    return;
}) /* As expected. */;

foo(() => {
    return undefined;
}) /* As expected. */;

foo(() => {
    // Empty body.
}) /* As expected. */;

foo(() => {
    return 3;
}) /* Not as expected. */;
```

**foo(bar, baz)**

- **bar** { [() =>](#function) [void](#void) }
- **baz** { [() =>](#function) [undefined](#undefined) }

For function parameters, the meaning of return type `void` differs from return type `undefined`.  
`void` means all returned values are ignored (see [As a parameter return type](#as-a-parameter-return-type)),  
while `undefined` means the return value must be of type `undefined`.

```js
foo(
    /* bar = */ () => {
        return;
    }, /* As expected. */
    /* baz = */ () => {
        return;
    }, /* As expected. */
);

foo(
    /* bar = */ () => {
        return undefined;
    }, /* As expected. */
    /* baz = */ () => {
        return undefined;
    }, /* As expected. */
);

foo(
    /* bar = */ () => {
        // Empty body.
    }, /* As expected. */
    /* baz = */ () => {
        // Empty body.
    }, /* As expected. */
);

foo(
    /* bar = */ () => {
        return 3;
    }, /* As expected. */
    /* baz = */ () => {
        return 3;
    }, /* Not as expected. */
);
```

> Note: If you replace `void` with `any` in the above method signature, the effect is the same regarding whether the `bar` parameter meets expectations.  
> However, there is a clear semantic difference: `void` means "I don't care about the return value of `bar`", while `any` means "any return type is acceptable".  
> This distinction becomes especially important when designing custom APIs or TypeScript declaration files.

## Never

## Object

### Literal Object Type

{{ a: number }}

## Generic

## Null

> See: [MDN #Term](https://developer.mozilla.org/en-US/docs/Glossary/Null/) / [MDN #Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/null/) / [MDN #Nullish](https://developer.mozilla.org/en-US/docs/Glossary/Nullish/)

## Undefined

```js
// device.vibrate(text: string, delay?: number): void
typeof device.vibrate("hello") === "undefined"; // true
```

> See: [MDN #Term](https://developer.mozilla.org/en-US/docs/Glossary/undefined/) / [MDN #Global Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined/)

## RegExPattern

Regular expression pattern type.

Usually only used in [Manipulating Generics](#pattern).

**foo(bar)**

- **bar** { [Pattern](#pattern)[<](#generic)[/^\d+$/](#regexp)[>](#generic) }

```js
foo("1"); /* As expected. */
foo("123"); /* As expected. */
foo("hello"); /* Not as expected. */
foo("1e3"); /* Not as expected. */
foo("1.3"); /* Not as expected. */
```

## Union Type

# Operators

## in

## keyof

## typeof

## extends

## index

## condition

## readonly

# Manipulating Generics

For example, `Array<T>`.

## Uppercase

**Uppercase&lt;T>: string**

Usually used for output transformation.  
Accepts a `string` type and produces the same type with all letters uppercase.

## Lowercase

**Lowercase&lt;T>: string**

Usually used for output transformation.  
Accepts a `string` type and produces the same type with all letters lowercase.

## Capitalize

**Capitalize&lt;T>: string**

Usually used for output transformation.  
Accepts a `string` type and produces the same type with the first letter capitalized.

## IgnoreCase

**IgnoreCase&lt;T extends string>: T**

Usually used for input transformation of parameter values.  
Accepts a `string` type and produces the same type while ignoring case.

For example, for `IgnoreCase<"webUrl">`, the following values all meet expectations:

```js
[ "webUrl", "WEBURL", "WebUrl", "WEBurl" ];
```

However, other characters cannot be inserted before, after, or inside the string,  
such as [ "WEB_URL" / "web-url" / "#WebUrl" ] etc.

## Pattern

**Pattern&lt;[T](#generic) [extends](#extends) [RegExPattern](#regexpattern)>: [string](#string)**

Usually used for input validation.  
Accepts a [regular expression literal](glossaries#regular-expression) and produces `string` type data that passes the test.

The generic wildcard `T` of `Pattern` is also called [string pattern](glossaries#string-pattern) in the documentation.

**foo(bar)**

- **bar** { [Pattern](#pattern)[<](#generic)[/^https?:/](#regexpattern)[>](#generic) }

```js
foo("http is an abbreviation."); /* Not as expected. */
foo("https://xxx"); /* As expected. */
foo("ftp://xxx"); /* Not as expected. */
```

Supports [flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#advanced_searching_with_flags):

**foo(bar)**

- **bar** { [Pattern](#pattern)[<](#generic)[/^h...[oy]/i](#regexpattern)[>](#generic) }

```js
foo("Happy"); /* As expected. */
foo("hello"); /* As expected. */
foo("Halloween"); /* As expected. */
foo("history"); /* As expected. */
foo("heroes"); /* Not as expected. */
```

For easier understanding or repeated reference, some `Pattern` types are redefined as custom types, such as [NumberString](dataTypes#numberstring).

> Note: As of (2022/08), neither JSDoc nor TypeScript has built-in type checking using regular expression literals to validate strings (see [StackOverflow](https://stackoverflow.com/questions/51445767/how-to-define-a-regex-matched-string-type-in-typescript)).  
> The above `Pattern` types are only intended to aid understanding of the documentation content.

## AnyBut

**AnyBut&lt;T>**

Any type except T.

**foo(bar)**

- **bar** { [AnyBut](#anybut)[<](#generic)[number](#number)[>](#generic) }

In the example above, the `bar` parameter accepts any type except [number](#number).

# Custom Types

## JavaArray

Java Array.

```js
let javaArr = java.lang.reflect.Array
    .newInstance(java.lang.Float.TYPE, 3);

console.log(util.isJavaArray(javaArr)); // true
console.log(Array.isArray(javaArr)); // false
```

Java arrays can use properties and methods of JavaScript arrays:

```js
let javaArr = java.lang.reflect.Array
    .newInstance(java.lang.Float.TYPE, 3);

console.log(javaArr.length); // 3

console.log(javaArr.slice === Array.prototype.slice); // true
Array.isArray(javaArr.slice(0)); // true
```

Once a Java array is initialized, its length cannot be changed. Both [changing length / out-of-bounds assignment] will fail and throw an exception:

```js
let javaArr = java.lang.reflect.Array
    .newInstance(java.lang.Float.TYPE, 3);

/* Silently fails. */
javaArr.length = 20;
console.log(javaArr.length); // 3

/* push or unshift causes out-of-bounds exception. */
javaArr.push(9); /* Error. */
javaArr.unshift(9); /* Error. */

/* pop or shift do not throw but do not change array length. */
javaArr.pop();
console.log(javaArr.length); // 3
javaArr.shift();
console.log(javaArr.length); // 3

/* Out-of-bounds access does not throw, returns undefined. */
console.log(javaArr[9]); // undefined

/* Out-of-bounds assignment throws an exception. */
javaArr[9] = 10; /* Error. */
```

Elements in a Java array are implicitly converted to the specified type, and this type is also converted to a JavaScript type. For example, Java's `Integer` is converted to `Number`:

```js
let javaArr = java.lang.reflect.Array
    .newInstance(java.lang.Integer.TYPE, 3);

console.log(javaArr.join()); // '0,0,0'

/* Number('1a') -> NaN */
javaArr[0] = '1a';
console.log(javaArr[0]); // NaN

/* Number('2.2') -> 2.2 $ JS */
/* java.lang.Integer(2.2 $ JS) -> 2 $ Java */
/* Number(2 $ Java) -> 2 $ JS */
javaArr[2] = '2.2';
console.log(javaArr[0]); // 2

/* 0xFF $ Hexadecimal == 255 $ Decimal / JS */
/* java.lang.Integer(255 $ JS) -> 255 $ Java */
/* Number(255 $ Java) -> 255 $ JS */
javaArr[0] = 0xFF;
console.log(javaArr[0]); // 255
```

> See: [Oracle Docs](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html)

## JavaArrayList

Java ArrayList.

Unlike [Java Array](#javaarray), arrays created by ArrayList can be resized:

```js
let arrList = new java.util.ArrayList();

arrList.add(10);
arrList.add('20');
arrList.add([ '30' ]);
arrList.add(/40/g);

console.log(arrList.length); // 4

arrList.forEach((o) => {
    // 10 (Number)
    // 20 (String)
    // 30 (Array)
    // /40/g (RegExp)
    console.log(`${o} (${species(o)})`);
});

arrList.addAll(arrList);
console.log(arrList.length); // 8

arrList.clear();
console.log(arrList.length); // 0
```

> See: [Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)

## NumberString

Numeric string.

[String pattern](glossaries#string-pattern): `/[+-]?(\d+(\.\d+)?(e\d+)?)/`.

```js
"12";
"-5";
"1.5";
"1.5e3";
```

## ComparisonOperatorString

Comparison operator string.

[String pattern](glossaries#string-pattern): `/<=?|>=?|=/`.

```js
">";
">=";
"<";
"<=";
"="; /* Corresponds to the strict equality operator "===" . */
```

## ScreenMetricNumberX

Screen horizontal metric value.

Representation:

- Number { X >= 1 or X < -1 } — Horizontal screen width value
- Number { X > -1 and X < 1 } — Percentage of horizontal screen width value
- Number { X == -1 } — The horizontal screen width value itself (special value)

For example, for the following parameter:

**bottom** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) }

- `bottom` assigned 50 → X coordinate is 50.
- `bottom` assigned -80 → X coordinate is -80.
- `bottom` assigned 0.5 → X coordinate is 50% of screen width, i.e. `0.5 * device.width`.
- `bottom` assigned -0.1 → X coordinate is -10% of screen width, i.e. `-0.1 * device.width`.
- `bottom` assigned -1 → X coordinate is the special value representing full screen width, i.e. `device.width`.

## ScreenMetricNumberY

Screen vertical metric value.

Representation:

- Number { Y >= 1 or Y < -1 } — Vertical screen height value
- Number { Y > -1 and Y < 1 } — Percentage of vertical screen height value
- Number { Y == -1 } — The vertical screen height value itself (special value)

For example, for the following parameter:

**top** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) }

- `top` assigned 50 → Y coordinate is 50.
- `top` assigned -80 → Y coordinate is -80.
- `top` assigned 0.5 → Y coordinate is 50% of screen height, i.e. `0.5 * device.height`.
- `top` assigned -0.1 → Y coordinate is -10% of screen height, i.e. `-0.1 * device.height`.
- `top` assigned -1 → Y coordinate is the special value representing full screen height, i.e. `device.height`.

## ScriptExecuteActivity

A subclass of [android.app.Activity](https://developer.android.com/reference/android/app/Activity).

`ScriptExecuteActivity` is the type of the global `activity` object in UI mode:

```js
'ui';
activity instanceof org.autojs.autojs.execution.ScriptExecuteActivity; // true
```

Some `activity`-related examples:

```js
/* Finish the current activity. */
activity.finish();
/* Set the status bar color to dark red. */
activity.getWindow().setStatusBarColor(colors.toInt('dark-red'));
/* Load a view object as content. */
activity.setContentView(web.newInjectableWebView('www.github.com'));
/* Get the height of the top-level window. */
activity.getWindow().getDecorView().getRootView().getHeight();
```

Because `ScriptExecuteActivity` inherits from many Java classes such as `android.app.Activity`, `activity` gains a very rich set of properties and methods. For details, see [Android Docs](https://developer.android.com/reference/android/app/Activity) and the [AutoJs6 source code](http://project.autojs6.com/blob/10960ddbee71f75ef80907ad5b6ab42f3e1bf31e/app/src/main/java/org/autojs/autojs/execution/ScriptExecuteActivity.java#L30).

## DetectCompass

The parameter type passed to [Control Compass](uiObjectType#m-compass), also known as `compass argument`.

The compass argument is of type [string](dataTypes#string) and supports individual or combined use.

Below are some examples of compass arguments:

- `p` - parent control
- `p2` - second-level parent control
- `c0` - index 0 (first) child control
- `c2` - index 2 child control
- `c-1` - last child control
- `s5` - index 5 sibling control
- `s-2` - second-to-last sibling control
- `s<1` - left adjacent sibling node
- `s>1` - right adjacent sibling node
- `k2` - search upward for clickable control (up to 2 levels)
- `p4c0>1>1>0s0` - combined usage

[Control Compass (UiObject.compass)](uiObjectType#m-compass) is a derived method of [Control Detection (UiObject.detect)](uiObjectType#m-detect), which is why the type is named `DetectCompass`.

## DetectResult

The result parameter type for [Control Detection (UiObject.detect)](uiObjectType#m-detect), also known as `detection result`. This process is also called `result filtering`.

- `# / w / widget` - [Control](uiObjectType)
- `$ / txt / content` - [Text content](uiObjectType#m-content)
- `. / pt / point` - [Point](uiObjectType#m-point)
- `UiObjectInvokable` - [Control invokable type](#uiobjectinvokable)

```js
/* Control. */
detect(w, '#');
detect(w, 'w'); /* Same as above. */
detect(w, 'widget'); /* Same as above. */

/* Text content. */
detect(w, '$');
detect(w, 'txt'); /* Same as above. */
detect(w, 'content'); /* Same as above. */

/* Point. */
detect(w, '.');
detect(w, 'pt'); /* Same as above. */
detect(w, 'point'); /* Same as above. */

/* UiObjectInvokable (control invokable type). */
detect(w, 'click'); /* i.e. w.click() */
detect(w, [ 'setText', 'hello' ]); /* i.e. w.setText('hello') */
```

Unlike [PickupResult](#pickupresult), the variety of `detection results` is relatively small.

## DetectCallback

Detection callback.

The detection callback is used to process the result of [Control Detection (UiObject.detect)](uiObjectType#m-detect).

The `callback result` affects the `detection result`. When the `callback result` returns `undefined`, the `detection result` is returned directly; otherwise, the `callback result` is returned:

```ts
function detect<T extends UiObject, R>(w: T, callback: (w: T) => R): T | R {
    let callbackResult: R = callback(w);
    return callbackResult == undefined ? w : callbackResult;
}
```

Examples:

```js
let w = pickup(/.+/);

/* Return the result of w.content(). */
detect(w, (w) => w.content());

/* Return the result of w. */
detect(w, (w) => {
    console.log(w.content());
});
```

## PickupSelector

The `selector argument` of [Pickup Selector](uiSelectorType#m-pickup).

The type of `selector argument` is divided into [Single-type Selector](#single-type-selector) and [Mixed-type Selector](#mixed-type-selector).

### Single-type Selector

Single-type selectors include [ [Classic Selector](#classic-selector) / [Content Selector](#content-selector) / [Object Selector](#object-selector) ].

#### Classic Selector

`text('abc')` or chained form `text('abc').clickable().centerX(0.5)`.

#### Content Selector

String `'abc'` or regular expression `/abc/`.  
Equivalent to `content('abc')` and `contentMatch(/abc/)`.

#### Object Selector

Use the selector name as the `key` and the selector argument as the `value`.  
If there is more than one argument, wrap them in an array. If there are no arguments, use `[]` (empty array), `null`, or the default value (e.g. `true`).  
Although a single argument can also be wrapped in an array, it is usually unnecessary.

```js
/* Classic selector. */
let selClassic = text('abc').clickable().centerX(0.5).boundsInside(0.2, 0.05, -1, -1).action('CLICK', 'SET_TEXT', 'LONG_CLICK');

/* Object selector. */
let selObject = {
    text: 'abc',
    clickable: [], /* or clickable: true */
    centerX: 0.5,
    boundsInside: [ 0.2, 0.05, -1, -1 ],
    action: [ 'CLICK', 'SET_TEXT', 'LONG_CLICK' ],
};
```

### Mixed-type Selector

A mixed-type selector consists of multiple single-type selectors.

Use an array to represent a mixed-type selector, where each element is a single-type selector:

```js
pickup([ /he.+/, clickable(true).boundsInside(0.2, 0.05, -1, -1) ]);
```

The selector argument in the example above uses a mixed-type selector containing two single-type selectors: a [Content Selector](#content-selector) and a [Classic Selector](#classic-selector).

The example above can be converted to a single-type selector:

```js
/* Object selector. */
pickup({
    contentMatch: /he.+/,
    clickable: true,
    boundsInside: [ 0.2, 0.05, -1, -1 ],
});

/* Classic selector. */
pickup(contentMatch(/he.+/).clickable(true).boundsInside(0.2, 0.05, -1, -1));
```

## PickupResult

Result parameter type of [Pickup Selector (UiSelector#pickup)](uiSelectorType#m-pickup), also known as `pickup result`. This process is also called `result filtering`.

- `# / w / widget` - [Control (UiObject)](uiObjectType)
- `{} / #{} / {#} / w{} / {w} / wc / collection / list` -> [Control Collection (UiObjectCollection)](uiObjectCollectionType)
- `[] / #[] / [#] / w[] / [w] / ws / widgets` -> [Control (UiObject)](uiObjectType) array
- `$ / txt / content` - [Text Content (UiObject#content)](uiObjectType#m-content)
- `$[] / [$] / txt[] / [txt] / content[] / [content] / contents` -> [Text Content (UiObject#content)](uiObjectType#m-content) array
- `. / pt / point` - [Point (UiObject#point)](uiObjectType#m-point)
- `.[] / [.] / point[] / [point] / pt[] / [pt] / points / pts` -> [Point (UiObject#point)](uiObjectType#m-point) array
- `@ / selector / sel` -> [Selector (UiSelector)](uiSelectorType)
- `? / exists` -> [Existence Check (UiSelector#exists)](uiSelectorType#m-exists)
- `UiObjectInvokable` - [Control Invokable Type](#uiobjectinvokable)

```js
/* Control. */
pickup(sel, '#');
pickup(sel, 'w'); /* Same as above. */
pickup(sel, 'widget'); /* Same as above. */

/* Text content. */
pickup(sel, '$');
pickup(sel, 'txt'); /* Same as above. */
pickup(sel, 'content'); /* Same as above. */

/* Text content array. */
pickup(sel, '$[]');
pickup(sel, 'txt[]'); /* Same as above. */
pickup(sel, '[content]'); /* Same as above. */
pickup(sel, 'contents'); /* Same as above. */

/* Point. */
pickup(sel, '.');
pickup(sel, 'pt'); /* Same as above. */
pickup(sel, 'point'); /* Same as above. */

/* Point array. */
pickup(sel, '.[]');
pickup(sel, '[.]'); /* Same as above. */
pickup(sel, '[point]'); /* Same as above. */
pickup(sel, 'points'); /* Same as above. */

/* UiObjectInvokable (Control Invokable Type). */
pickup(sel, 'click'); /* i.e. sel.findOnce().click() */
pickup(sel, [ 'setText', 'hello' ]); /* i.e. sel.findOnce().setText('hello') */
```

Compared with [DetectResult (Detection Result)](#detectresult), `PickupResult` has a richer variety of types.

## UiObjectInvokable

Control invokable type, used to implement method invocation in parameter form, also known as `parameterized invocation`.

Supports all instance methods of [UiObject](uiObjectType). If a method requires parameters, the parameters together with the method name must be placed in an array before being passed.

```js
/* Parameterless methods. */
detect(w, 'click'); /* i.e. w.click() */
detect(w, 'imeEnter'); /* i.e. w.imeEnter() */

/* Methods with parameters. */
detect(w, [ 'child', 0 ]); /* i.e. w.child(0) */
detect(w, [ 'setText', 'hello' ]); /* i.e. w.setText('hello') */
detect(w, [ 'setSelection', 2, 3 ]); /* i.e. w.setSelection(2, 3) */
```

## RootMode

Root mode, enum type, globalized.

| Enum Instance Name | Description                                      | <span style="white-space:nowrap">JavaScript Representative Parameter</span> |
|--------------------|--------------------------------------------------|-----------------------------------------------------------------------------|
| AUTO_DETECT        | <span style="white-space:nowrap">Auto-detect Root permission</span> | '<span style="white-space:nowrap">auto' / -1</span>                         |
| FORCE_ROOT         | <span style="white-space:nowrap">Force Root mode</span>   | <span style="white-space:nowrap"> 'root' / 1 / true</span>                  |
| FORCE_NON_ROOT     | <span style="white-space:nowrap">Force non-Root mode</span>  | <span style="white-space:nowrap">'non-root' / 0 / false</span>              |

Detect Root mode:

```js
console.log(autojs.getRootMode() === RootMode.AUTO_DETECT);
console.log(autojs.getRootMode() === RootMode.FORCE_ROOT);
console.log(autojs.getRootMode() === RootMode.FORCE_NON_ROOT);
```

Set Root mode, using 'Force Root mode' as an example:

```js
autojs.setRootMode(RootMode.FORCE_ROOT);
autojs.setRootMode('root'); /* Same as above. */
autojs.setRootMode(1); /* Same as above. */
autojs.setRootMode(true); /* Same as above. */
```

## ColorHex

Color code (Color Hex Code).

In web pages, strings like `#FF4500` are commonly used to represent a color.

In AutoJs6, there are three representation methods, all using hexadecimal codes:

### #AARRGGBB

Uses four components to represent a color, with the component order fixed as `A (alpha)`, `R (red)`, `G (green)`, `B (blue)`. Each component is represented by a hexadecimal number corresponding to `[0..255]`, padded with zero if less than two digits.

For example, a color represented as `rgba(120, 14, 224, 255)` is converted to `#AARRGGBB` format:

```text
R: 120 -> 0x78
G: 14 -> 0xE
B: 224 -> 0xE0
A: 255 -> 0xFF
#AARRGGBB -> #FF780EE0
```

Note that the `G` component in the above example needs to be zero-padded.

> Extended reading:
>
> Reverse conversion, i.e. '#FF780EE0' to RGBA components:  
> colors.toRgba('#FF780EE0'); // [ 120, 14, 224, 255 ]
>
> Get individual components:  
> let [r, g, b, a] = colors.toRgba('#FF780EE0');  
> console.log(r); // 120

### #RRGGBB

When the `A (alpha)` component is `255 (0xFF)`, the `A` component can be omitted:

```js
colors.toInt('#CD853F') === colors.toInt('#FFCD853F'); // true
```

Getting the `A (alpha)` component of `#RRGGBB` will yield `255`:

```js
colors.alpha('#CD853F'); // 255
```

Additionally, note that when using hexadecimal numbers to represent colors, `FF` cannot be omitted:

```js
colors.toHex('#CD853F', 8); // #FFCD853F
colors.toHex('#FFCD853F', 8); // #FFCD853F
colors.toHex(0xCD853F); // #00CD853F
colors.toHex(0xFFCD853F); // #FFCD853F
```

### #RGB

Three-digit shorthand form of the `#RRGGBB` hexadecimal code, e.g. `#BBFF33` can be abbreviated as `#BF3`, `#FFFFFF` as `#FFF`.

Like `#RRGGBB`, the `A (alpha)` component of `#RGB` is always `255 (0xFF)`.

```js
colors.toInt('#BBFF33') === colors.toInt('#BF3'); // true
colors.alpha('#BF3') === 255; // true
```

## ColorInt

Color integer (Color Integer).

In most cases, a color integer is used to represent a color.  
In Android source code, color integers are represented by `ColorInt`, whose value range is determined by Java's `Integer` type, i.e. `[-2^31..2^31-1]`.  
For example, the number `0xBF110523` corresponds to the decimal `3205563683`, which exceeds the above `ColorInt` range. Therefore, related methods (such as [colors.toInt](color#m-toint)) will shift this value by a `2^32` offset to the appropriate range, ultimately yielding the result `-1089403613`.

```js
colors.toInt(0xBF110523); // -1089403613
colors.toInt('#BF110523'); /* Same as above. */

console.log(0xBF110523); // 3205563683
console.log(0xBF110523 - 2 ** 32); // -1089403613
```

It follows that when `ColorInt` is passed as a parameter type, there is no range restriction, because the parameter will be shifted by the `2^32` offset into the above legal range. For example, `colors.toHex(0xFFFF3300)` will correctly return `"#FF3300"`, even though the argument `0xFFFF3300` is not in the `[-2^31..2^31-1]` range.

When `ColorInt` is used as a return value type, its return value is always within the `[-2^31..2^31-1]` range. For example, `colors.toInt(0xFFFF3300)` returns `-52480`. This return value lacks readability and is usually only used as a new parameter passed to other methods.

> Note:  
> In fact, `-52480` is the result of `0xFFFF3300 - 2 ** 32`.  
> To restore a value like `-52480` to a human-readable color code, use methods such as [colors.toHex](color#m-tohex).

## ColorName

Color name.

In the [Color Table](colorTable) chapter, the string form of the "variable name" in each color list can be used directly as a color name:

```js
/* ORANGE_RED in the CSS color list. */

/* Used as ColorInt. */
colors.toHex(colors.css.ORANGE_RED);
/* Used as ColorName. */
colors.toHex('ORANGE_RED');

/* CREAM in the WEB color list. */

/* Used as ColorInt. */
colors.toHex(colors.web.CREAM);
/* Used as ColorName. */
colors.toHex('CREAM');
```

### Name Conflicts

When using `ColorName` as a parameter, the same name may appear in different [color lists](colorTable) at the same time. For example, `CYAN` appears in all lists, and the `CYAN` in the [Material color list](colorTable#material-color-list) is different from `CYAN` in other lists.

To avoid the above conflicts, color names are looked up and used according to the following namespace priority:

```text
android > css > web > material
```

See the [Color Name Conflicts](colorTable#color-name-conflicts) section in the [Color Table](colorTable) chapter for details.

### Parameter Formats

In addition to uppercase form (such as `BLACK` or `DARK_RED`), ColorName also supports the following formats (using `LIGHT_GREY` as an example):

- `LIGHT_GREY` -- uppercase + underscore
- `LIGHTGREY` -- uppercase merged
- `light_grey` -- lowercase + underscore
- `lightgrey` -- lowercase merged
- `light-grey` -- lowercase + hyphen

Therefore, the following example code produces identical results:

```js
colors.toInt(colors.LIGHT_GREY);
colors.toInt('LIGHT_GREY');
colors.toInt('LIGHTGREY');
colors.toInt('light_grey');
colors.toInt('lightgrey');
colors.toInt('light-grey');
```

## ColorComponent

Color component type.

For example, to represent an `R (red)` component with a value of `128`, representations such as `128`, `0.5`, and `50%` can be used.

### Component Representation

An integer is usually used to represent a color component, such as `colors.rgb(10, 20, 30)`.  
The RGB series color mode range is `[0..255]`, and the HSX series color mode range is `[0..100]`.

In addition to the above integer component representation, AutoJs6 also supports percentage and other methods to represent a color component (such as `0.2`, `"20%"`, etc.).

The following table lists the component representation methods supported by AutoJs6:

**1. Integer**

| Example                         | Equivalent Statement               | Note                                              |
|---------------------------------|------------------------------------|---------------------------------------------------|
| colors.rgb(64, 32, 224)         | -                                  | -                                                 |
| colors.rgba(64, 32, 224, 255)   | -                                  | -                                                 |
| colors.hsv(30, 20, 60)          | colors.hsv(30, 0.2, 0.6)           | S (saturation) and V (value) components range [0..100] |
| colors.hsva(30, 20, 60, 255)    | colors.hsva(30, 0.2, 0.6, 255)     | A (alpha) component range [0..255]                |

**2. Floating point**

| Example                              | Equivalent Statement             | Note                  |
|--------------------------------------|----------------------------------|-----------------------|
| colors.rgb(0.5, 0.25, 0.125)         | colors.rgb(128, 64, 32)          | -                     |
| colors.rgba(0.5, 0.25, 0.1, 0.2)     | colors.rgba(128, 64, 26, 51)     | -                     |
| colors.hsv(10, 0.3, 0.2)             | colors.hsv(10, 30, 20)           | -                     |
| colors.hsva(10, 0.3, 0.2, 0.5)       | colors.hsva(10, 30, 20, 128)     | Different component ranges |

**3. Percentage**

| Example                                       | Equivalent Statement             | Note                  |
|-----------------------------------------------|----------------------------------|-----------------------|
| colors.rgb('50%', '25%', '12.5%')             | colors.rgb(128, 64, 32)          | -                     |
| colors.rgba('50%', '25%', '10%', '20%')       | colors.rgba(128, 64, 26, 51)     | -                     |
| colors.hsv(10, '30%', '20%')                  | colors.hsv(10, 30, 20)           | -                     |
| colors.hsva(10, '30%', '20%', '50%')          | colors.hsva(10, 30, 20, 128)     | Different component ranges |

### Representation Range

Different components have different ranges. When using floating point or percentage representations, pay attention to their representation ranges:

| Component        | Range     |
|------------------|-----------|
| R (red)          | [0..255]  |
| G (green)        | [0..255]  |
| B (blue)         | [0..255]  |
| A (alpha)        | [0..255]  |
| H (hue)          | [0..360]  |
| S (saturation)   | [0..100]  |
| V (value)        | [0..100]  |
| L (lightness)    | [0..100]  |

```js
colors.hsva(0.5, 0.5, 0.5, 0.5);
colors.hsva(180, 50, 50, 128); /* Same as above. */
```

### Representation Combination

Component representations support combined usage:

```js
colors.rgb(0.5, '25%', 32); /* Equivalent to colors.rgb(128, 64, 32). */
colors.rgba(0.5, '25%', 32, '50%'); /* Equivalent to colors.rgba(128, 64, 32, 128). */
```

### Flexible 1

When using combined component representations, `1` can be interpreted as either an integer component or a percentage component, according to the following rules:

For non-`RGB` components, such as `A (alpha)`, `S (saturation)`, `V (value)`, `L (lightness)`, etc., `1` is always interpreted as `100%`.

```js
colors.argb(1, 255, 255, 255); /* Equivalent to argb(255, 255, 255, 255), 1 interpreted as 100%. */
colors.hsv(60, 1, 0.5); /* S component equivalent to 100, 1 interpreted as 100%. */
colors.hsla(0, 1, 1, 1); /* Equivalent to hsla(0, 100, 100, 255). */
```

For `RGB` components, only when all three `R` / `G` / `B` components satisfy `c <= 1` and are not all `1`, it is interpreted as percentage `1` (i.e. `100%`); in other cases, it is interpreted as integer `1`.

```js
colors.rgb(1, 0.2, 0.5); /* Equivalent to rgb(255, 51, 128), 1 interpreted as 100%, yielding 255. */
colors.rgb(1, 0.2, 224); /* Equivalent to rgb(1, 51, 224), 1 interpreted as 1. */
colors.rgb(1, 160, 224); /* No special conversion, 1 interpreted as 1. */
colors.rgb(1, 1, 1); /* Equivalent to rgb(1, 1, 1), color code #010101, 1 all interpreted as 1. */
colors.rgb(1, 1, 0.5); /* Equivalent to rgb(255, 255, 128), 1 all interpreted as 100%. */
```

It can be seen that for `RGB` components, as long as one component uses a `0.x` percentage representation, `1` will all be interpreted as `255 (100%)`.

### 1 and 1.0

`JavaScript` has only the number type; `1` and `1.0` are indistinguishable, and the following two statements are completely equivalent:

```js
colors.rgb(1, 1, 0.5);
colors.rgb(1.0, 1.0, 0.5); /* Same as above. */
```

Therefore, when using `1` to represent `100%` when passing a color component parameter, it is recommended to use `1.0` for improved readability:

```js
colors.hsla(120, 0.32, 1.0, 0.5); /* Use 1.0 to represent 100%. */
```

## ColorComponents

Array of [color components](#colorcomponent).

The same color can be represented using different color modes, such as RGB color mode or HSV color mode.

The array composed of the `components` of each color mode is called a color components array. For example, the component array `[100, 240, 72]` of the RGB color mode represents `R (red)` component `100`, `G (green)` component `240`, `B (blue)` component `72`. It can be accessed using array subscript notation or destructuring assignment:

```js
let components = colors.toRgb(colors.rgb(100, 240, 72)); // [ 100, 240, 72 ]

/* Array subscript notation. */
console.log(`R: ${components[0]}, G: ${components[1]}, B: ${components[2]}`);

/* Destructuring assignment. */
let [ r, g, b ] = components;
console.log(`R: ${r}, G: ${g}, B: ${b}`);
```

Many methods starting with "to" on the global `colors` object can return color components arrays, such as [toRgb](color#m-torgb), [toHsv](color#m-tohsv), [toHsl](color#m-tohsl), [toRgba](color#m-torgba), [toArgb](color#m-toargb), etc.

Pay special attention to the `A (alpha)` component in the results of [toRgba](color#m-torgba) and [toArgb](color#m-toargb): the default range is `[0..255]`, while other methods always use `[0..1]`:

```js
colors.toRgba('blue-grey')[3]; /* A component is 255. */
colors.toArgb('blue-grey')[0]; /* A component is 255. */
colors.toHsva('blue-grey')[3]; /* A component is 1. */
colors.toHsla('blue-grey')[3]; /* A component is 1. */
```

If you want the `A (alpha)` component range in the `toRgba` and `toArgb` results to also be `[0..1]`, use the `maxAlpha` parameter:

```js
colors.toRgba('blue-grey', { maxAlpha: 1 })[3]; /* A component is 1. */
```

## ColorDetectionAlgorithm

Color detection algorithm, used to detect the degree of difference between two colors, i.e., color difference.

[Color difference](https://en.wikipedia.org/wiki/Color_difference), also known as color distance, is a parameter in the field of color science.  
Color difference quantifies an abstract concept; for example, a specific difference quantity can be calculated via [Euclidean distance](https://en.wikipedia.org/wiki/Euclidean_distance) within a color space.

When quantifying color difference, there are many different quantification methods. Color detection algorithms are usually used to calculate Euclidean distance, and color difference is quantified from this distance.

AutoJs6 has several built-in color detection algorithms; these algorithms are usually passed as parameters to a function.

### RGB Difference Detection

Parameter name: `diff`

Calculates the difference of each component between two RGB colors:

<picture>
  <source srcset="images/rgb-difference-color-detection-dark.png" media="(prefers-color-scheme: dark) and (max-width: 1024px)" width="430px">
    <source srcset="images/rgb-difference-color-detection-dark.png" media="(prefers-color-scheme: dark) and (min-width: 1024px)" width="215px">
    <source srcset="images/rgb-difference-color-detection.png" media="(min-width: 1024px)" width="215px">
    <img src="images/rgb-difference-color-detection.png" alt="rgb-difference-color-detection" width="430">
</picture>

### RGB Distance Detection

Parameter name: `rgb`

Calculates the distance between two points in RGB color space:

<picture>
  <source srcset="images/rgb-distance-color-detection-dark.png" media="(prefers-color-scheme: dark) and (max-width: 1024px)" width="508px">
    <source srcset="images/rgb-distance-color-detection-dark.png" media="(prefers-color-scheme: dark) and (min-width: 1024px)" width="254px">
    <source srcset="images/rgb-distance-color-detection.png" media="(min-width: 1024px)" width="254px">
    <img src="images/rgb-distance-color-detection.png" alt="rgb-distance-color-detection" width="508">
</picture>

### Weighted RGB Distance Detection

Parameter name: `rgb+`

Weighted RGB distance detection (Delta E):

<picture>
  <source srcset="images/weighted-rgb-distance-color-detection-dark.png" media="(prefers-color-scheme: dark) and (max-width: 1024px)" width="1070px">
    <source srcset="images/weighted-rgb-distance-color-detection-dark.png" media="(prefers-color-scheme: dark) and (min-width: 1024px)" width="535px">
    <source srcset="images/weighted-rgb-distance-color-detection.png" media="(min-width: 1024px)" width="535px">
    <img src="images/weighted-rgb-distance-color-detection.png" alt="weighted-rgb-distance-color-detection" width="1070">
</picture>

> See also:   
> [Colour metric (from compuphase.com)](https://www.compuphase.com/cmetric.htm)  
> [CIELAB Delta E* (from Wikipedia)](https://en.wikipedia.org/wiki/Color_difference#CIELAB_%CE%94E*)

### H Distance Detection

Parameter name: `h`

Distance detection of the `H (hue)` component in HSV color space:

<picture>
  <source srcset="images/h-distance-color-detection-dark.png" media="(prefers-color-scheme: dark) and (max-width: 1024px)" width="821px">
    <source srcset="images/h-distance-color-detection-dark.png" media="(prefers-color-scheme: dark) and (min-width: 1024px)" width="411px">
    <source srcset="images/h-distance-color-detection.png" media="(min-width: 1024px)" width="411px">
    <img src="images/h-distance-color-detection.png" alt="h-distance-color-detection" width="821">
</picture>

### HS Distance Detection

Parameter name: `hs`

Related distance detection of `H (hue)` and `S (saturation)` in HSV color space:

<picture>
  <source srcset="images/hs-distance-color-detection-dark.png" media="(prefers-color-scheme: dark) and (max-width: 1024px)" width="695px">
    <source srcset="images/hs-distance-color-detection-dark.png" media="(prefers-color-scheme: dark) and (min-width: 1024px)" width="348px">
    <source srcset="images/hs-distance-color-detection.png" media="(min-width: 1024px)" width="348px">
    <img src="images/hs-distance-color-detection.png" alt="hs-distance-color-detection" width="695">
</picture>

## Range

Represents a numeric range.

| Notation   | Range                     |
|------------|---------------------------|
| (a..b)     | {x &#124; a < x < b}      |
| [a..b]     | {x &#124; a <= x <= b}    |
| (a..b]     | {x &#124; a < x <= b}     |
| [a..b)     | {x &#124; a <= x < b}     |
| (a..+∞)    | {x &#124; x > a}          |
| [a..+∞)    | {x &#124; x >= a}         |
| (-∞..b)    | {x &#124; x < b}          |
| (-∞..b]    | {x &#124; x <= b}         |
| (-∞..+∞)   | {x} (any value)           |

For example, `Range[10..30]` represents the number `x` in the range `10 <= x <= 30`, while `Range[0..1)` represents the number `x` in the range `0 <= x < 1`.

## IntRange

Represents the value range of an integer. Its notation can be found in the [Range](#range) section.

For example, `IntRange[10..30]` represents the integer `x` in the range `10 <= x <= 30`, while `IntRange[0..100)` represents the integer `x` in the range `0 <= x < 100`.

## StandardCharset

The StandardCharset type supports both Java Charset class form and string form:

| Charset    | String                      | Wikipedia                                                                 |
|------------|-----------------------------|---------------------------------------------------------------------------|
| ISO_8859_1 | "ISO_8859_1" / "iso-8859-1" | [EN](https://en.wikipedia.org/wiki/ISO/IEC_8859-1)                        |
| US_ASCII   | "US_ASCII" / "us-ascii"     | [EN](https://en.wikipedia.org/wiki/ASCII)                                 |
| UTF_8      | "UTF_8" / "utf-8"           | [EN](https://en.wikipedia.org/wiki/UTF-8)                                 |
| UTF_16     | "UTF_16" / "utf-16"         | [EN](https://en.wikipedia.org/wiki/UTF-16)                                |
| UTF_16BE   | "UTF_16BE" / "utf-16be"     | [EN](https://en.wikipedia.org/wiki/UTF-16#Byte-order_encoding_schemes)    |
| UTF_16LE   | "UTF_16LE" / "utf-16le"     | [EN](https://en.wikipedia.org/wiki/UTF-16#Byte-order_encoding_schemes)    |

The Charset class can be obtained from the static constants of StandardCharsets, such as `StandardCharsets.UTF_8`.  
When representing the StandardCharset type as a string, both the uppercase form with the same name as the static constant (e.g. `'UTF_8'`) and the lowercase form with hyphens (e.g. `'utf-8'`) are supported.

Typescript declaration (TS declaration):

```ts
declare type StandardCharset = java.nio.charset.StandardCharsets
    | 'US_ASCII' | 'ISO_8859_1' | 'UTF_8' | 'UTF_16BE' | 'UTF_16LE' | 'UTF_16'
    | 'us-ascii' | 'iso-8859-1' | 'utf-8' | 'utf-16be' | 'utf-16le' | 'utf-16';
```

JavaScript example:

```js
/**
 * @param {StandardCharset} char
 * @returns void
 */
function test(char) {
    /* ... */
}

test(StandardCharsets.UTF_8); /* Charset class form. */
test('UTF_8'); /* Uppercase string form. */
test('utf-8'); /* Lowercase string form. */
```

> Note: In AutoJs6, StandardCharsets supports globalized calls.

> See also: [Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/nio/charset/StandardCharsets.html)

## ExtendModulesNames

Plugin names for AutoJs6 [built-in extension plugins](plugins#built-in-extension-plugins).

Supported string constants:

- `'Arrayx'` or `'Array'`
- `'Numberx'` or `'Number'`
- `'Mathx'` or `'Math'`

```js
/* Enable the Array built-in extension plugin. */
plugins.extend('Arrayx');
plugins.extend('Arrayx'); /* Same as above. */
```

## ActivityShortForm

Short names for jumping to internal AutoJs6 Activities.

These short names all correspond to built-in Activity pages in AutoJs6, such as the log page and settings page of AutoJs6.

```js
/* Jump to the AutoJs6 log page. */
app.startActivity('console');
app.startActivity('log'); /* Same as above. */

/* Jump to the AutoJs6 homepage. */
app.startActivity('homepage');
app.startActivity('home'); /* Same as above. */
```

All supported page short names:

- Log page - `console` / `log`
- Settings page - `settings` / `preferences` / `pref`
- Homepage - `homepage` / `home`
- About page - `about`
- Build page - `build`
- Documentation page - `documentation` / `doc` / `docs`

## BroadcastShortForm

Short names for broadcast actions that AutoJs6 can receive.

These short names all correspond to broadcast actions that AutoJs6 can receive, such as layout bounds analysis, etc.

```js
/* Send "layout bounds analysis" broadcast. */
app.sendBroadcast('inspect_layout_bounds');
app.sendBroadcast('layout_bounds'); /* Same as above. */
app.sendBroadcast('bounds'); /* Same as above. */

/* Send "layout hierarchy analysis" broadcast. */
app.sendBroadcast('inspect_layout_hierarchy');
app.sendBroadcast('layout_hierarchy');
app.sendBroadcast('hierarchy'); /* Same as above. */
```

All supported broadcast action short names:

- Layout bounds analysis - `inspect_layout_bounds` / `layout_bounds` / `bounds`
- Layout hierarchy analysis - `inspect_layout_hierarchy` / `layout_hierarchy` / `hierarchy`

## OcrModeName

OCR mode names for AutoJs6.

When using different mode names, the global `ocr` method and its related methods (such as [ocr.detect](ocr#m-detect)) will use different engines, which may result in different recognition speeds and results.

- `mlkit` - Represents the MLKit engine
- `paddle` - Represents the Paddle Lite engine

## OcrResult

OcrResult is an interface representing OCR recognition results.

---

<p style="font: bold 2em sans-serif; color: #FF7043">OcrResult</p>

---

### [p] label

- { [string](dataTypes#string) }

The text label of the OCR recognition result, usually usable as the final text recognition result.

```js
images.requestScreenCapture();
let img = images.captureScreen();
let results = ocr.detect(img);
results.map(o => o.label); /* Map all recognition results to text labels. */
```

### [p] confidence

- { [string](dataTypes#string) }

The confidence of the OCR recognition result. Higher confidence means the result is likely more accurate.

```js
images.requestScreenCapture();
let img = images.captureScreen();
let results = ocr.detect(img);
results.filter(o => o.confidence > 0.9); /* Filter results with confidence higher than 0.9. */
```

### [p] bounds

- { [AndroidRect](androidRectType) }

The bounding rectangle of the OCR recognition result, represented by [AndroidRect](androidRectType).

```js
images.requestScreenCapture();
let img = images.captureScreen();
let results = ocr.detect(img);
let clickToStart = results.find(o => o.label === 'click to start');
if (!isNullish(clickToStart)) {
    /* Click the bounding rectangle of the OCR recognition result. */
    click(clickToStart.bounds);
}
```

### [m] toString

#### toString()

- <ins>**returns**</ins> { [string](dataTypes#string) }

The overridden `toString` method of the OCR recognition result. Example format:

```text
OcrResult@46a77f4{label=19:43:52, confidence=0.9165039, bounds=Rect(14, 15 - 121, 35)}
OcrResult@9fed472{label=Service, confidence=0.88002235, bounds=Rect(30, 76 - 106, 97)}
OcrResult@59cab38{label=Tools, confidence=0.8421875, bounds=Rect(30, 324 - 88, 345)}
```

## ThemeColor

Alias for AutoJs6's built-in class `org.autojs.autojs.theme.ThemeColor`.

ThemeColor represents a theme color.

Common related methods or properties:

- [autojs.themeColor](autojs#p-themecolor)
- [Color](colorType)(**themeColor**)

When ThemeColor is used as [OmniColor](omniTypes#omnicolor), its "primary color" is used as the color value:

```js
let themeColor = autojs.themeColor;
Color(themeColor).toInt() === Color(themeColor.getColorPrimary()).toInt(); // true
```

## JsByteArray

The type used in JavaScript to represent a "byte array", i.e. [number](dataTypes#number)[[]](dataTypes#array).

> Note: Java uses the byte[] type to represent byte arrays.

Convert a JavaScript byte array to a JavaScript string:

```js
let arr = [ 104, 101, 108, 108, 111 ];
let string = ArrayUtils.jsBytesToString(arr);
console.log(string); // hello
```

Convert a JavaScript string to a Java byte array:

```js
let str = 'hello';
let bytes = new java.lang.String(str).getBytes();
console.log(bytes); // [ 104, 101, 108, 108, 111 ]
console.log(species(bytes)); // JavaArray
```

Convert a JavaScript byte array to a Java byte array:

```js
let arr = [ 104, 101, 108, 108, 111 ];
let bytes = ArrayUtils.jsBytesToByteArray(arr);
console.log(bytes); // [ 104, 101, 108, 108, 111 ]
console.log(species(bytes)); // JavaArray
```

## ByteArray

The type used in Java to represent a "byte array", i.e. `byte[]`.

> Note: Kotlin uses the ByteArray type to represent byte arrays.

A Java byte array is not a JavaScript `number[]`:

```js
console.log(util.getClass(new java.lang.String('hello').getBytes())); // class [B
console.log(util.getClassName(new java.lang.String('hello').getBytes())); // [B
```

Convert a Java byte array to a JavaScript string:

```js
let bytes = new java.lang.String('hello').getBytes();
console.log(bytes); // [ 104, 101, 108, 108, 111 ]
let str = String(new java.lang.String(bytes));
console.log(str); // hello
```

In Java, the element range of a byte array is `[-127..128]`:

```js
let key = new crypto.Key('a'.repeat(16));
console.log(
    crypto.encrypt('hello world', key, 'AES')
); // [ 105, -52, -100, 42, -7, 27, -87, -32, 83, -59, 25, 115, -103, -75, 98, 18 ]
```

To convert to the `[0..255]` range, use the `x & 0xFF` conversion:

```js
let key = new crypto.Key('a'.repeat(16));
console.log(
    crypto.encrypt('hello world', key, 'AES').map(x => x & 0xFF)
); // [ 105, 204, 156, 42, 249, 27, 169, 224, 83, 197, 25, 115, 153, 181, 98, 18 ]
```

## CryptoDigestAlgorithm

Message digest algorithms used by the [crypto](crypto) module.

| Value (string) |
|---------|
| MD5     |
| SHA-1   |
| SHA-224 |
| SHA-256 |
| SHA-384 |
| SHA-512 |

MD: Message-Digest algorithm. MD5 is widely used. MD5 is a cryptographic hash function that generates a 128-bit hash value (often represented as a 32-digit hexadecimal number) to ensure the integrity and consistency of information transmission.

SHA: Secure Hash Algorithm, a family of cryptographic hash functions. It computes a fixed-length string (i.e., message digest) corresponding to the message. Different input messages have a high probability of producing different message digests. When different messages produce the same message digest (even with very low probability), it is called a hash collision.

```js
/* Get MD5 digest of the string "hello". */
console.log(crypto.digest('hello', 'MD5')); // 5d41402abc4b2a76b9719d911017c592

/* Get SHA-1 digest of the string "hello". */
console.log(crypto.digest('hello', 'SHA-1')); // aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d

/* Empty string MD5. */
console.log(crypto.digest('', 'MD5')); // d41d8cd98f00b204e9800998ecf8427e
```

> See also: [Oracle Docs](https://docs.oracle.com/en/java/javase/11/docs/specs/security/standard-names.html#keypairgenerator-algorithms) / [Common Message Digest Algorithms Introduction](http://www.semlinker.com/message-digest-intro)

## CryptoKeyPairGeneratorAlgorithm

Key pair generator algorithms used by the [crypto](crypto) module.

| Value (string) | Alias           |
|---------|---------------|
| DH      | DiffieHellman |
| DSA     | -             |
| RSA     | -             |
| EC      | -             |
| XDH     | -             |

For example, AutoJs6's [crypto.generateKeyPair](crypto#m-generatekeypair) method can generate a public-private key pair for asymmetric encryption algorithms:

```js
let kp = crypto.generateKeyPair('DSA', 1024);
console.log(kp.publicKey);
console.log(kp.privateKey);
```

In the above example, `'DSA'` is one of the valid key pair generator algorithms.

> See also: [Oracle Docs](https://docs.oracle.com/en/java/javase/11/docs/specs/security/standard-names.html#keypairgenerator-algorithms)

## CryptoDigestOptions

Message digest generation options, mainly used in the [crypto](crypto) module.

| Property | Valid Values                                                                            | Description                              |
|----------|--------------------------------------------------------------------------------|---------------------------------|
| input    | 'file' / 'base64' / 'hex' / **'string'**                                       | Specifies input type.                         |
| output   | 'bytes' / 'base64' / **'hex'** / 'string'                                      | Specifies output type.                         |
| encoding | 'US-ASCII' / 'ISO-8859-1' / **'UTF-8'**<br> 'UTF-16BE' / 'UTF-16LE' / 'UTF-16' | Specifies input or output encoding,<br>only valid for 'string' type. |

> Note: Bold values in the table above are the default values for the properties.

## CryptoCipherTransformation

Cipher transformation name, mainly used in the [crypto](crypto) module.

Cipher can be translated as "password" or "cipher".

In AutoJs6's [crypto](crypto) module, the internal implementation of [encrypt](crypto#m-encrypt) and [decrypt](crypto#m-decrypt) both rely on `javax.crypto.Cipher` instances.

The `javax.crypto.Cipher` class provides encryption and decryption functionality. It forms the core of `JCE (Java Cryptography Extension)` and is a native Java JDK API.

Cipher instances are initialized using the `Cipher.getInstance(transformation: String)` method. This `transformation` parameter, i.e., the "transformation name", is used to obtain Cipher instances for different encryption/decryption methods.

The `transformation` parameter has two formats:

- Algorithm name (algorithm)
- Algorithm name / working mode / padding (algorithm/mode/padding)

```js
/* Cipher instance with transformation name in "algorithm name" format. */
let cipherA = Cipher.getInstance("AES");

/* Cipher instance with transformation name in "algorithm name / working mode / padding" format. */
let cipherB = Cipher.getInstance("DES/CBC/PKCS5Padding");
```

Common related methods or properties:

- [crypto.encrypt](crypto#m-encrypt)(data, key, **transformation**, options?)
- [crypto.decrypt](crypto#m-decrypt)(data, key, **transformation**, options?)

The following table lists the transformation name components supported by AutoJs6. They can be combined to form many different transformation names:

| Algorithm Name | Working Mode                                   | Padding                                                                                                                                                                                                        |
|----------|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AES      | CBC<br>CFB<br>CTR<br>CTS<br>ECB<br>OFB | ISO10126Padding<br>NoPadding<br>PKCS5Padding                                                                                                                                                                |
| AES      | GCM                                    | NoPadding                                                                                                                                                                                                   |
| AES_128  | CBC<br>ECB                             | NoPadding<br>PKCS5Padding                                                                                                                                                                                   |
| AES_128  | GCM                                    | NoPadding                                                                                                                                                                                                   |
| AES_256  | CBC<br>ECB                             | NoPadding<br>PKCS5Padding                                                                                                                                                                                   |
| AES_256  | GCM                                    | NoPadding                                                                                                                                                                                                   |
| ARC4     | ECB                                    | NoPadding                                                                                                                                                                                                   |
| ARC4     | NONE                                   | NoPadding                                                                                                                                                                                                   |
| BLOWFISH | CBC<br>CFB<br>CTR<br>CTS<br>ECB<br>OFB | ISO10126Padding<br>NoPadding<br>PKCS5Padding                                                                                                                                                                |
| ChaCha20 | NONE<br>Poly1305                       | NoPadding                                                                                                                                                                                                   |
| DES      | CBC<br>CFB<br>CTR<br>CTS<br>ECB<br>OFB | ISO10126Padding<br>NoPadding<br>PKCS5Padding                                                                                                                                                                |
| DESede   | CBC<br>CFB<br>CTR<br>CTS<br>ECB<br>OFB | ISO10126Padding<br>NoPadding<br>PKCS5Padding                                                                                                                                                                |
| RSA      | ECB<br>NONE                            | NoPadding<br>OAEPPadding<br>PKCS1Padding<br>OAEPwithSHA-1andMGF1Padding<br>OAEPwithSHA-224andMGF1Padding<br>OAEPwithSHA-256andMGF1Padding<br>OAEPwithSHA-384andMGF1Padding<br>OAEPwithSHA-512andMGF1Padding |

Taking the DES algorithm as an example, the following are all valid transformation names:

- DES
- DES/CBC/ISO10126Padding
- DES/CBC/PKCS5Padding
- DES/ECB/PKCS5Padding
- DES/ECB/NoPadding
- ... ...

## Storage

See [Storage - Storage Class](storageType) type chapter.

## AndroidBundle

See [AndroidBundle](androidBundleType) type chapter.

## AndroidRect

See [AndroidRect](androidRectType) type chapter.

## CryptoCipherOptions

See [CryptoCipherOptions](cryptoCipherOptionsType) type chapter.

## ConsoleBuildOptions

See [ConsoleBuildOptions](consoleBuildOptionsType) type chapter.

## HttpRequestBuilderOptions

See [HttpRequestBuilderOptions](httpRequestBuilderOptionsType) type chapter.

## HttpRequestHeaders

See [HttpRequestHeaders](httpRequestHeadersType) type chapter.

## HttpResponseBody

See [HttpResponseBody](httpResponseBodyType) type chapter.

## HttpResponseHeaders

See [HttpResponseHeaders](httpResponseHeadersType) type chapter.

## HttpResponse

See [HttpResponse](httpResponseType) type chapter.

## InjectableWebClient

See [InjectableWebClient](injectableWebClientType) type chapter.

## InjectableWebView

See [InjectableWebView](injectableWebViewType) type chapter.

## NoticeOptions

See [NoticeOptions](noticeOptionsType) type chapter.

## NoticeChannelOptions

See [NoticeChannelOptions](noticeChannelOptionsType) type chapter.

## NoticePresetConfiguration

See [NoticePresetConfiguration](noticePresetConfigurationType) type chapter.

## NoticeBuilder

See [NoticeBuilder](noticeBuilderType) type chapter.

## Okhttp3HttpUrl

See [Okhttp3HttpUrl](okhttp3HttpUrlType) type chapter.

## OcrOptions

See [OcrOptions](ocrOptionsType) type chapter.

## Okhttp3Request

See [Okhttp3Request](okhttp3RequestType) type chapter.

## OpenCVPoint

See [OpenCVPoint](opencvPointType) type chapter.

## OpenCVRect

See [OpenCVRect](opencvRectType) type chapter.

## OpenCVSize

See [OpenCVSize](opencvSizeType) type chapter.

## OpenCCConversion

See [OpenCCConversion](openCCConversionType) type chapter.