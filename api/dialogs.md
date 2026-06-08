# Dialogs

---

<p style="font: italic 1em sans-serif; color: #78909C">This chapter is pending supplementation or improvement...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Oct 22, 2022.</p>

---

The `dialogs` module provides simple dialog support, allowing interaction with the user through dialogs. The simplest example is:

```js
alert("Hello");
```

This code will show a message dialog displaying "Hello", and continue running after the user clicks "OK". A slightly more complex example:

```js
var clear = confirm("Clear all cache?");
if (clear) {
    alert("Cleared successfully!");
}
```

`confirm()` shows a dialog and lets the user choose "Yes" or "No". It returns `true` if "Yes" is selected.

**Important note**: In UI mode, dialogs cannot be used in the usual blocking way. You should use callback functions or [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) form instead. This can be a bit confusing at first. Example:

```js
"ui";

// Callback form
confirm("Clear all cache?", function(clear) {
    if (clear) {
        alert("Cleared successfully!");
    }
});

// Promise form
confirm("Clear all cache?")
    .then(clear => {
        if (clear) {
            alert("Cleared successfully!");
        }
    });
```

## dialogs.alert(title[, content, callback])

* `title` {string} Title of the dialog.
* `content` {string} Optional. Content of the dialog. Default is empty.
* `callback` {Function} Optional callback function, called when the user clicks OK (mainly used in UI mode).

Displays a prompt dialog containing only an "OK" button. The script will pause until the user clicks OK.

This function can also be used globally.

```js
alert("An error occurred~", "Unknown error, please contact the script author");
```

In UI mode, this function returns a `Promise`. For example:

```js
"ui";
alert("Hey hey hey").then(() => {
    // Executes after clicking OK
});
```

## dialogs.confirm(title[, content, callback])

* `title` {string} Title of the dialog.
* `content` {string} Optional. Content of the dialog. Default is empty.
* `callback` {Function} Optional callback. Called when the user clicks a button (mainly for UI mode).

Displays a dialog with "OK" and "Cancel" buttons. Returns `true` if the user clicks "OK", otherwise `false`.

This function can also be used globally.

In UI mode, it returns a `Promise`. Example:

```js
"ui";
confirm("Are you sure?").then(value => {
    // Executes after clicking OK or Cancel. `value` is true or false.
});
```

## dialogs.rawInput(title[, prefill, callback])

* `title` {string} Title of the dialog.
* `prefill` {string} Optional initial content for the input box. Default is empty.
* `callback` {Function} Optional callback. Called when the user clicks OK (mainly for UI mode).

Shows a dialog containing an input box. Waits for the user to enter content and returns the entered string when they click OK. Returns `null` if the user cancels.

This function can also be used globally.

```js
var name = rawInput("Please enter your name", "Xiao Ming");
alert("Your name is " + name);
```

In UI mode, it returns a `Promise`. Example:

```js
"ui";
rawInput("Please enter your name", "Xiao Ming").then(name => {
    alert("Your name is " + name);
});
```

It can also be used with a callback:

```js
rawInput("Please enter your name", "Xiao Ming", name => {
    alert("Your name is " + name);
});
```

## dialogs.input(title[, prefill, callback])

Equivalent to `eval(dialogs.rawInput(title, prefill, callback))`. The difference from `rawInput` is that the input string is evaluated with `eval` before being returned (the result may not be a string).

This function can be used to input numbers, arrays, etc. Example:

```js
var age = dialogs.input("Please enter your age", "18");
// new Date().getYear() + 1900 gets the current year
var year = new Date().getYear() + 1900 - age;
alert("Your birth year is " + year);
```

In UI mode, it returns a `Promise`. Example:

```js
"ui";
dialogs.input("Please enter your age", "18").then(age => {
    var year = new Date().getYear() + 1900 - age;
    alert("Your birth year is " + year);
});
```

## dialogs.prompt(title[, prefill, callback])

Equivalent to `dialogs.rawInput()`.

