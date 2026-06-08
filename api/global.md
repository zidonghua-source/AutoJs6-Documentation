# Global

In JavaScript, [almost everything is an object](https://stackoverflow.com/questions/9108925/how-is-almost-everything-in-javascript-an-object/).  
The global "objects" here include [variables / methods / constructors], etc.  
Global objects are available everywhere, including ECMAScript built-in objects (such as [Number / RegExp / String], etc.).

All built-in modules in AutoJs6 support global usage, such as `app`, `images`, `device`, etc.

For convenience, some methods from AutoJs6 modules have also been globalized,  
such as `images.captureScreen()`, `dialogs.alert()`, `app.launch()`, etc.  
Globalized methods are marked with the `Global` tag.

Script files can be run directly or imported as modules (using the `require` method).  
When used as a module, `exports` and `module` are available as global objects.  
There are also some UI-mode-specific global objects, such as `activity`.

## Overwrite Protection

AutoJs6 has added overwrite protection for certain global objects and built-in modules.  
The following global declarations or assignments will cause exceptions or unexpected results:

```js
/* Using the global object "selector" as an example. */

/* Declaration is invalid. */
let selector = 1; /* Error: Variable selector has already been declared. */
const selector = 1; /* Same as above. */
var selector = 1; /* Same as above. */

/* Overwrite is invalid (non-strict mode). */
selector = 1;
typeof selector; // "function" - Silent failure, overwrite did not take effect.

/* Overwrite is invalid (strict mode). */
"use strict";
selector = 1; /* Error: Cannot modify read-only property: selector. */
```

Local scope is not affected by the above restrictions:

```js
(function () {
    let selector = 1;
    return typeof selector;
})(); // "number"
```

As of October 2022, the following objects are protected from being overwritten:

```text
selector
continuation
```

---

<p style="font: bold 2em sans-serif; color: #FF7043">global</p>

---

## [@] global

`global` is the default top-level scope object in AutoJs6 and can be used as a global object:

```js
typeof global; // "object"
typeof global.sleep; // "function"
```

You can also access the top-level scope object using the following code:

```js
runtime.topLevelScope;
```

`runtime.topLevelScope` itself has a `global` property, so the global object `global` also has one:

```js
typeof runtime.topLevelScope.global; // "object"

global.global === global; // true
global.global.global.global === global; // true
```

Properties can be added to the `global` object, and some properties can be overwritten or deleted (protected ones cannot):

```js
global.hello = "hello";
delete global.hello;
```

The `global` object itself can be overwritten:

```js
typeof global; // "object"
global = 3;
typeof global; // "number"
```

If the `global` object is accidentally overwritten (although unlikely),  
it can be accessed or restored via `runtime.topLevelScope`:

```js
global = 3; /* Overwrite the global object. */
typeof global; // "number"
typeof global.sleep; // "undefined"
typeof runtime.topLevelScope.sleep; // "function"

global = runtime.topLevelScope; /* Restore the global object. */
typeof global; // "object"
typeof global.sleep; // "function"
```

## [m] sleep

### sleep(millis)

**`Global`** **`Overload 1/3`** **`Non-UI`**

- **millis** { [number](dataTypes#number) } - Sleep duration (milliseconds)
- <ins>**returns**</ins> { [void](dataTypes#void) }

Makes the current thread sleep for a period of time.

```js
/* Sleep for 9 seconds. */
sleep(9000);
/* Sleep for 9 seconds (using scientific notation). */
sleep(9e3);
```

### sleep(millisMin, millisMax)

**`6.2.0`** **`Global`** **`Overload 2/3`** **`Non-UI`**

- **millisMin** { [number](dataTypes#number) } - Minimum sleep duration (milliseconds)
- **millisMax** { [number](dataTypes#number) } - Maximum sleep duration (milliseconds)
- <ins>**returns**</ins> { [void](dataTypes#void) }

Makes the current thread sleep for a random duration between `millisMin` and `millisMax`.

```js
/* Sleep randomly between 3 and 5 seconds. */
sleep(3e3, 5e3);
```

### sleep(millis, bounds)

**`6.2.0`** **`Global`** **`Overload 3/3`** **`Non-UI`**

- **millis** { [number](dataTypes#number) } - Sleep duration (milliseconds)
- **bounds** { [NumberString](dataTypes#NumberString) | [string](dataTypes#string) } - Floating value
- <ins>**returns**</ins> { [void](dataTypes#void) }

Makes the current thread sleep for a random duration between `millis ± bounds`.  
The `bounds` parameter accepts a [NumberString](dataTypes#NumberString) type (e.g. `"12"`), or a string prefixed with "±" to explicitly indicate the meaning (e.g. `"±12"`).

```js
/* Sleep randomly between 3 and 5 seconds (i.e., 4 ± 1 second). */
sleep(4e3, "1e3");
sleep(4e3, "±1e3"); /* Same as above. */
```

## [m+] toast

Globalized object for the toast module. See the [Toast](toast) module chapter.

## [m] toastLog

Displays a toast message and prints the message to the console.  
Equivalent to the following combination of code:

```js
toast(text, ...args);
console.log(text);
```

Therefore, the method overloads are exactly the same as [toast](#m-toast).

> Note: Although the `toast` method is asynchronous, `console.log` is synchronous, so `toastLog` is also synchronous.

### toastLog(text)

**`Global`** **`Overload 1/4`**

- **text** { [string](dataTypes#string) } - Message content
- <ins>**returns**</ins> { [void](dataTypes#void) }

> See: [toast(text)](toast#toasttext)

### toastLog(text, isLong)

**`Global`** **`Overload 2/4`**

- **text** { [string](dataTypes#string) } - Message content
  **isLong = false** { `'long'` | `'l'` | `'short'` | `'s'` | [boolean](dataTypes#boolean) } - Whether to display for a longer duration
- <ins>**returns**</ins> { [void](dataTypes#void) }

> See: [toast(text, isLong)](toast#toasttext-islong)

### toastLog(text, isLong, isForcible)

**`Global`** **`Overload 3/4`**

- **text** { [string](dataTypes#string) } - Message content
  **isLong = false** { `'long'` | `'l'` | `'short'` | `'s'` | [boolean](dataTypes#boolean) } - Whether to display for a longer duration
  **isForcible = false** { `'forcible'` | `'f'` | [boolean](dataTypes#boolean) } - Whether to forcibly overwrite the display
- <ins>**returns**</ins> { [void](dataTypes#void) }

> See: [toast(text, isLong, isForcible)](toast#toasttext-islong-isforcible)

### toastLog(text, isForcible)

**`Global`** **`Overload 4/4`**

- **text** { [string](dataTypes#string) } - Message content
- **isForcible** { `'forcible'` | `'f'` } - Forcibly overwrite the display (character identifier)
- <ins>**returns**</ins> { [void](dataTypes#void) }

> See: [toast(text, isForcible)](toast#toasttext-isforcible)

## [m+] notice

Globalized object for the notice module. See the [Notice](notice) module chapter.

## [m] random

### random()

**`Global`** **`Overload 1/2`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Same as `Math.random()`, returns a random number in the range [0, 1).

### random(min, max)

**`Global`** **`Overload 2/2`**

- **min** { [number](dataTypes#number) } - Lower bound of the random number
- **max** { [number](dataTypes#number) } - Upper bound of the random number
- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns a random number in the range [min, max].

> Note: `random(min, max)` has a closed upper bound, while `random()` has an open upper bound.

## [m] wait

### wait(condition)

**`6.2.0`** **`Global`** **`Overload 1/6`** **`A11Y?`** **`Non-UI`**

- **condition** { [(() => any)](dataTypes#function) | [PickupSelector](dataTypes#pickupselector) } - Condition to end the wait
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Blocks and waits until the condition is satisfied.  
The default wait time is 10 seconds, with a condition check interval of 200 milliseconds.  
If it times out, waiting is abandoned and a specific timeout result is returned (e.g., `false`).  
If the condition is satisfied before timeout, waiting ends and a specific success result is returned (e.g., `true`).

> Note: Unlike the "condition" in loop statements such as `while` and `for`,  
> the condition in this method is the **end-wait condition** — it keeps waiting as long as the condition is **not** met.  
> In contrast, loop statements continue looping as long as the condition **is** met.

The wait condition supports both functions and selectors.

Function example — wait until the device screen is off:

```js
wait(function () {
    return device.isScreenOff();
});

/* Using arrow function. */
wait(() => device.isScreenOff());

/* Using bind. */
wait(device.isScreenOff.bind(device));

/* Handling the result with branching. */
if (wait(() => device.isScreenOff())) {
    console.log("Successfully waited for screen to turn off");
} else {
    console.log("Timed out waiting for screen to turn off");
}
```

Selector example — wait for a control with the text "Start immediately" to appear:

```js
/* The following three formats are different representations of a Pickup selector; they have the same effect. */
wait('Start immediately');
wait(content('Start immediately')); /* Same as above. */
wait({ content: 'Start immediately' }); /* Same as above. */

/* Function form. */
wait(() => content('Start immediately').exists());
wait(() => pickup('Start immediately', '?')); /* Same as above. */

/* Simple usage of the return value from wait. */
wait('Start immediately') && toast('OK');
wait('Start immediately') ? toast('√') : toast('×');
```

Whether the wait condition is satisfied depends on the function's return value.  
For example, the wait condition is considered satisfied when the function returns `true`.

The following values are considered as "condition not satisfied":  
[ [false](dataTypes#boolean) / [null](dataTypes#null) / [undefined](dataTypes#undefined) / [NaN](https://developer.mozilla.org/en-US/docs/Glossary/NaN/) ]  
All other return values are treated as "condition satisfied" (including empty strings and the number 0).

A common mistake is when the function condition is missing a return value:

```js
wait(() => {
    if (device.isScreenOff()) {
        console.log("Screen has been successfully turned off");
    }
});
```

In the example above, the wait condition can never be satisfied because the function always returns `undefined`.

It can be fixed by adding a proper return value:

```js
wait(() => {
    if (device.isScreenOff()) {
        console.log("Screen has been successfully turned off");
        return true;
    }
});
```

> See: [pickup](uiSelectorType#m-pickup)

### wait(condition, limit)

**`6.2.0`** **`Global`** **`Overload 2/6`** **`A11Y?`** **`Non-UI`**

- **condition** { [(() => any)](dataTypes#function) | [PickupSelector](uiSelectorType#m-pickup) } - Condition to end the wait
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Extends [wait(condition)](#waitcondition) by adding a detection limit.  
Once the limit is reached, it is treated as a timeout and waiting is abandoned.  
The limit can be either a "count limit" (`limit < 100`) or a "time limit" (`limit >= 100`).

```js
/* Wait for the screen to turn off, check the screen status at most 20 times. */
wait(() => device.isScreenOff(), 20); /* limit < 100, treated as count limit. */
/* Wait for the screen to turn off, check the screen status for at most 5 seconds. */
wait(() => device.isScreenOff(), 5e3); /* limit >= 100, treated as time limit. */
```

### wait(condition, limit, interval)

**`6.2.0`** **`Global`** **`Overload 3/6`** **`A11Y?`** **`Non-UI`**

- **condition** { [(() => any)](dataTypes#function) | [PickupSelector](uiSelectorType#m-pickup) } - Condition to end the wait
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **interval** { [number](dataTypes#number) } - Wait condition detection interval
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Extends [wait(condition, limit)](#waitcondition-limit) by adding a detection interval.  
As long as the condition is not satisfied, the `wait()` method will keep checking until the condition is satisfied or the detection limit is reached.  
The `interval` parameter sets the time between checks (default is 200 milliseconds).

```text
Check condition (not met) - interval - Check condition (not met) - interval - Check condition...
```

```js
/* Wait for the screen to turn off, check at most 20 times, with 3 seconds between each check. */
wait(() => device.isScreenOff(), 20, 3e3);
/* Wait for the screen to turn off, check at most 20 times, using continuous detection (no interval). */
wait(() => device.isScreenOff(), 20, 0);
```

> Note: No interval occurs after the final condition check (whether the condition was met or the limit was reached).
>
> For example, if the condition is met on the 3rd check:  
> Check (×) - interval - Check (×) - interval - Check (√) - `wait()` ends immediately

### wait(condition, callback)

**`6.2.0`** **`Global`** **`Overload 4/6`** **`A11Y?`** **`Non-UI`**

- **condition** { [(() => T)](dataTypes#function) | [PickupSelector](uiSelectorType#m-pickup) } - Condition to end the wait
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

Extends [wait(condition)](#waitcondition) by adding a callback object.

The callback object contains two methods, `then` and `else`, corresponding to success and failure cases respectively:

```js
wait(() => device.isScreenOff(), {
    then: () => console.log("Successfully waited for screen to turn off"),
    else: () => console.log("Timed out waiting for screen to turn off"),
});
```

Both methods receive the result of the last check as an argument, which can be used directly inside the method body:

```js
/* Wait for a random number between 99.99 and 100. */
wait(() => {
    let num = Math.random() * 100;
    return num > 99.99 && num;
}, {
    then(o) {
        console.log(`Successfully obtained random number: ${o}`);
    },
    else() {
        console.log("Timed out waiting for a random number between 99.99 and 100");
    },
});
```

> Note: The parameter of the `else` callback can only be one of [ [false](dataTypes#boolean) / [null](dataTypes#null) / [undefined](dataTypes#undefined) / [NaN](https://developer.mozilla.org/en-US/docs/Glossary/NaN/) ].  
> Therefore, the parameter of `else` is almost never used.

Important: The return value of the callback methods is "transparent".  
Using a `return` statement inside a callback method directly affects the return value of `wait()` (except for `undefined`).

In the example above, neither `then` nor `else` returns a value, so `wait()` returns a `boolean` indicating whether the condition was satisfied.  
In the example below, non-`undefined` return values are added to the callbacks, and `wait()` will return those values.

```js
let result = wait(() => {
    let num = Math.random() * 100;
    return num > 99.99 && num;
}, {
    then(o) {
        console.log(`Successfully obtained random number`);
        return o;
    },
    else() {
        console.log("Timed out waiting for a random number between 99.99 and 100");
        return NaN;
    },
});
result; /* A number (e.g. 99.99732126036437) or NaN. */
```

In the example above, if the wait condition is satisfied, it returns the value from `then` (type `number`).  
If it times out, it returns the value from `else` (NaN, also type `number`).

If the `return` statement is removed from `else`, then on timeout `wait()` will return `false` (type `boolean`).

If you want to further process the return value of `wait()`, it is recommended that both callback methods return values of the same type:

```js
wait(() => {
    let num = Math.random() * 100;
    return num > 99.99 && num;
}, {
    then(o) {
        return [ o - 1, o, o + 1 ];
    },
    else() {
        /* Even on timeout, forEach can still be called. */
        return [];
    },
}).forEach(x => console.log(x));
```

### wait(condition, limit, callback)

**`6.2.0`** **`Global`** **`Overload 5/6`** **`A11Y?`** **`Non-UI`**

- **condition** { [(() => T)](dataTypes#function) | [PickupSelector](uiSelectorType#m-pickup) } - Condition to end the wait
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

Extends [wait(condition, callback)](#waitcondition-callback) by adding a detection limit.

> See: [wait(condition, limit)](#waitcondition-limit)

### wait(condition, limit, interval, callback)

**`6.2.0`** **`Global`** **`Overload 6/6`** **`A11Y?`** **`Non-UI`**

- **condition** { [(() => T)](dataTypes#function) | [PickupSelector](uiSelectorType#m-pickup) } - Condition to end the wait
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **interval** { [number](dataTypes#number) } - Wait condition detection interval
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

Extends [wait(condition, limit, callback)](#waitcondition-limit-callback) by adding a detection interval.

> See: [wait(condition, limit, interval)](#waitcondition-limit-interval)

## [m] waitForActivity

Waits for an Activity with the specified name to appear (and come to the foreground).  
This method is equivalent to `wait(() => currentActivity() === activityName, ...args)`,  
so all its overloads have the same structure as `wait`.  
To save space, only the important information (signatures, etc.) will be listed.

### waitForActivity(activityName)

**`6.2.0`** **`Global`** **`Overload 1/6`** **`A11Y?`** **`Non-UI`**

- **activityName** { [string](dataTypes#string) } - Target activity name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

> See: [wait(condition)](#waitcondition)

### waitForActivity(activityName, limit)

**`6.2.0`** **`Global`** **`Overload 2/6`** **`A11Y?`** **`Non-UI`**

- **activityName** { [string](dataTypes#string) } - Target activity name
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

> See: [wait(condition, limit)](#waitcondition-limit)

### waitForActivity(activityName, limit, interval)

**`6.2.0`** **`Global`** **`Overload 3/6`** **`A11Y?`** **`Non-UI`**

- **activityName** { [string](dataTypes#string) } - Target activity name
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **interval** { [number](dataTypes#number) } - Wait condition detection interval
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

> See: [wait(condition, limit, interval)](#waitcondition-limit-interval)

### waitForActivity(activityName, callback)

**`6.2.0`** **`Global`** **`Overload 4/6`** **`A11Y?`** **`Non-UI`**

- **activityName** { [string](dataTypes#string) } - Target activity name
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

> See: [wait(condition, callback)](#waitcondition-callback)

### waitForActivity(activityName, limit, callback)

**`6.2.0`** **`Global`** **`Overload 5/6`** **`A11Y?`** **`Non-UI`**

- **activityName** { [string](dataTypes#string) } - Target activity name
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

> See: [wait(condition, limit, callback)](#waitcondition-limit-callback)

### waitForActivity(activityName, limit, interval, callback)

**`6.2.0`** **`Global`** **`Overload 6/6`** **`A11Y?`** **`Non-UI`**

- **activityName** { [string](dataTypes#string) } - Target activity name
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **interval** { [number](dataTypes#number) } - Wait condition detection interval
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

> See: [wait(condition, limit, interval, callback)](#waitcondition-limit-interval-callback)

## [m] waitForPackage

Waits for an app with the specified package name to appear (and come to the foreground).  
This method is equivalent to `wait(() => currentPackage() === packageName, ...args)`,  
so all its overloads have the same structure as `wait`.  
To save space, only the important information will be listed.

### waitForPackage(packageName)

**`6.2.0`** **`Global`** **`Overload 1/6`** **`A11Y?`** **`Non-UI`**

- **packageName** { [string](dataTypes#string) } - Target app package name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

> See: [wait(condition)](#waitcondition)

### waitForPackage(packageName, limit)

**`6.2.0`** **`Global`** **`Overload 2/6`** **`A11Y?`** **`Non-UI`**

- **packageName** { [string](dataTypes#string) } - Target app package name
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

> See: [wait(condition, limit)](#waitcondition-limit)

### waitForPackage(packageName, limit, interval)

**`6.2.0`** **`Global`** **`Overload 3/6`** **`A11Y?`** **`Non-UI`**

- **packageName** { [string](dataTypes#string) } - Target app package name
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **interval** { [number](dataTypes#number) } - Wait condition detection interval
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

> See: [wait(condition, limit, interval)](#waitcondition-limit-interval)

### waitForPackage(packageName, callback)

**`6.2.0`** **`Global`** **`Overload 4/6`** **`A11Y?`** **`Non-UI`**

- **packageName** { [string](dataTypes#string) } - Target app package name
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

> See: [wait(condition, callback)](#waitcondition-callback)

### waitForPackage(packageName, limit, callback)

**`6.2.0`** **`Global`** **`Overload 5/6`** **`A11Y?`** **`Non-UI`**

- **packageName** { [string](dataTypes#string) } - Target app package name
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

> See: [wait(condition, limit, callback)](#waitcondition-limit-callback)

### waitForPackage(packageName, limit, interval, callback)

**`6.2.0`** **`Global`** **`Overload 6/6`** **`A11Y?`** **`Non-UI`**

- **packageName** { [string](dataTypes#string) } - Target app package name
- **limit** { [number](dataTypes#number) } - Wait condition detection limit
- **interval** { [number](dataTypes#number) } - Wait condition detection interval
- **callback** {{
    - then(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
    - else(result?: [T](dataTypes#generic))?: [R](dataTypes#generic)
- }} - Callback object when waiting ends
- <ins>**returns**</ins> { [R](dataTypes#generic) extends [void](dataTypes#void) ? [boolean](dataTypes#boolean) : [R](dataTypes#generic) }
- <ins>**template**</ins> [T](dataTypes#generic), [R](dataTypes#generic)

> See: [wait(condition, limit, interval, callback)](#waitcondition-limit-interval-callback)

## [m] exit

Stops the script execution.

### exit()

**`Global`** **`Overload 1/2`**

- <ins>**returns**</ins> { [void](dataTypes#void) }

Stops the script by throwing a `ScriptInterruptedException`.  
Therefore, wrapping the `exit()` call in a `try` block will allow the script to continue running for a short while:

```js
try {
    log('exit now');
    exit();
    log("after"); /* This will not be printed to the console. */
} catch (e) {
    e.javaException instanceof ScriptInterruptedException; // true
}
while (true) log("hello"); /* The console will print a certain number of "hello". */
```

If your script is very sensitive to the "stopped" state (i.e., you require that code after `exit()` is never executed), you can add an explicit stop check:

```js
if (!isStopped()) {
    // other code...
}
```

Therefore, the previous example with the stop check will not print "hello":

```js
try {
    log('exit now');
    exit();
} catch (_) {
    // Ignored.
}
if (!isStopped()) {
    while (true) {
        /* The console will not print "hello". */
        log("hello");
    }
}
```

In addition to [isStopped](#isstopped), you can also obtain the stopped state via the `threads` or `engines` modules:

```js
/* threads. */
if (!threads.currentThread().isInterrupted()) {
    // other code...
}

/* engines. */
if (!engines.myEngine().isStopped()) {
    // other code...
}
```

### exit(e)

**`Global`** **`Overload 2/2`**

- **e** { [OmniThrowable](omniTypes#omnithrowable) } - Exception argument
- <ins>**returns**</ins> { [void](dataTypes#void) }

Stops the script and throws the exception specified in the argument.

```js
let arg = 'hello';
try {
    if (typeof arg !== "number") {
        throw Error('arg parameter is not of type number');
    }
} catch (e) {
    exit(e);
}
```

[OmniThrowable](omniTypes#omnithrowable) supports string arguments. A string argument can be passed as the exception message to the `exit` method:

```js
let buttonText = 'Tap here to start';
if (!pickup(buttonText)) {
    exit(`"${buttonText}" button does not exist.`);
}
```

## [m] stop

### stop()

**`Global`** - <ins>**returns**</ins> { [void](dataTypes#void) }

Stops the script execution.

Alias for [exit()](#exit).

> Note: The `stop` method does not have an overload corresponding to [exit(e)](#exite).

## [m] isStopped

### isStopped()

**`Global`** **`DEPRECATED`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the main script thread has been interrupted.

Equivalent to `runtime.isInterrupted()`.

## [m] isShuttingDown

### isShuttingDown()

**`Global`** **`DEPRECATED`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the main script thread has been interrupted.

Deprecated because the method name easily causes ambiguity and confusion. It is recommended to use [isStopped()](#m-isstopped) or `runtime.isInterrupted()` instead.

## [m] isRunning

### isRunning()

**`Global`** - <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the main script thread has not been interrupted.

Equivalent to `!runtime.isInterrupted()`.

## [m] notStopped

### notStopped()

**`Global`** **`DEPRECATED`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the main script thread has not been interrupted.

Deprecated because the method name easily causes ambiguity and confusion. It is recommended to use [isRunning()](#m-isrunning) or `!runtime.isInterrupted()` instead.

## [m] requiresApi

### requiresApi(api)

**`Global`** - **api** { [number](dataTypes#number) } - Android API level

- <ins>**returns**</ins> { [void](dataTypes#void) }

Minimum API level requirement for the script to run.

For example, to require the script to run on Android API 30 (11) [R] or higher:

```js
requiresApi(30);
requiresApi(util.versionCodes.R.apiLevel); /* Same as above. */
requiresApi(android.os.Build.VERSION_CODES.R); /* Same as above. */
```

If the API level requirement is not met, the script throws an exception and stops execution.

> See also:
> - [Android API Level](apiLevel)
> - [util.versionCodes](util#versioncodes)

## [m] requiresAutojsVersion

### requiresAutojsVersion(versionName)

**`Global`** **`Overload 1/2`**

- **versionName** { [string](dataTypes#string) } - AutoJs6 version name
- <ins>**returns**</ins> { [void](dataTypes#void) }

Minimum AutoJs6 version requirement (by version name) for the script to run.

```js
requiresAutojsVersion("6.2.0");
```

You can check the AutoJs6 version name via `autojs.versionName`.

> See: [autojs.versionName](autojs#versionname)

### requiresAutojsVersion(versionCode)

**`Global`** **`Overload 2/2`**

- **versionCode** { [number](dataTypes#number) } - AutoJs6 version code
- <ins>**returns**</ins> { [void](dataTypes#void) }

Minimum AutoJs6 version requirement (by version code) for the script to run.

```js
requiresAutojsVersion(1024);
```

You can check the AutoJs6 version code via `autojs.versionCode`.

> See: [autojs.versionCode](autojs#versioncode)

## [m] importPackage

### importPackage(...pkg)

**`Global`** - **pkg** { ...( [string](dataTypes#string) | [object](dataTypes#object) ) } - Java packages to import

- <ins>**returns**</ins> { [void](dataTypes#void) }

```js
/* Import one Java package. */

importPackage(java.lang);
importPackage('java.lang'); /* Same as above. */

/* Import multiple Java packages. */

importPackage(java.io);
importPackage(java.lang);
importPackage(java.util);

importPackage(java.io, java.lang, java.util); /* Same as above. */
``` 

> See: [Accessing Java Packages and Classes](scriptingJava#accessing-java-packages-and-classes)

## [m] importClass

### importClass(...cls)

**`Global`** - **cls** { ...( [string](dataTypes#string) | [object](dataTypes#object) ) } - Java classes to import

- <ins>**returns**</ins> { [void](dataTypes#void) }

```js
/* Import one Java class. */

importClass(java.lang.Integer);
importClass('java.lang.Integer'); /* Same as above. */

/* Import multiple Java classes. */

importClass(java.io.File);
importClass(java.lang.Integer);
importClass(java.util.HashMap);

importClass(
    java.io.File,
    java.lang.Integer,
    java.util.HashMap,
); /* Same as above. */
``` 

> See: [Accessing Java Packages and Classes](scriptingJava#accessing-java-packages-and-classes)

## [m] currentPackage

### currentPackage()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) }

Gets the most recently detected app package name and treats it as the currently running app's package name.

## [m] currentActivity

### currentActivity()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) }

Gets the most recently detected activity name and treats it as the currently running activity name.

## [m] setClip

### setClip(text)

**`Global`** - **text** { [string](dataTypes#string) } - Clipboard content

- <ins>**returns**</ins> { [void](dataTypes#void) }

Sets the system clipboard content.

> See: [getClip](#m-getclip)

## [m] getClip

### getClip()

**`Global`** - <ins>**returns**</ins> { [string](dataTypes#string) } - System clipboard content

Note that starting from [Android API 29 (10) [Q]](apiLevel), access to clipboard data is restricted:

To better protect user privacy, clipboard data can only be accessed by the default input method and the currently focused foreground app.

```js
setClip("test");

/* Android 10 and below: prints "test". */
/* Android 10 and above: prints "test" if AutoJs6 is in the foreground, otherwise prints an empty string. */
console.log(getClip());
```

> See: [setClip](#m-setclip)

> See: [Android Docs](https://developer.android.com/about/versions/10/privacy/changes#clipboard-data)

## [m] selector

### selector()

**`Global`** - <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Builds an "empty" [selector](uiSelectorType).

## [m] pickup

Pickup selector (also called picker) is a highly encapsulated mixed-form selector used for quick operations during control filtering and result processing.  
It supports [ mixed selector formats / control compass / result filtering / parameterized calls ], etc.

See [UiSelector.pickup](uiSelectorType#m-pickup).

## [m] detect

Control detection.

Detection is equivalent to performing a series of combined operations on controls (compass positioning, result filtering, parameterized calls, callback handling).

See [UiObject#detect](uiObjectType#m-detect).

## [m] existsAll

### existsAll(...selectors)

**`Global`** - **selectors** { [...](documentation#可变参数)[PickupSelector](dataTypes#pickupselector)[[]](documentation#可变参数) } - Mixed selector arguments

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - All selectors satisfy the "exists" condition

All provided selector arguments satisfy the "exists" condition, i.e., `selector.exists() === true`.

For example, to require that the current active window simultaneously contains controls matching the following three selectors:

1. contentMatch(/^Start.*/)
2. descMatch(/descriptions?/)
3. content('Click to continue')

```js
console.log(existsAll(contentMatch(/^Start.*/), descMatch(/descriptions?/), content('Click to continue'))); /* e.g. true */
```

Because mixed selector arguments support simplified forms for the content family of selectors, the above example can also be rewritten as:

```js
console.log(existsAll(/^Start.*/, descMatch(/descriptions?/), 'Click to continue')); /* e.g. true */
```

Traditional logical form equivalent to this method:

```js
console.log(contentMatch(/^Start.*/).exists()
    && descMatch(/descriptions?/).exists()
    && content('Click to continue').exists()); /* e.g. true */
```

## [m] existsOne

### existsOne(...selectors)

**`Global`** - **selectors** { [...](documentation#可变参数)[PickupSelector](dataTypes#pickupselector)[[]](documentation#可变参数) } - Mixed selector arguments

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - At least one selector satisfies the "exists" condition

Any of the provided selector arguments satisfies the "exists" condition, i.e., `selector.exists() === true`.

For example, to require that the current active window contains at least one control matching any of the following selectors:

1. contentMatch(/^Start.*/)
2. descMatch(/descriptions?/)
3. content('Click to continue')

```js
console.log(existsOne(contentMatch(/^Start.*/), descMatch(/descriptions?/), content('Click to continue'))); /* e.g. true */
```

Because mixed selector arguments support simplified forms for the content family of selectors, the above example can also be rewritten as:

```js
console.log(existsOne(/^Start.*/, descMatch(/descriptions?/), 'Click to continue')); /* e.g. true */
```

Traditional logical form equivalent to this method:

```js
console.log(contentMatch(/^Start.*/).exists()
    || descMatch(/descriptions?/).exists()
    || content('Click to continue').exists()); /* e.g. true */
```

## [m] cX

Horizontal coordinate scaling.

### cX()

**`6.2.0`** **`Global`** **`Overload 1/5`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

When called with no arguments, returns the current device width.

```js
console.log(cX() === device.width); // true
```

### cX(x, base)

**`6.2.0`** **`Global`** **`Overload 2/4`**

- **x** { [number](dataTypes#number) } - Absolute coordinate value
- **[ base = 720 ]** { [number](dataTypes#number) } - Coordinate base value
- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the horizontal coordinate value converted from the base.

For example, 100 pixels on a device with width `1096` will be converted to different values on devices with other widths:

```js
/* On a device with width 1096 pixels. */
cX(100, 1096); // 100

/* On a device with width 1080 pixels. */
cX(100, 1096); // 99

/* On a device with width 720 pixels. */
cX(100, 1096); // 66

/* On a device with width 540 pixels. */
cX(100, 1096); // 49
```

In the example above, `1096` is the base. The default base is `720`. To set a custom default base, use the following method:

```js
cX(100); /* Equivalent to cX(100, 720). */
setScaleBaseX(1096);
cX(100); /* Equivalent to cX(100, 1096). */
```

The default base can be modified at most once.

### cX(x, isRatio)

**`6.2.0`** **`Global`** **`Overload 3/4`**

- **x** { [number](dataTypes#number) } - Absolute coordinate value or screen width percentage
- **[ isRatio = 'auto' ]** { `'auto'` | [boolean](dataTypes#boolean) } - Whether to force `x` to be treated as a percentage
- <ins>**returns**</ins> { [number](dataTypes#number) }

The `isRatio` parameter defaults to `'auto'`, meaning whether `x` is treated as a percentage is automatically determined by the range of the `x` parameter.  
That is, when the `x` parameter satisfies `-1 < x < 1`, `x` will be treated as a screen width percentage; otherwise it will be treated as an absolute coordinate value.

When `isRatio` is `true`, the `x` parameter is forcibly treated as a percentage. For example, `cX(2, true)` means twice the screen width; the meaning of `2` is no longer a pixel value.

When `isRatio` is `false`, the `x` parameter is forcibly treated as an absolute coordinate value. For example, `cX(0.5, false)` means a `0.5` pixel value; the meaning is no longer a percentage.

### cX(x)

**`6.2.0`** **`Global`** **`Overload 4/4`**

- **x** { [number](dataTypes#number) } - Absolute coordinate value or screen width percentage
- <ins>**returns**</ins> { [number](dataTypes#number) }

When the parameter `x` satisfies `-1 < x < 1`, it is equivalent to `cX(x, /* isRatio = */ true)`, i.e., `x` will be treated as a screen width percentage.

When the parameter `x` satisfies `x <= -1 | x >= 1`, it is equivalent to `cX(x, /* base = */ 720)`, i.e., `x` will be treated as an absolute coordinate value. In addition, the `base` parameter may be modified by methods such as `setScaleBaseX`; `720` is its default value.

## [m] cY

Vertical coordinate scaling.

### cY()

**`6.2.0`** **`Global`** **`Overload 1/5`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

When called with no arguments, returns the current device height.

```js
console.log(cY() === device.height); // true
```

### cY(y, base)

**`6.2.0`** **`Global`** **`Overload 2/4`**

- **y** { [number](dataTypes#number) } - Absolute coordinate value
- **[ base = 1280 ]** { [number](dataTypes#number) } - Coordinate base value
- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the vertical coordinate value converted from the base.

For example, 100 pixels on a device with height `2560` will be converted to different values on devices with other heights:

```js
/* On a device with height 2560 pixels. */
cY(100, 2560); // 100

/* On a device with height 1920 pixels. */
cY(100, 2560); // 75

/* On a device with height 1280 pixels. */
cY(100, 2560); // 50

/* On a device with height 960 pixels. */
cY(100, 2560); // 38
```

In the example above, `2560` is the base. The default base is `1280`. To set a custom default base, use the following method:

```js
cY(100); /* Equivalent to cY(100, 1280). */
setScaleBaseY(2560);
cY(100); /* Equivalent to cY(100, 2560). */
```

The default base can be modified at most once.

### cY(y, isRatio)

**`6.2.0`** **`Global`** **`Overload 3/4`**

- **y** { [number](dataTypes#number) } - Absolute coordinate value or screen height percentage
- **[ isRatio = 'auto' ]** { `'auto'` | [boolean](dataTypes#boolean) } - Whether to force `y` to be treated as a percentage
- <ins>**returns**</ins> { [number](dataTypes#number) }

The `isRatio` parameter defaults to `'auto'`, meaning whether `y` is treated as a percentage is automatically determined by the range of the `y` parameter.  
That is, when the `y` parameter satisfies `-1 < y < 1`, `y` will be treated as a screen height percentage; otherwise it will be treated as an absolute coordinate value.

When `isRatio` is `true`, the `y` parameter is forcibly treated as a percentage. For example, `cY(2, true)` means twice the screen height; the meaning of `2` is no longer a pixel value.

When `isRatio` is `false`, the `y` parameter is forcibly treated as an absolute coordinate value. For example, `cY(0.5, false)` means a `0.5` pixel value; the meaning is no longer a percentage.

### cY(y)

**`6.2.0`** **`Global`** **`Overload 4/4`**

- **y** { [number](dataTypes#number) } - Absolute coordinate value or screen height percentage
- <ins>**returns**</ins> { [number](dataTypes#number) }

When the parameter `y` satisfies `-1 < y < 1`, it is equivalent to `cY(y, /* isRatio = */ true)`, i.e., `y` will be treated as a screen height percentage.

When the parameter `y` satisfies `y <= -1 | y >= 1`, it is equivalent to `cY(y, /* base = */ 1280)`, i.e., `y` will be treated as an absolute coordinate value. In addition, the `base` parameter may be modified by methods such as `setScaleBaseY`; `1280` is its default value.

## [m] cYx

Vertical coordinate scaling measured by the horizontal coordinate.

A coordinate scale that is independent of device height and related to device width.

For example, `cYx(0.5, '9:16')` produces identical results on the following 5 devices (distinguished by resolution):

```text
1. 1080 × 1920
4. 1080 × 2160
5. 1080 × 2340
3. 1080 × 2520
2. 1080 × 2560
```

Because all devices share the same width, the result of `cYx` is height-independent.

Calculation result:

```js
1080 * 0.5 * 16 / 9; // 960
```

Imagine the following scenario: an app page can scroll down to display more content. There is a button `BTN` in the upper half of the screen, at a distance `H` from the top edge of the screen. Another device has the same screen width as the current device but greater height (the screen is vertically longer). At this point, the button `BTN` is still at distance `H` from the top edge of the screen; only more content is displayed below the screen.  
Therefore, `cYx` scaling can be used to represent the position of button `BTN`, such as `cYx(0.2, 1080 / 1920)` or `cYx(0.2, 9 / 16)` or `cYx(0.2, '9:16')`.

In the example above, `0.2` is a relative value relative to the current device screen height, so the second parameter corresponds to the device aspect ratio value.  
If an absolute coordinate value (`Y` coordinate value) is used, such as `384`, then the second parameter corresponds to the device screen width value:

| 1st Parameter | 2nd Parameter |        Example        |
|:-------:|:-------:|:----------------:|
| Y coordinate percentage |  Device aspect ratio  | cYx(0.2, '9:16') |
|  Y coordinate value  |  Device width value  |  cYx(384, 1096)  |

### cYx(coordinateY, baseX)

**`6.2.0`** **`Global`** **`Overload [1(A)]/3`**

- **coordinateY** { [number](dataTypes#number) } - Vertical coordinate value
- **[ baseX = 720 ]** { [number](dataTypes#number) } - Horizontal coordinate base
- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the vertical coordinate value converted from the horizontal coordinate base.

For example, a height of 512 pixels on a device with width `1096` will be converted to different values on devices with other widths:

```js
/* On a device with width 1096 pixels. */
cYx(512, 1096); // 512

/* On a device with width 1080 pixels. */
cYx(512, 1096); // 505

/* On a device with width 720 pixels. */
cYx(512, 1096); // 336

/* On a device with width 540 pixels. */
cYx(512, 1096); // 252
```

In the example above, `1096` is the base. The default base is `720`. To set a custom default base, use the following method:

```js
cYx(512); /* Equivalent to cYx(512, 720). */
setScaleBaseX(1096);
cYx(512); /* Equivalent to cYx(512, 1096). */
```

The default base can be modified at most once.

### cYx(percentY, ratio)

**`6.2.0`** **`Global`** **`Overload [1(B)]/3`**

- **percentY** { [number](dataTypes#number) } - Vertical coordinate percentage
- **[ ratio = '9:16' ]** { [number](dataTypes#number) | [string](dataTypes#string) } - Device aspect ratio
- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns a new vertical coordinate value converted from the device aspect ratio.

For example, a height of 512 pixels (i.e., 0.2 times the screen height) on a device with width and height `1096` and `2560` respectively will be converted to different values on devices with other widths:

```js
/* On a device with width 1096 pixels. */
cYx(0.2, 1096 / 2560); // 512

/* On a device with width 1080 pixels. */
cYx(0.2, 1096 / 2560); // 505

/* On a device with width 720 pixels. */
cYx(0.2, 1096 / 2560); // 336

/* On a device with width 540 pixels. */
cYx(0.2, 1096 / 2560); // 252
```

In the example above, `1096 / 2560` is the base. The default base is `720 / 1280`. To set a custom default base, use the following method:

```js
cYx(0.2); /* Equivalent to cYx(0.2, 720 / 1280). */
setScaleBases(1096, 2560);
cYx(0.2); /* Equivalent to cYx(0.2, 1096 / 2560). */
```

The default base can be modified at most once.

### cYx(y, isRatio)

**`6.2.0`** **`Global`** **`Overload 2/3`**

- **y** { [number](dataTypes#number) } - Absolute coordinate value or screen height percentage
- **[ isRatio = 'auto' ]** { `'auto'` | [boolean](dataTypes#boolean) } - Whether to force `y` to be treated as a percentage
- <ins>**returns**</ins> { [number](dataTypes#number) }

The `isRatio` parameter defaults to `'auto'`, meaning whether `y` is treated as a percentage is automatically determined by the range of the `y` parameter.  
That is, when the `y` parameter satisfies `-1 < y < 1`, `y` will be treated as a screen height percentage; otherwise it will be treated as an absolute coordinate value.

When `isRatio` is `true`, the `y` parameter is forcibly treated as a percentage. For example, `cYx(2, true)` means twice the screen height; the meaning of `2` is no longer a pixel value.

When `isRatio` is `false`, the `y` parameter is forcibly treated as an absolute coordinate value. For example, `cYx(0.5, false)` means a `0.5` pixel value; the meaning is no longer a percentage.

### cYx(y)

**`6.2.0`** **`Global`** **`Overload 3/3`**

- **y** { [number](dataTypes#number) } - Absolute coordinate value or screen height percentage
- <ins>**returns**</ins> { [number](dataTypes#number) }

When the parameter `y` satisfies `-1 < y < 1`, it is equivalent to `cY(y, /* isRatio = */ true)`, i.e., `y` will be treated as a screen height percentage.

When the parameter `y` satisfies `y <= -1 | y >= 1`, it is equivalent to `cY(y, /* base = */ 720)`, i.e., `y` will be treated as an absolute coordinate value. In addition, the `base` parameter may be modified by methods such as `setScaleBaseX`; `720` is its default value.

```js
cYx(0.3); /* Equivalent to cYx(0.3, '9:16'). */
cYx(384); /* Equivalent to cYx(384, 720). */
```

## [m] cXy

Horizontal coordinate scaling measured by the vertical coordinate.

A coordinate scale that is independent of device width and related to device height.

For example, `cXy(0.5, '9:16')` produces identical results on the following 5 devices (distinguished by resolution):

```text
1. 1080 × 1920
4. 1096 × 1920
5. 720 × 1920
3. 540 × 1920
2. 960 × 1920
```

Because all devices share the same height, the result of `cXy` is width-independent.

Calculation result:

```js
1920 * 0.5 * 9 / 16; // 540
```

Imagine the following scenario: an app page can scroll right to display more content. There is a button `BTN` in the left half of the screen, at a distance `W` from the left edge of the screen. Another device has the same screen height as the current device but greater width (the screen is horizontally longer). At this point, the button `BTN` is still at distance `W` from the left edge of the screen; only more content is displayed to the right of the screen.  
Therefore, `cXy` scaling can be used to represent the position of button `BTN`, such as `cXy(0.2, 1080 / 1920)` or `cXy(0.2, 9 / 16)` or `cXy(0.2, '9:16')`.

In the example above, `0.2` is a relative value relative to the current device screen width, so the second parameter corresponds to the device aspect ratio value.  
If an absolute coordinate value (`X` coordinate value) is used, such as `384`, then the second parameter corresponds to the device screen height value:

| 1st Parameter | 2nd Parameter |        Example        |
|:-------:|:-------:|:----------------:|
| X coordinate percentage |  Device aspect ratio  | cXy(0.2, '9:16') |
|  X coordinate value  |  Device height value  |  cXy(384, 2560)  |

### cXy(coordinateX, baseY)

**`6.2.0`** **`Global`** **`Overload [1(A)]/3`**

- **coordinateX** { [number](dataTypes#number) } - Horizontal coordinate value
- **[ baseY = 1280 ]** { [number](dataTypes#number) } - Vertical coordinate base
- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the horizontal coordinate value converted from the vertical coordinate base.

For example, a width of 512 pixels on a device with height `2560` will be converted to different values on devices with other heights:

```js
/* On a device with height 2560 pixels. */
cXy(512, 2560); // 512

/* On a device with height 1920 pixels. */
cXy(512, 2560); // 384

/* On a device with height 1280 pixels. */
cXy(512, 2560); // 256

/* On a device with height 960 pixels. */
cXy(512, 2560); // 192
```

In the example above, `2560` is the base. The default base is `1280`. To set a custom default base, use the following method:

```js
cXy(512); /* Equivalent to cXy(512, 1280). */
setScaleBaseY(2560);
cXy(512); /* Equivalent to cXy(512, 2560). */
```

The default base can be modified at most once.

### cXy(percentX, ratio)

**`6.2.0`** **`Global`** **`Overload [1(B)]/3`**

- **percentX** { [number](dataTypes#number) } - Horizontal coordinate percentage
- **[ ratio = '9:16' ]** { [number](dataTypes#number) | [string](dataTypes#string) } - Device aspect ratio
- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns a new horizontal coordinate value converted from the device aspect ratio.

For example, a width of 548 pixels (i.e., 0.5 times the screen width) on a device with height and width `1096` and `2560` respectively will be converted to different values on devices with other heights:

```js
/* On a device with height 2560 pixels. */
cXy(0.5, 1096 / 2560); // 548

/* On a device with height 1920 pixels. */
cXy(0.5, 1096 / 2560); // 411

/* On a device with height 1280 pixels. */
cXy(0.5, 1096 / 2560); // 274

/* On a device with height 960 pixels. */
cXy(0.5, 1096 / 2560); // 206
```

In the example above, `1096 / 2560` is the base. The default base is `720 / 1280`. To set a custom default base, use the following method:

```js
cXy(0.5); /* Equivalent to cXy(0.5, 720 / 1280). */
setScaleBases(1096, 2560);
cXy(0.5); /* Equivalent to cXy(0.5, 1096 / 2560). */
```

The default base can be modified at most once.

### cXy(x, isRatio)

**`6.2.0`** **`Global`** **`Overload 2/3`**

- **x** { [number](dataTypes#number) } - Absolute coordinate value or screen width percentage
- **[ isRatio = 'auto' ]** { `'auto'` | [boolean](dataTypes#boolean) } - Whether to force `x` to be treated as a percentage
- <ins>**returns**</ins> { [number](dataTypes#number) }

The `isRatio` parameter defaults to `'auto'`, meaning whether `x` is treated as a percentage is automatically determined by the range of the `x` parameter.  
That is, when the `x` parameter satisfies `-1 < x < 1`, `x` will be treated as a screen width percentage; otherwise it will be treated as an absolute coordinate value.

When `isRatio` is `true`, the `x` parameter is forcibly treated as a percentage. For example, `cXy(2, true)` means twice the screen width; the meaning of `2` is no longer a pixel value.

When `isRatio` is `false`, the `x` parameter is forcibly treated as an absolute coordinate value. For example, `cXy(0.5, false)` means a `0.5` pixel value; the meaning is no longer a percentage.

### cXy(x)

**`6.2.0`** **`Global`** **`Overload 3/3`**

- **x** { [number](dataTypes#number) } - Absolute coordinate value or screen width percentage
- <ins>**returns**</ins> { [number](dataTypes#number) }

When the parameter `x` satisfies `-1 < x < 1`, it is equivalent to `cY(x, /* isRatio = */ true)`, i.e., `x` will be treated as a screen width percentage.

When the parameter `x` satisfies `x <= -1 | x >= 1`, it is equivalent to `cY(x, /* base = */ 720)`, i.e., `x` will be treated as an absolute coordinate value. In addition, the `base` parameter may be modified by methods such as `setScaleBaseX`; `720` is its default value.

```js
cXy(0.3); /* Equivalent to cXy(0.3, '9:16'). */
cXy(384); /* Equivalent to cXy(384, 720). */
```

## [m+] species

### species(o)

**`Global`**

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [string](dataTypes#string) }

Returns the "species" of any object, such as `Object`, `Array`, `Number`, `String`, `RegExp`, etc.

Internal implementation code summary:

```js
Object.prototype.toString.call(o).slice('[Object\x20'.length, ']'.length * -1);
```

Example:

```js
species('xyz'); // String
species(20); // Number
species(20n); // BigInt
species(true); // Boolean
species(undefined); // Undefined
species(null); // Null
species(() => null); // Function
species({ a: 'Apple' }); // Object
species([ 5, 10, 15 ]); // Array
species(/^\d{8,11}$/); // RegExp
species(new Date()); // Date
species(new TypeError()); // Error
species(new Map()); // Map
species(new Set()); // Set
species(<text/>); // XML
species(org.autojs.autojs6); // JavaPackage
species(org.autojs.autojs6.R); // JavaClass
```

To check whether an object is of a specific "species", you can use extension methods in the form `species.isXxx`:

```js
species.isObject(23); // false
species.isNumber(23); // true
species.isRegExp(/test$/); // true
```

### [m] isArray

#### isArray(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Array`.

### [m] isArrayBuffer

#### isArrayBuffer(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `ArrayBuffer`.

### [m] isBigInt

#### isBigInt(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `BigInt`.

### [m] isBoolean

#### isBoolean(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Boolean`.

### [m] isContinuation

#### isContinuation(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Continuation`.

### [m] isDataView

#### isDataView(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `DataView`.

### [m] isDate

#### isDate(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Date`.

### [m] isError

#### isError(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Error`.

### [m] isFloat32Array

#### isFloat32Array(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Float32Array`.

### [m] isFloat64Array

#### isFloat64Array(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Float64Array`.

### [m] isFunction

#### isFunction(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Function`.

### [m] isHTMLDocument

#### isHTMLDocument(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `HTMLDocument`.

### [m] isInt16Array

#### isInt16Array(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Int16Array`.

### [m] isInt32Array

#### isInt32Array(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Int32Array`.

### [m] isInt8Array

#### isInt8Array(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Int8Array`.

### [m] isJavaObject

#### isJavaObject(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `JavaObject`.

### [m] isJavaPackage

#### isJavaPackage(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `JavaPackage`.

### [m] isMap

#### isMap(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Map`.

### [m] isNamespace

#### isNamespace(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Namespace`.

### [m] isNull

#### isNull(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Null`.

### [m] isNumber

#### isNumber(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Number`.

### [m] isObject

#### isObject(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Object`.

### [m] isQName

#### isQName(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `QName`.

### [m] isRegExp

#### isRegExp(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `RegExp`.

### [m] isSet

#### isSet(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Set`.

### [m] isString

#### isString(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `String`.

### [m] isUint16Array

#### isUint16Array(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Uint16Array`.

### [m] isUint32Array

#### isUint32Array(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Uint32Array`.

### [m] isUint8Array

#### isUint8Array(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Uint8Array`.

### [m] isUint8ClampedArray

#### isUint8ClampedArray(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Uint8ClampedArray`.

### [m] isUndefined

#### isUndefined(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Undefined`.

### [m] isWeakMap

#### isWeakMap(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `WeakMap`.

### [m] isWeakSet

#### isWeakSet(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `WeakSet`.

### [m] isWindow

#### isWindow(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `Window`.

### [m] isXML

#### isXML(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `XML`.

### [m] isXMLList

#### isXMLList(o)

- **o** { [any](dataTypes#any) } - Any object
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Checks whether the object's "species" is `XMLList`.

## [p] WIDTH

**`6.2.0`** **`Global`** **`Getter`**

- **&lt;get&gt;** [number](dataTypes#number)

Alias property for [device.width](device#p-width).

## [p] HEIGHT

**`6.2.0`** **`Global`** **`Getter`**

- **&lt;get&gt;** [number](dataTypes#number)

Alias property for [device.height](device#p-height).

## [p+] R

Using static integers from subclasses of the R class in code allows access to [application resources](glossaries#应用资源). For details, see the [Resource ID](glossaries#资源-ID) glossary.

### [p+] anim

**`6.2.0`** **`Global`**

Animation resources.

Defines predetermined animations.  
Tween animations are stored in `res/anim/` and can be accessed via the `R.anim` property.  
Frame animations are stored in `res/drawable/` and can be accessed via the `R.drawable` property.

```js
'ui';

ui.layout(<vertical id="main">
    <vertical width="100" height="100" bg="#00695C"></vertical>
</vertical>);

const AnimationUtils = android.view.animation.AnimationUtils;

const mContentContainer = ui.main;
const mSlideDownAnimation = AnimationUtils.loadAnimation(context, R.anim.slide_down);
mSlideDownAnimation.setDuration(2000);
mContentContainer.startAnimation(mSlideDownAnimation);
```

### [p+] array

**`6.2.0`** **`Global`**

Static resources.

XML resources that provide arrays.

```js
dialogs.build({
    title: R.string.text_pinch_to_zoom,
    items: R.array.values_editor_pinch_to_zoom_strategy,
    itemsSelectMode: 'single',
    itemsSelectedIndex: defSelectedIndex,
    positive: 'OK',
}).on('single_choice', function (idx, item) {
    toastLog(`${idx}: ${item}`);
}).show();
```

### [p+] bool

**`6.2.0`** **`Global`**

Static resources.

XML resources that contain boolean values.

```js
console.log(context.getResources().getBoolean(R.bool.pref_auto_check_for_updates));
```

### [p+] color

**`6.2.0`** **`Global`**

Static resources.

XML resources that contain color values (hexadecimal colors).

```js
console.log(colors.toString(context.getColor(R.color.console_view_warn), 6)); // #1976D2
```

### [p+] dimen

**`6.2.0`** **`Global`**

Static resources.

XML resources that contain dimension values (and measurement units).

```js
console.log(context.getResources().getDimensionPixelSize(R.dimen.textSize_item_property)); // e.g. 28
```

### [p+] drawable

**`6.2.0`** **`Global`**

Drawable resources.

Defines various graphics using bitmaps or XML.  
Stored in `res/drawable/` and accessible via the `R.drawable` property.

```js
/* Draw a light green bell icon. */

'ui';

ui.layout(<vertical bg="#FFFFFF">
    <img id="img" tint="#9CCC65"/>
</vertical>);

ui.img.setImageResource(R.drawable.ic_ali_notification);
```

### [p+] id

**`6.2.0`** **`Global`**

Static resources.

XML resources that provide unique identifiers for application resources and components.

```js
'ui';

ui.layout(<vertical bg="#FFFFFF">
    <text id="txt" size="30"/>
</vertical>);

let childCount = ui.txt.getRootView().findViewById(R.id.action_bar_root).getChildCount(); // e.g 2
ui.txt.setText(`Child count is ${childCount}`);
```

### [p+] integer

**`6.2.0`** **`Global`**

Static resources.

XML resources that contain integer values.

```js
console.log(context.getResources().getInteger(R.integer.layout_node_info_view_decoration_line)); // 2
```

### [p+] layout

**`6.2.0`** **`Global`**

Layout resources.

Defines the layout of the application interface.  
Stored in `res/layout/` and accessible via the `R.layout` property.

```js
'ui';

activity.setContentView(R.layout.activity_log);
```

### [p+] menu

**`6.2.0`** **`Global`**

Menu resources.

Defines the content of application menus.  
Stored in `res/menu/` and accessible via the `R.menu` property.

```js
'ui';

ui.layout(<vertical bg="#FFFFFF">
    <text id="txt" size="30"/>
</vertical>);

const PopupMenu = android.widget.PopupMenu;

let childCount = ui.txt.getRootView().findViewById(R.id.action_bar_root).getChildCount(); // e.g 2
ui.txt.setText(`Child count is ${childCount}`);

let popupMenu = new PopupMenu(context, ui.txt);
popupMenu.inflate(R.menu.menu_script_options);
popupMenu.show();
```

### [p+] plurals

**`6.2.0`** **`Global`**

Static resources.

Defines resource plurals.

```js
console.log(context.getResources().getQuantityString(
    R.plurals.text_already_stop_n_scripts,
    new java.lang.Integer(1),
    new java.lang.Integer(1))); // e.g. 1 script stopped
console.log(context.getResources().getQuantityString(
    R.plurals.text_already_stop_n_scripts,
    new java.lang.Integer(3),
    new java.lang.Integer(3))); // e.g. 3 scripts stopped
```

### [p+] string

**`6.2.0`** **`Global`**

String resources.

Defines strings.  
Stored in `res/values/` and accessible via the `R.string` property.

```js
console.log(context.getString(R.string.app_name)); // AutoJs6
```

### [p+] strings

**`6.2.0`** **`Global`**

String resources.

Same as [R.string](#p-string).  
Because in `TypeScript Declarations (TS declaration files)`, `string` is a reserved keyword and cannot be used as a class name, the `R.strings` alias class is specially provided to enable IDE intelligent completion.

```js
console.log(context.getString(R.strings.app_name)); // AutoJs6
console.log(context.getString(R.string.app_name)); /* Same as above, but IDE cannot provide intelligent completion. */
```

### [p+] style

**`6.2.0`** **`Global`**

Style resources.

Defines the appearance and format of interface elements.  
Stored in `res/values/` and accessible via the `R.style` property.

```js
'ui';

const MaterialDialog = com.afollestad.materialdialogs.MaterialDialog;
const ContextThemeWrapper = android.view.ContextThemeWrapper;

new MaterialDialog.Builder(new ContextThemeWrapper(activity, R.style.Material3DarkTheme))
    .title('Hello')
    .content('This is a test for showing a dialog with material 3 dark theme.')
    .positiveText('OK')
    .onPositive(() => ui.finish())
    .cancelable(false)
    .build()
    .show();
```