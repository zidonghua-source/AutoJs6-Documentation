# Control Node Actions (UiObjectActions)

UiObjectActions is a Java interface representing the set of actions for [control nodes (UiObject)](uiObjectType).

This interface has one abstract method [performAction](#m-performaction) which is the core for executing specific control node actions.  
Methods such as [ click / copy / paste ] are all wrappers around performAction, so users can also use performAction to implement custom control node action wrappers.

The following table lists some Action ID names and their corresponding implemented wrapper method names (asterisk indicates methods newly added in AutoJs6):

| Action ID                                 | Wrapper Method Name                | Minimum API Level      |
|:------------------------------------------|:-----------------------------------|------------------------|
| ACTION_ACCESSIBILITY_FOCUS                | accessibilityFocus                 | -                      |
| ACTION_CLEAR_ACCESSIBILITY_FOCUS          | clearAccessibilityFocus            | -                      |
| ACTION_CLEAR_FOCUS                        | clearFocus                         | -                      |
| ACTION_CLEAR_SELECTION                    | clearSelection *                   | -                      |
| ACTION_CLICK                              | click                              | -                      |
| ACTION_COLLAPSE                           | collapse                           | -                      |
| ACTION_CONTEXT_CLICK                      | contextClick                       | -                      |
| ACTION_COPY                               | copy                               | -                      |
| ACTION_CUT                                | cut                                | -                      |
| ACTION_DISMISS                            | dismiss                            | -                      |
| ACTION_DRAG_CANCEL                        | dragCancel *                       | 32 (12.1) [S_V2]       |
| ACTION_DRAG_DROP                          | dragDrop *                         | 32 (12.1) [S_V2]       |
| ACTION_DRAG_START                         | dragStart *                        | 32 (12.1) [S_V2]       |
| ACTION_EXPAND                             | expand                             | -                      |
| ACTION_FOCUS                              | focus                              | -                      |
| ACTION_HIDE_TOOLTIP                       | hideTooltip *                      | 28 (9) [P]             |
| ACTION_IME_ENTER                          | imeEnter *                         | 30 (11) [R]            |
| ACTION_LONG_CLICK                         | longClick                          | -                      |
| ACTION_MOVE_WINDOW                        | moveWindow *                       | 26 (8) [O]             |
| ACTION_NEXT_AT_MOVEMENT_GRANULARITY       | nextAtMovementGranularity *        | -                      |
| ACTION_NEXT_HTML_ELEMENT                  | nextHtmlElement *                  | -                      |
| ACTION_PAGE_DOWN                          | pageDown *                         | 29 (10) [Q]            |
| ACTION_PAGE_LEFT                          | pageLeft *                         | 29 (10) [Q]            |
| ACTION_PAGE_RIGHT                         | pageRight *                        | 29 (10) [Q]            |
| ACTION_PAGE_UP                            | pageUp *                           | 29 (10) [Q]            |
| ACTION_PASTE                              | paste                              | -                      |
| ACTION_PRESS_AND_HOLD                     | pressAndHold *                     | 30 (11) [R]            |
| ACTION_PREVIOUS_AT_MOVEMENT_GRANULARITY   | previousAtMovementGranularity *    | -                      |
| ACTION_PREVIOUS_HTML_ELEMENT              | previousHtmlElement *              | -                      |
| ACTION_SCROLL_BACKWARD                    | scrollBackward                     | -                      |
| ACTION_SCROLL_DOWN                        | scrollDown                         | -                      |
| ACTION_SCROLL_FORWARD                     | scrollForward                      | -                      |
| ACTION_SCROLL_LEFT                        | scrollLeft                         | -                      |
| ACTION_SCROLL_RIGHT                       | scrollRight                        | -                      |
| ACTION_SCROLL_TO_POSITION                 | scrollTo                           | -                      |
| ACTION_SCROLL_UP                          | scrollUp                           | -                      |
| ACTION_SELECT                             | select                             | -                      |
| ACTION_SET_PROGRESS                       | setProgress                        | -                      |
| ACTION_SET_SELECTION                      | setSelection                       | -                      |
| ACTION_SET_TEXT                           | setText                            | -                      |
| ACTION_SHOW_ON_SCREEN                     | show                               | -                      |
| ACTION_SHOW_TEXT_SUGGESTIONS              | showTextSuggestions *              | 33 (13) [TIRAMISU]     |
| ACTION_SHOW_TOOLTIP                       | showTooltip *                      | 28 (9) [P]             |

If the current device does not meet the minimum API level requirement listed, calling the corresponding method will not throw an exception and will silently return false:

```js
/* 
    For example, ACTION_IME_ENTER requires the device to run on Android API 30 (11) [R] or higher.
    On devices with API < 30, it will always return false and IME ENTER will have no effect (but no exception will be thrown).
 */
console.log(pickup({
    focusable: true,
    contentMatch: '.+',
}, 'imeEnter'));
```

All wrapper method **names** corresponding to the control actions listed in the table above have been globalized. For usage of globalized methods and their binding source information, see the [Global Action Redirection](#global-action-redirection) section.

> See also: [Android Docs](https://developer.android.com/reference/android/view/accessibility/AccessibilityNodeInfo.AccessibilityAction)

---

<p style="font: bold 2em sans-serif; color: #FF7043">UiObjectActions</p>

---

## [m!] performAction

Used to execute the specified control action.  
It is an abstract method with no default implementation.

### performAction(action, ...arguments)

**`A11Y`**

- **action** { [number](dataTypes#number) } - Unique identifier of the action (Action ID)
- **arguments** { [...](documentation#variadic-parameter)[ActionArgument](#i-actionargument)[[]](documentation#variadic-parameter) } - Action arguments, used to pass parameters to the action
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

Classes that implement this method:

- [UiSelector](uiSelectorType)
- [UiObject](uiObjectType)
- [UiObjectCollection](uiObjectCollectionType)

Source code summary:

- UiSelector

```kotlin
/* Updated as of Nov 2, 2022. */

override fun performAction(action: Int, vararg arguments: ActionArgument): Boolean {
    return untilFind().performAction(action, *arguments)
}
```

- UiObject

```kotlin
/* Updated as of Nov 2, 2022. */

override fun performAction(action: Int, vararg arguments: ActionArgument): Boolean {
    return performAction(action, Bundle().apply { arguments.forEach { it.putIn(this) } })
}

override fun performAction(action: Int, bundle: Bundle): Boolean = try {
    when (bundle.isEmpty) {
        true -> super.performAction(action)
        else -> super.performAction(action, bundle)
    }
} catch (e: IllegalStateException) {
    false
}
```

- UiObjectCollection

```kotlin
/* Updated as of Nov 2, 2022. */

override fun performAction(action: Int, vararg arguments: ActionArgument): Boolean {
    var success = true
    nodes.filterNotNull().forEach { node ->
        when (arguments.isEmpty()) {
            true -> node.performAction(action)
            else -> node.performAction(action, *arguments)
        }.also { success = success and it }
    }
    return success
}
```

It can be seen that both [UiSelector](uiSelectorType) and [UiObjectCollection](uiObjectCollectionType) ultimately call the `performAction` method of [UiObject](uiObjectType), while `UiObject`'s `performAction` calls Android's [AccessibilityNodeInfoCompat#performAction](https://developer.android.com/reference/androidx/core/view/accessibility/AccessibilityNodeInfoCompat#performAction(int,android.os.Bundle)) method.

`UiObjectCollection` is equivalent to calling `UiObject#performAction` on every control in the collection.  
`UiSelector` is equivalent to first calling [untilFind](uiSelectorType#m-untilfind) to find all controls in the current window, treating them as a collection and calling `UiObjectCollection#performAction`.

Because the global `untilFind()` performs "unconditional" filtering, it adds all controls in the window (often dozens or even hundreds or thousands) into the collection. At this point, executing any `Action` is equivalent to every control in the collection performing that action. Such operations are often meaningless and can easily lead to unexpected or even uncontrollable results. Therefore, it is not recommended to use the `Action` methods provided by `UiSelector`.

Here is an example of an action provided by `UiSelector`, again emphasizing that it is not recommended:

```js
/* ACTION_SET_TEXT action */

/* Set the content to "hello" for all controls in the current window that support setting text. */
selector().setText("hello");

/* Almost all methods of UiSelector have been globalized, including setText. */
setText("hello"); /* Same effect as above. */
```

If you have the above requirement (setting text content on controls) and want to set it on multiple controls at once, it is recommended to use a selector to locate the specific collection of controls, then uniformly execute the `Action`:

```js
/* First filter the collection. */
let nodes = pickup({
    focusable: true,
    textMatch: "name",
    boundInside: [ cX(0.2), cYx(0.04), cX(0.8), cY(0.92) ],
}, '[w]');

/* Then execute the action. */
nodes.forEach(w => w.setText("hello"));
```

If you need to perform a custom action on a control, you can do so via `UiObject#performAction`:

```js
/* Perform the ACTION_IME_ENTER action on the control. */

let { AccessibilityActionCompat } = androidx.core.view.accessibility.AccessibilityNodeInfoCompat;

let w = focusable().contentMatch(/name/).findOnce();
w.performAction(AccessibilityActionCompat.ACTION_IME_ENTER.id);
```

Some `Actions` require parameters. In such cases, you can pass parameters using the [ActionArgument](#i-actionargument) interface:

```js
/* Perform ACTION_SET_TEXT and ACTION_SET_SELECTION actions on the control. */

let { AccessibilityNodeInfoCompat } = androidx.core.view.accessibility
let { AccessibilityActionCompat } = AccessibilityNodeInfoCompat;
let { ActionArgument } = org.autojs.autojs.core.automator;

let w = focusable().contentMatch(/name/).findOnce();

/* ACTION_SET_TEXT requires an ACTION_ARGUMENT_SET_TEXT_CHARSEQUENCE "action argument". */
w.performAction(
    AccessibilityActionCompat.ACTION_SET_TEXT.id,
    ActionArgument.CharSequenceActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_SET_TEXT_CHARSEQUENCE, "hello"),
);

/* ACTION_SET_SELECTION requires two "action arguments": */
/* ACTION_ARGUMENT_SELECTION_START_INT and ACTION_ARGUMENT_SELECTION_END_INT. */
w.performAction(
    AccessibilityActionCompat.ACTION_SET_SELECTION.id,
    ActionArgument.IntActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_SELECTION_START_INT, 1),
    ActionArgument.IntActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_SELECTION_END_INT, 4),
);
```

`UiObject` has another instance method [performAction(action, bundle)](uiObjectType#performactionaction-bundle), so the above example can also be rewritten as:

```js
let arguments = new android.os.Bundle();
arguments.putInt(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_SELECTION_START_INT, 1);
arguments.putInt(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_SELECTION_END_INT, 4);
w.performAction(AccessibilityActionCompat.ACTION_SET_SELECTION.id, arguments);
```

To check whether a control has one or more specific `Actions`, you can use [UiObject#hasAction](uiObjectType#m-hasaction):

```js
console.log(w.hasAction("ACTION_CLICK"));
console.log(w.hasAction("CLICK")); /* The "ACTION_" prefix can be omitted. */

/* Check for multiple Actions at once. */
console.log(w.hasAction("CLICK", "IME_ENTER", "SCROLL_UP"));
```

To use an `Action` selector to filter controls, you can use [UiSelector#action](uiSelectorType#m-action):

```js
console.log(action("ACTION_CLICK").findOnce());
console.log(action("CLICK").findOnce()); /* The "ACTION_" prefix can be omitted. */

/* Filter for multiple Actions. */
console.log(action("CLICK", "IME_ENTER", "SCROLL_UP").findOnce());
```

## [m=] click

### click()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ click ] action.

To check if a control node is clickable:

```js
console.log(w.clickable());
console.log(w.isClickable()); /* Same as above. */
```

The following situations may cause `w.click()` to return `false`:

- The control is not clickable (`w.clickable()` is `false`)
- The page cannot respond to click events

Sometimes it happens that `w` itself is not clickable, but its parent controls such as `w.parent()` or `w.parent().parent()` are clickable:

```js
function tryClick(w) {
    let max = 3;
    let tmp = w;
    while (max--) {
        tmp = tmp.parent();
        if (tmp.isClickable()) {
            return tmp.click();
        }
    }
    return false;
}

console.log(tryClick(w));

/* The above process can be simplified using pickup. */
console.log(pickup(w, 'k3', 'click'));
```

Main advantages and disadvantages of using the control's `click` method (compared to coordinate-based clicking):

- [Advantage] Faster
- [Advantage] Suitable for controls whose position changes frequently
- [Advantage] Suitable for controls that are not within the visible area of the window
- [Advantage] Suitable for controls covered or obscured by other controls on top
- [Disadvantage] Some controls are difficult to precisely locate using selectors
- [Disadvantage] Some controls do not respond after executing the `click` action
- [Disadvantage] Cannot fully adapt to changes in control properties or hierarchy

Given the above advantages and disadvantages, the control's `click` method is usually used in combination with methods such as [global.click](global#m-click) ([automator.click](automator#m-click)) or [UiObject#clickByBounds](uiObjectType#m-clickbybounds).

## [m=] longClick

### longClick()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ long click ] action.

Check whether a control node is long-clickable:

```js
console.log(w.longClickable());
console.log(w.isLongClickable()); /* Same as above. */
```

The following situations may cause `w.longClick()` to return `false`:

- The control is not long-clickable (`w.longClickable()` is `false`)
- The page cannot respond to long-click events

## [m=] accessibilityFocus

### accessibilityFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ accessibility focus ] action.

accessibilityFocus() can only be used normally when accessibility software (such as [TalkBack](https://support.google.com/accessibility/android/topic/10601570?hl=en)) is enabled on the current device.

Taking TalkBack as an example, once enabled, the control that gains accessibility focus in the current window will have its bounds marked with a green box. At this point, pressing the Enter key on the keyboard or the confirm key on an accessibility device (such as a [D-pad](https://en.wikipedia.org/wiki/D-pad)), depending on the device, will activate the control.

```js
/* Gain accessibility focus. */
console.log(pickup(idEndsWith('fab'), 'accessibilityFocus')); /* boolean result. */

/* Check whether accessibility focus has been gained. */
console.log(pickup(idEndsWith('fab'), 'accessibilityFocused')); /* boolean result. */
```

To clear focus, use the [clearAccessibilityFocus](#m-clearaccessibilityfocus) method.

## [m=] clearAccessibilityFocus

### clearAccessibilityFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ clear accessibility focus ] action.

clearAccessibilityFocus() can only be used normally when accessibility software (such as [TalkBack](https://support.google.com/accessibility/android/topic/10601570?hl=en)) is enabled on the current device.

```js
/* Clear accessibility focus. */
console.log(pickup(idEndsWith('fab'), 'clearAccessibilityFocus')); /* boolean result. */
```

## [m=] focus

### focus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ focus ] action.

When an external keyboard or other input device is connected to the current device, pressing TAB or arrow keys can "switch" between controls; these controls are all focusable.

```js
/* Check whether the control is focusable. */
console.log(w.focusable());
console.log(w.isFocusable()); /* Same as above. */
```

After a control gains focus, the Enter or OK key (indicating confirmation) on the input device can be used to activate it.  
If the control supports text input (such as common EditText controls), an input cursor will appear after it gains focus, and a soft keyboard may pop up for user input.

```js
/* Print an array of text content of focusable controls in the current window. */
console.log(pickup({ focusable: true }, 'txt[]'));

/* Filter a control by text content and make it gain focus. */
pickup([ { focusable: true }, /search/ ], 'focus');
```

To clear focus, use the [clearFocus](#m-clearfocus) method.

## [m=] clearFocus

### clearFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ clear focus ] action.

For a focusable control, if it does not currently have focus, calling clearFocus will return false.

```js
/* w is focusable, but does not currently have focus. */
console.log(w.focusable()); // true
console.log(w.isFocused()); // false

/* isFocused returns false, so clearFocus also returns false. */
console.log(w.clearFocus()); // false
```

## [m=] dragStart

### dragStart()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ drag start ] action.

This operation initializes the system's internal drag-and-drop (Drag & Drop) functionality.  
The content to be dragged will be prepared before the drag action starts.

## [m=] dragDrop

### dragDrop()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ drag drop ] action.

This operation targets the drop target for which an ACTION_DRAG_START action has already started.

## [m=] dragCancel

### dragCancel()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ drag cancel ] action.

This operation targets the drop target for which an ACTION_DRAG_START action has already started.

## [m=] imeEnter

### imeEnter()

**`6.2.0`** **`A11Y`** **`API>=30`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ IME enter key ] action.

This operation is usually only effective for controls that have focus and are editable.

imeEnter is typically used to simulate the Enter key to implement line breaks in text controls.  
It can also simulate certain confirmation operations, such as [ Search / Send / Next / Go / Begin execution ] etc.

```js
/* Simulate Enter key. */
console.log(pickup({
    className: 'EditText',
    focused: true,
}, 'imeEnter')); /* e.g. true */
```

## [m=] moveWindow

### moveWindow(x, y)

**`6.2.0`** **`A11Y`** **`API>=26`**

- **x** { [number](dataTypes#number) } - X coordinate
- **y** { [number](dataTypes#number) } - Y coordinate
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ move window to new position ] action.

## [m=] nextAtMovementGranularity

### nextAtMovementGranularity(granularity, isExtendSelection)

**`6.2.0`** **`A11Y`**

- **granularity** { [number](dataTypes#number) } - Granularity
- **isExtendSelection** { [boolean](dataTypes#boolean) } - Whether to extend text selection
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ move to next position by granularity ] action.

Moves the cursor to the next text entity position by the specified granularity, for example moving to the next word, next line, next paragraph, etc.

```js
const AccessibilityNodeInfo = android.view.accessibility.AccessibilityNodeInfo;

let w = pickup([ /.+/, { className: 'EditText' } ]);

/* Move by WORD granularity. */
/* In addition to WORD, CHARACTER (character), LINE (line), PARAGRAPH (paragraph), PAGE (page) and other granularities are also supported. */
w.nextAtMovementGranularity(AccessibilityNodeInfo.MOVEMENT_GRANULARITY_WORD, false);
```

## [m=] nextHtmlElement

### nextHtmlElement(element)

**`6.2.0`** **`A11Y`**

- **element** { [string](dataTypes#string) } - Element name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ move to next position by element ] action.

Moves focus to the next element position by the specified element name, for example moving to the next button, next list, next input box, etc.

```js
console.log(w.nextHtmlElement("BUTTON"));
```

## [m=] pageLeft

### pageLeft()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ page left ] action.

This operation moves the viewport to the left so that more content (if any) to the left of the pageable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view to the right.

- New visible content: left.
- Viewport movement direction: left.
- View movement direction: right.

## [m=] pageUp

### pageUp()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ page up ] action.

This operation moves the viewport upward so that more content (if any) above the pageable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view downward.

- New visible content: up.
- Viewport movement direction: up.
- View movement direction: down.

## [m=] pageRight

### pageRight()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ page right ] action.

This operation moves the viewport to the right so that more content (if any) to the right of the pageable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view to the left.

- New visible content: right.
- Viewport movement direction: right.
- View movement direction: left.

## [m=] pageDown

### pageDown()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ page down ] action.

This operation moves the viewport downward so that more content (if any) below the pageable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view upward.

- New visible content: down.
- Viewport movement direction: down.
- View movement direction: up.

## [m=] pressAndHold

### pressAndHold()

**`6.2.0`** **`A11Y`** **`API>=30`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ press and hold ] action.

Press and hold means press and keep pressed; it is different from ACTION_LONG_CLICK (long click).  
If a control's single-action response is designed for "long click", the wrapped longClick method should be used instead of pressAndHold.  
pressAndHold is only effective if the control has a response to the "press and hold" action.  
Usually controls do not have responses to both of the above actions at the same time.

## [m=] previousAtMovementGranularity

### previousAtMovementGranularity(granularity, isExtendSelection)

**`6.2.0`** **`A11Y`**

- **granularity** { [number](dataTypes#number) } - Granularity
- **isExtendSelection** { [boolean](dataTypes#boolean) } - Whether to extend text selection
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ move to previous position by granularity ] action.

Moves the cursor to the previous text entity position by the specified granularity, for example moving to the previous word, previous line, previous paragraph, etc.

```js
const AccessibilityNodeInfo = android.view.accessibility.AccessibilityNodeInfo;

let w = pickup([ /.+/, { className: 'EditText' } ]);

/* Move by WORD granularity. */
/* In addition to WORD, CHARACTER (character), LINE (line), PARAGRAPH (paragraph), PAGE (page) and other granularities are also supported. */
w.previousAtMovementGranularity(AccessibilityNodeInfo.MOVEMENT_GRANULARITY_WORD, false);
```

## [m=] previousHtmlElement

### previousHtmlElement(element)

**`6.2.0`** **`A11Y`**

- **element** { [string](dataTypes#string) } - Element name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ move to previous position by element ] action.

Moves focus to the previous element position by the specified element name, for example moving to the previous button, previous list, previous input box, etc.

```js
console.log(w.previousHtmlElement("BUTTON"));
```

## [m=] showTextSuggestions

### showTextSuggestions()

**`6.2.0`** **`A11Y`** **`API>=33`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ show text suggestions ] action.

This operation displays relevant input suggestions for an editable text control.

## [m=] showTooltip

### showTooltip()

**`6.2.0`** **`A11Y`** **`API>=28`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ show tooltip ] action.

This operation is usually only effective for controls whose view is not currently showing tooltip information.

## [m=] hideTooltip

### hideTooltip()

**`6.2.0`** **`A11Y`** **`API>=28`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ hide tooltip ] action.

This operation is usually only effective for controls whose view is currently showing tooltip information.

## [m=] show

### show()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ show in viewport ] action.

This operation makes all boundaries of the control appear inside the viewport.  
If necessary, the page will scroll.

```js
/* The "About app and developer" button is partially (or completely) outside the viewport. */
let w = pickup("About app and developer");

if (w !== null) {
    /* The control will scroll into the viewport along with the page. */
    w.show();
}
```

> See also [View.requestRectangleOnScreen(Rect)](https://developer.android.com/reference/android/view/View#requestRectangleOnScreen(android.graphics.Rect))

## [m=] dismiss

### dismiss()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ dismiss ] action.

Check whether a control node is dismissable:

```js
console.log(w.dismissable());
console.log(w.isDismissable()); /* Same as above. */
```

## [m=] copy

### copy()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ copy text ] action.

This operation copies the selected text content of the control to the clipboard.

## [m=] cut

### cut()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ cut text ] action.

This operation cuts the selected text content of the control and places it on the clipboard.

## [m=] paste

### paste()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ paste text ] action.

This operation pastes the clipboard text content into the editable text area of the control.

Note that starting from [Android API 29 (10) [Q]](apiLevel), access to clipboard data will be restricted.  
See [getClip](global#m-getclip) for details.

## [m=] select

### select()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ select ] action.

This operation selects the current control.

Check whether a control node is selected:

```js
console.log(w.selected());
console.log(w.isSelected()); /* Same as above. */
```

## [m=] expand

### expand()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ expand ] action.

This operation is used to expand expandable controls.

## [m=] collapse

### collapse()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ collapse ] action.

This operation is used to collapse (or retract) expandable controls.

## [m=] scrollLeft

### scrollLeft()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ scroll left ] action.

This operation moves the viewport to the left so that more content (if any) to the left of the scrollable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view to the right.

- New visible content: left.
- Viewport movement direction: left.
- View movement direction: right.

## [m=] scrollUp

### scrollUp()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ scroll up ] action.

This operation moves the viewport upward so that more content (if any) above the scrollable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view downward.

- New visible content: up.
- Viewport movement direction: up.
- View movement direction: down.

## [m=] scrollRight

### scrollRight()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ scroll right ] action.

This operation moves the viewport to the right so that more content (if any) to the right of the scrollable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view to the left.

- New visible content: right.
- Viewport movement direction: right.
- View movement direction: left.

## [m=] scrollDown

### scrollDown()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ scroll down ] action.

This operation moves the viewport downward so that more content (if any) below the scrollable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view upward.

- New visible content: down.
- Viewport movement direction: down.
- View movement direction: up.

## [m=] scrollForward

### scrollForward()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ scroll forward ] action.

This operation moves the viewport forward so that more content (if any) in front of the scrollable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view backward.

- New visible content: forward.
- Viewport movement direction: forward.
- View movement direction: backward.

> Note: "forward" includes "left" or "up", "backward" includes "right" or "down".

## [m=] scrollBackward

### scrollBackward()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ scroll backward ] action.

This operation moves the viewport backward so that more content (if any) behind the scrollable control is displayed inside the viewport.  
For touch-screen devices, this operation is equivalent to pressing and holding on the screen and dragging the view forward.

- New visible content: backward.
- Viewport movement direction: backward.
- View movement direction: forward.

> Note: "forward" includes "left" or "up", "backward" includes "right" or "down".

## [m=] scrollTo

### scrollTo(row, column)

**`A11Y`**

- **row** { [number](dataTypes#number) } - Row index
- **column** { [number](dataTypes#number) } - Column index
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ scroll specified position into viewport ] action.

This operation scrolls the specified position (marked by "row" and "column") in the collection into the viewport.

```js
scrollable().find().some((w) => {
    let info = w.getCollectionInfo();
    if (info !== null) {
        console.log(info.getRowCount()); /* e.g. 17 */
        console.log(info.getColumnCount()); /* e.g. 2 */
        
        let randRow = Mathx.randInt(info.getRowCount() - 1);
        let randColumn = Mathx.randInt(info.getColumnCount() - 1);
        console.log(`${randRow},${randColumn}`); /* e.g. 10,1 */
        
        console.log(w.scrollTo(randRow, randColumn)); /* e.g. false */
        
        return /* @some */ true;
    }
});
```

## [m=] contextClick

### contextClick()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ context click ] action.

This operation usually pops up a context menu, similar to a right-click menu.

> Note: In the Microsoft Windows operating system, right-clicking the mouse (or pressing the Menu key on the keyboard) is similar to the Context Click behavior of a control, and the pop-up right-click menu is also called a Context Menu.

## [m=] setText

### setText(text)

**`A11Y`**

- **text** { [string](dataTypes#string) } - Text
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ set text ] action.

This operation replaces the original text with new text and places the cursor at the end of the text.

```js
let w = pickup({ className: 'EditText' });

/* Set text to "hello". */
w.setText("hello");

/* Clear text. */
w.setText("");
```

## [m=] setSelection

### setSelection(start, end)

**`A11Y`**

- **start** { [number](dataTypes#number) } - Start position
- **end** { [number](dataTypes#number) } - End position
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ select text ] action.

This operation selects the text content of the control within the specified range.

```js
let w = pickup({ className: 'EditText' });

/* Select 1 character from 2 to 3, with the start cursor at position 2 and the end cursor at position 3. */
w.setSelection(2, 3);

/* No effect, cursor does not change. */
w.setSelection(2, 0);
w.setSelection(2, -5);

/* Throws an exception. */
w.setSelection(NaN, 0);
w.setSelection(Infinity, 0);

/* Select 0 characters; at this point the start and end cursors coincide. */
w.setSelection(2, 2);
```

## [m=] clearSelection

### clearSelection()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ clear text selection ] action.

## [m=] setProgress

### setProgress(progress)

**`A11Y`**

- **progress** { [number](dataTypes#number) } - Progress value
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [ set progress value ] action.

```js
pickup({ action: ['SET_PROGRESS'] }, '[]').some((w) => {
    const info = w.getRangeInfo();
    if (info !== null) {
        console.log(w.getMin(), w.getMax());
        let randProgress = Mathx.randInt(w.getMin(), w.getMax());
        console.log(randProgress);
        console.log(w.setProgress(randProgress));
    }
});
```

## [I] ActionArgument

Control action argument interface.  
Mainly used inside the abstract [performAction](#m-performaction) method for custom control actions.

### [C] IntActionArgument

Concrete class of ActionArgument.  
Used to pass Int type action arguments.

#### [c] (name, value)

- **name** { [string](dataTypes#string) } - Action name
- **value** { [number](dataTypes#number) } - Action argument value
- <ins>**returns**</ins> { [ActionArgument](#i-actionargument) }

Construct an Int type action argument.

```js
/* Simulate the scrollTo wrapper method. */
function scrollTo(x, y) {
    return w.performAction(
        AccessibilityActionCompat.ACTION_SCROLL_TO_POSITION.id,
        ActionArgument.IntActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_ROW_INT, x),
        ActionArgument.IntActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_COLUMN_INT, y),
    );
}
```

### [C] BooleanActionArgument

Concrete class of ActionArgument.  
Used to pass Boolean type action arguments.

#### [c] (name, value)

- **name** { [string](dataTypes#string) } - Action name
- **value** { [boolean](dataTypes#boolean) } - Action argument value
- <ins>**returns**</ins> { [ActionArgument](#i-actionargument) }

Construct a Boolean type action argument.

```js
/* Simulate the nextAtMovementGranularity wrapper method. */
function nextAtMovementGranularity(granularity, isExtendSelection) {
    return w.performAction(
        AccessibilityActionCompat.ACTION_NEXT_AT_MOVEMENT_GRANULARITY.id,
        ActionArgument.IntActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_MOVEMENT_GRANULARITY_INT, granularity),
        ActionArgument.BooleanActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_EXTEND_SELECTION_BOOLEAN, isExtendSelection),
    );
}
```

### [C] CharSequenceActionArgument

Concrete class of ActionArgument.  
Used to pass CharSequence type action arguments.

#### [c] (name, value)

- **name** { [string](dataTypes#string) } - Action name
- **value** { [string](dataTypes#string) } - Action argument value
- <ins>**returns**</ins> { [ActionArgument](#i-actionargument) }

Construct a CharSequence type action argument.

```js
/* Simulate the setText wrapper method. */
function setText(text) {
    return w.performAction(
        AccessibilityActionCompat.ACTION_SET_TEXT.id,
        ActionArgument.IntActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_SET_TEXT_CHARSEQUENCE, text),
    );
}
```

### [C] StringActionArgument

Concrete class of ActionArgument.  
Used to pass String type action arguments.

#### [c] (name, value)

- **name** { [string](dataTypes#string) } - Action name
- **value** { [string](dataTypes#string) } - Action argument value
- <ins>**returns**</ins> { [ActionArgument](#i-actionargument) }

Construct a String type action argument.

```js
/* Simulate the nextHtmlElement wrapper method. */
function nextHtmlElement(element) {
    return w.performAction(
        AccessibilityActionCompat.ACTION_NEXT_HTML_ELEMENT.id,
        ActionArgument.StringActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_HTML_ELEMENT_STRING, element),
    );
}
```

### [C] FloatActionArgument

Concrete class of ActionArgument.  
Used to pass Float type action arguments.

#### [c] (name, value)

- **name** { [string](dataTypes#string) } - Action name
- **value** { [number](dataTypes#number) } - Action argument value
- <ins>**returns**</ins> { [ActionArgument](#i-actionargument) }

Construct a Float type action argument.

```js
/* Simulate the setProgress wrapper method. */
function nextHtmlElement(progress) {
    return w.performAction(
        AccessibilityActionCompat.ACTION_SET_PROGRESS.id,
        ActionArgument.FloatActionArgument(AccessibilityNodeInfoCompat.ACTION_ARGUMENT_PROGRESS_VALUE, progress),
    );
}
```

# Global Action Redirection

All control action method **names** in this chapter have been globalized, meaning they support direct global calls such as [ `click()` / `paste()` / `scrollDown()` / `show()` ].  
Most of these methods are direct bindings of UiSelector instance methods, but some methods are overridden by SimpleActionAutomator.

The following table lists the binding sources for control action methods.  
AUTO represents SimpleActionAutomator, SEL represents UiSelector.

| Global Actions                | AUTO | SEL |        
|-------------------------------|:----:|:---:|
| accessibilityFocus            |      |  √  |
| clearAccessibilityFocus       |      |  √  |
| clearFocus                    |      |  √  |
| clearSelection                |      |  √  |
| click                         |  √   |     |
| collapse                      |      |  √  |
| contextClick                  |      |  √  |
| copy                          |      |  √  |
| cut                           |      |  √  |
| dismiss                       |      |  √  |
| dragCancel                    |      |  √  |
| dragDrop                      |      |  √  |
| dragStart                     |      |  √  |
| expand                        |      |  √  |
| focus                         |      |  √  |
| hideTooltip                   |      |  √  |
| imeEnter                      |      |  √  |
| longClick                     |  √   |     |
| moveWindow                    |      |  √  |
| nextAtMovementGranularity     |      |  √  |
| nextHtmlElement               |      |  √  |
| pageDown                      |      |  √  |
| pageLeft                      |      |  √  |
| pageRight                     |      |  √  |
| pageUp                        |      |  √  |
| paste                         |      |  √  |
| pressAndHold                  |      |  √  |
| previousAtMovementGranularity |      |  √  |
| previousHtmlElement           |      |  √  |
| scrollBackward                |      |  √  |
| scrollDown                    |  √   |     |
| scrollForward                 |      |  √  |
| scrollLeft                    |      |  √  |
| scrollRight                   |      |  √  |
| scrollTo                      |      |  √  |
| scrollUp                      |  √   |     |
| select                        |      |  √  |
| setProgress                   |      |  √  |
| setSelection                  |      |  √  |
| setText                       |  √   |     |
| show                          |      |  √  |
| showTextSuggestions           |      |  √  |
| showTooltip                   |      |  √  |

As of now (2022/11), only the global methods [ click, longClick, scrollDown, scrollUp, setText ] belong to SimpleActionAutomator.

```js
copy(); /* Equivalent to selector().copy(). */
paste(); /* Equivalent to selector().paste(). */
clearFocus(); /* Equivalent to selector().clearFocus(). */
imeEnter(); /* Equivalent to selector().imeEnter(). */

click(1, 2); /* Equivalent to automator.click(1, 2). */
longClick(1, 2); /* Equivalent to automator.longClick(1, 2). */
setText("hello"); /* Equivalent to automator.setText("hello"). */
scrollUp(); /* Equivalent to automator.scrollUp(). */
scrollDown(); /* Equivalent to automator.scrollDown(). */
```

As can be seen from the [performAction](#m-performaction) section, the control action methods of UiSelector actually execute the Action once on all controls in the current window. Therefore, almost all control action methods of UiSelector are not recommended.

The global method [paste](#m-paste) is a relatively frequently used control action, and its effect is often as expected.  
For analysis of the execution process and principles of the global `paste` method, see the [UiSelector#paste](uiSelectorType#m-paste) section.