## dialogs.select(title, items, callback)

* `title` {string} Title of the dialog.
* `items` {Array} List of options for the dialog (array of strings).
* `callback` {Function} Optional callback. Called when the user makes a selection (mainly for UI mode).

Displays a dialog with a list of options and waits for the user to select one. Returns the index of the selected option (0 to items.length - 1). Returns -1 if the user cancels.

```js
var options = ["Option A", "Option B", "Option C", "Option D"];
var i = dialogs.select("Please choose an option", options);
if (i >= 0) {
    toast("You selected " + options[i]);
} else {
    toast("You cancelled the selection");
}
```

In UI mode, this function returns a `Promise`. Example:

```js
"ui";
dialogs.select("Please choose an option", ["Option A", "Option B", "Option C", "Option D"])
    .then(i => {
        toast(i);
    });
```

## dialogs.singleChoice(title, items[, index, callback])

* `title` {string} Title of the dialog.
* `items` {Array} List of options (array of strings).
* `index` {number} Index of the initially selected option (default: 0).
* `callback` {Function} Optional callback (mainly for UI mode).

Displays a single-choice list dialog. Returns the index of the selected option. Returns -1 if cancelled.

In UI mode, it returns a `Promise`.

## dialogs.multiChoice(title, items[, indices, callback])

* `title` {string} Title of the dialog.
* `items` {Array} List of options (array of strings).
* `indices` {Array} Array of initially selected indices (default: empty array).
* `callback` {Function} Optional callback (mainly for UI mode).

Displays a multi-choice list dialog. Returns an array of selected indices. Returns `[]` if cancelled.

In UI mode, it returns a `Promise`.

## dialogs.build(properties)

* `properties` {Object} Dialog properties used to configure the dialog.
* Returns {Dialog}

Creates a customizable dialog. Example:

```js
dialogs.build({
    // Dialog title
    title: "New version found",
    // Dialog content
    content: "Changelog: Fixed several BUGs",
    // Positive button text
    positive: "Download",
    // Negative button text
    negative: "Cancel",
    // Neutral button text
    neutral: "Download from browser",
    // Checkbox text
    checkBoxPrompt: "Don't show again"
}).on("positive", () => {
    // Listen for positive button
    toast("Starting download....");
}).on("neutral", () => {
    // Listen for neutral button
    app.openUrl("https://www.autojs.org");
}).on("check", (checked) => {
    // Listen for checkbox
    log(checked);
}).show();
```

Available properties for configuration:

* `title` {string} Dialog title
* `titleColor` {string} | {number} Color of the dialog title
* `buttonRippleColor` {string} | {number} Ripple color for dialog buttons
* `icon` {string} | {Image} Icon of the dialog (URL or Image object)
* `content` {string} Dialog text content
* `contentColor` {string} | {number} Color of the dialog content text
* `contentLineSpacing` {number} Line height multiplier for dialog content text (1.0 = single line height)
* `items` {Array} Options for the dialog list
* `itemsColor` {string} | {number} Text color for list options
* `itemsSelectMode` {string} Selection mode for the list. Can be:
    * `select` — Normal selection mode
    * `single` — Single choice mode
    * `multi` — Multiple choice mode
* `itemsSelectedIndex` {number} | {Array} Pre-selected item index (single mode) or array of indices (multi mode)
* `positive` {string} Text for the positive button (rightmost)
* `positiveColor` {string} | {number} Text color for the positive button
* `neutral` {string} Text for the neutral button (leftmost)
* `neutralColor` {string} | {number} Text color for the neutral button
* `negative` {string} Text for the negative button (button to the left of positive)
* `negativeColor` {string} | {number} Text color for the negative button
* `checkBoxPrompt` {string} Checkbox text
* `checkBoxChecked` {boolean} Whether the checkbox is checked by default
* `progress` {Object} Configuration object for the progress bar:
    * `max` {number} Maximum value of the progress bar. Use -1 for an indeterminate (infinite) progress bar.
    * `horizontal` {boolean} If true, the indeterminate progress bar will be horizontal.
    * `showMinMax` {boolean} Whether to show min/max values for the progress bar.
* `cancelable` {boolean} Whether the dialog can be cancelled. If false, it can only be dismissed programmatically.
* `canceledOnTouchOutside` {boolean} Whether the dialog is cancelled when tapping outside it (default: true)
* `inputHint` {string} Hint text for the input box
* `inputPrefill` {string} Default text in the input box

Using these options, you can create highly customized dialogs and handle interactions by listening to events on the returned Dialog object. Here are some examples.

Simulating an alert dialog:

```js
dialogs.build({
    title: "Hello",
    content: "Stay energetic today!",
    positive: "OK"
}).show();
```

Simulating a confirm dialog:

```js
dialogs.build({
    title: "Hello",
    content: "Are you an idiot?",
    positive: "Yes",
    negative: "I'm a big idiot"
}).on("positive", () => {
    alert("Hahaha idiot");
}).on("negative", () => {
    alert("Hahaha big idiot");
}).show();
```

Simulating a single-choice dialog:

```js
dialogs.build({
    title: "Single Choice",
    items: ["Option 1", "Option 2", "Option 3", "Option 4"],
    itemsSelectMode: "single",
    itemsSelectedIndex: 3
}).on("single_choice", (index, item) => {
    toast("You selected " + item);
}).show();
```

"Processing" dialog:

```js
var d = dialogs.build({
    title: "Downloading...",
    progress: {
        max: -1
    },
    cancelable: false
}).show();

setTimeout(() => {
    d.dismiss();
}, 3000);
```

Input dialog:

```js
dialogs.build({
    title: "Please enter your age",
    inputPrefill: "18"
}).on("input", (input) => {
    var age = parseInt(input);
    toastLog(age);
}).show();
```

One clear difference when using this function to build dialogs is that you must use callbacks instead of getting synchronous return values like the other `dialogs` functions. However, you can achieve similar behavior using the `threads` module. For example, showing an input dialog and retrieving the result:

```js
var input = threads.disposable();
dialogs.build({
    title: "Please enter your age",
    inputPrefill: "18"
}).on("input", text => {
    input.setAndNotify(text);
}).show();
var age = parseInt(input.blockedGet());
toastLog(age);
```

# Dialog

The dialog object returned by `dialogs.build()`. It has built-in events for responding to user interaction and methods to get the dialog's state and information.

## Event: `show`

* `dialog` {Dialog} The dialog

Fired when the dialog is shown. Example:

```js
dialogs.build({
    title: "Title"
}).on("show", (dialog) => {
    toast("Dialog is shown");
}).show();
```

## Event: `cancel`

* `dialog` {Dialog} The dialog

Fired when the dialog is cancelled. A dialog can be cancelled by the cancel button, back key, or tapping outside. Example:

```js
dialogs.build({
    title: "Title",
    positive: "OK",
    negative: "Cancel"
}).on("cancel", (dialog) => {
    toast("Dialog was cancelled");
}).show();
```

## Event: `dismiss`

* `dialog` {Dialog} The dialog

Fired when the dialog is dismissed (either cancelled or by calling `dialog.dismiss()` manually). Example:

```js
var d = dialogs.build({
    title: "Title",
    positive: "确定",
    negative: "取消"
}).on("dismiss", (dialog)=>{
    toast("对话框消失了");
}).show();

setTimeout(()=>{
    d.dismiss();
}, 5000);
```

## 事件: `positive`

* `dialog` {Dialog} 对话框

确定按钮按下时触发的事件. 例如：

```
var d = dialogs.build({
    title: "标题",
    positive: "确定",
    negative: "取消"
}).on("positive", (dialog)=>{
    toast("你点击了确定");
}).show();
```

## 事件: `negative`

* `dialog` {Dialog} 对话框

取消按钮按下时触发的事件. 例如：

```
var d = dialogs.build({
    title: "标题",
    positive: "确定",
    negative: "取消"
}).on("negative", (dialog)=>{
    toast("你点击了取消");
}).show();
```

## 事件: `neutral`

* `dialog` {Dialog} 对话框

中性按钮按下时触发的事件. 例如：

```
var d = dialogs.build({
    title: "标题",
    positive: "确定",
    negative: "取消",
    neutral: "稍后提示"
}).on("positive", (dialog)=>{
    toast("你点击了稍后提示");
}).show();
```

## 事件: `any`

* `dialog` {Dialog} 对话框
* `action` {string} 被点击的按钮, 可能的值为:
    * `positive` 确定按钮
    * `negative` 取消按钮
    * `neutral` 中性按钮

任意按钮按下时触发的事件. 例如:

```
var d = dialogs.build({
    title: "标题",
    positive: "确定",
    negative: "取消",
    neutral: "稍后提示"
}).on("any", (action, dialog)=>{
    if(action == "positive"){
        toast("你点击了确定");
    }else if(action == "negative"){
        toast("你点击了取消");
    }
}).show();
```

## Event: `item_select`

* `index` {number} Index of the selected item (starting from 0)
* `item` {Object} The selected item
* `dialog` {Dialog} The dialog

Fired when an item in a normal list (`itemsSelectMode: "select"`) is clicked. Example:

```js
var d = dialogs.build({
    title: "Please select",
    positive: "OK",
    negative: "Cancel",
    items: ["A", "B", "C", "D"],
    itemsSelectMode: "select"
}).on("item_select", (index, item, dialog) => {
    toast("You selected item " + (index + 1) + ": " + item);
}).show();
```

## Event: `single_choice`

* `index` {number} Index of the selected item (starting from 0)
* `item` {Object} The selected item
* `dialog` {Dialog} The dialog

Fired when an item in single-choice mode is selected and the user confirms. Example:

```js
var d = dialogs.build({
    title: "Please select",
    positive: "OK",
    negative: "Cancel",
    items: ["A", "B", "C", "D"],
    itemsSelectMode: "singleChoice"
}).on("single_choice", (index, item, dialog) => {
    toast("You selected item " + (index + 1) + ": " + item);
}).show();
```

## Event: `multi_choice`

* `indices` {Array} Array of selected item indices
* `items` {Array} Array of selected items
* `dialog` {Dialog} The dialog

Fired when items in multi-choice mode are selected and the user confirms. Example:

```js
var d = dialogs.build({
    title: "Please select",
    positive: "OK",
    negative: "Cancel",
    items: ["A", "B", "C", "D"],
    itemsSelectMode: "multiChoice"
}).on("multi_choice", (indices, items, dialog) => {
    toast("Selected indices: " + indices + ", items: " + items);
}).show();
```

## Event: `input`

* `text` {string} Content of the input box
* `dialog` {Dialog} The dialog

Fired when the positive button is clicked on a dialog with an input field. Example:

```js
dialogs.build({
    title: "Please enter",
    positive: "OK",
    negative: "Cancel",
    inputPrefill: ""
}).on("input", (text, dialog) => {
    toast("You entered: " + text);
}).show();
```

## Event: `input_change`

* `text` {string} Current content of the input box
* `dialog` {Dialog} The dialog

Fired when the text in the input box changes. Example:

```js
dialogs.build({
    title: "Please enter",
    positive: "OK",
    negative: "Cancel",
    inputPrefill: ""
}).on("input_change", (text, dialog) => {
    toast("Current input: " + text);
}).show();
```

## dialog.getProgress()

* 返回 {number}

获取当前进度条的进度值, 是一个整数

## dialog.getMaxProgress()

* 返回 {number}

获取当前进度条的最大进度值, 是一个整数

## dialog.getActionButton(action)

* `action` {string} 动作, 包括:
    * `positive`
    * `negative`
    * `neutral`
