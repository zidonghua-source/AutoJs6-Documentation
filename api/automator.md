# Automation (Automator)

---

<p style="font: italic 1em sans-serif; color: #78909C">This chapter is pending supplementation or improvement...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Oct 22, 2022.</p>

---

## Simple Automation (SimpleActionAutomator)

Pending...

## Root Automation (RootAutomator)

Pending...

## Automation Configuration (AutomatorConfiguration)

Pending...

## Selector (UiSelector)

`UiSelector` (selector) can also be viewed as a condition filter for [control nodes](uiObjectType). It is used to filter one or more `control nodes` from the active window by attaching different conditions, and then perform further processing, such as [ executing [control actions](uiObjectActionsType) (click, long click, set text, etc.) / determining position / retrieving text content / getting specific control states / performing [compass](uiObjectType#m-compass) navigation within the [control hierarchy](glossaries#control-hierarchy) ], etc.

For details, see the [Selector (UiSelector)](uiSelectorType) chapter.

## Control Node (UiObject)

`UiObject` is commonly referred to as [control / node / control node]. It can be thought of as an [AccessibilityNodeInfo](https://developer.android.com/reference/android/view/accessibility/AccessibilityNodeInfo) object wrapped by the Android Accessibility service. It represents a node in the current active window. Through this node, you can collect control information or perform control actions, thereby implementing a series of automation operations.

For details, see the [Control Node (UiObject)](uiObjectType) chapter.

## Control Collection (UiObjectCollection)

`UiObjectCollection` represents a collection of [control node (UiObject)](uiObjectType) objects.

For details, see the [Control Collection (UiObjectCollection)](uiObjectCollectionType) chapter.

## Control Node Actions (UiObjectActions)

`UiObjectActions` is a Java interface that represents the set of actions available on a [control node (UiObject)](uiObjectType).

For details, see the [Control Node Actions (UiObjectActions)](uiObjectActionsType) chapter.

---

# Coordinate-based Touch Simulation

This section introduces functions for performing clicks and swipes using screen coordinates. Some of these functions require Android 7.0 or higher, while others require root privileges.

To obtain the coordinates of the position you want to click, you can enable "Pointer location" in Developer Options.

Scripts that rely on coordinates often face resolution issues. You can use the `setScreenMetrics()` function to automatically scale coordinates. This function affects all click, long-click, swipe, and similar functions in this section. By setting the resolution for which the script was designed, AutoJs will automatically scale the coordinates when running on devices with different resolutions.

Controls and coordinates can also be combined. Some controls are not clickable (`clickable` is `false`) and cannot be clicked using the `.click()` function. In such cases, if the device is running Android 7.0+ or has root access, you can click them using the following method:

```js
// Get the control
var widget = id("xxx").findOne();
// Get its center position and click it
click(widget.bounds().centerX(), widget.bounds().centerY());
// Use Tap if you have root privileges
```

## setScreenMetrics(width, height)

* `width` {number} Screen width in pixels
* `height` {number} Screen height in pixels

Sets the screen width and height that the script's coordinate-based clicks are designed for. If the actual screen size differs when the script runs, coordinates will be automatically scaled.

For example, on a 1920×1080 device, the code might be:

```js
setScreenMetrics(1080, 1920);
click(800, 200);
longClick(300, 500);
```

On other devices, AutoJs will automatically scale the coordinates so the script remains effective. For instance, on a 540×960 screen, `click(800, 200)` will actually click at position (400, 100).

# Touch and Gesture Simulation on Android 7.0 and Above

**Note: The following commands only work on Android 7.0 and higher.**

## click(x, y)

* `x` {number} X coordinate to click
* `y` {number} Y coordinate to click

Simulates a tap at the coordinate (x, y) and returns whether the click was successful. The script will only continue after the click operation completes.

In general, a click will only fail if it is interrupted by another event during the click process (approximately 150 milliseconds), such as the user tapping themselves.

When using this function to simulate rapid repeated clicks, the click speed may be too slow. In such cases, use the `press()` function instead.

## longClick(x, y)

* `x` {number} X coordinate to long-press
* `y` {number} Y coordinate to long-press

Simulates a long press at the coordinate (x, y) and returns whether it was successful. The script will only continue after the long press completes (approximately 600 milliseconds).

In general, a long press will only fail if it is interrupted by another event during the process (such as the user tapping).

## press(x, y, duration)

* `x` {number} X coordinate to press
* `y` {number} Y coordinate to press
* `duration` {number} Press duration in milliseconds

Simulates pressing and holding at the coordinate (x, y) for the specified duration and returns whether it was successful. The script continues only after the press operation completes.

If the press duration is very short, the system may treat it as a click. If the duration exceeds 500 milliseconds, it is treated as a long press.

In general, the operation will only fail if it is interrupted by another event during the press.

Example of a rapid clicker:

```js
// Click 100 times
for (var i = 0; i < 100; i++) {
  // Click position (500, 1000), each press lasts 1 millisecond
  press(500, 1000, 1);
}
```

## swipe(x1, y1, x2, y2, duration)

* `x1` {number} X coordinate of the swipe start point
* `y1` {number} Y coordinate of the swipe start point
* `x2` {number} X coordinate of the swipe end point
* `y2` {number} Y coordinate of the swipe end point
* `duration` {number} Swipe duration in milliseconds

Simulates swiping from coordinate (x1, y1) to (x2, y2) and returns whether it was successful. The script continues only after the swipe completes.

In general, the swipe will only fail if interrupted by another event during the gesture.

## gesture(duration, [x1, y1], [x2, y2], ...)

* `duration` {number} Duration of the gesture
* [x, y] ... Series of coordinates that form the gesture path

Simulates a gesture operation. For example, `gesture(1000, [0, 0], [500, 500], [500, 1000])` simulates a gesture from (0,0) → (500,500) → (500,1000) lasting 2 seconds.

## gestures([delay1, duration1, [x1, y1], [x2, y2], ...], [delay2, duration2, [x3, y3], [x4, y4], ...], ...)

Simulates multiple gestures simultaneously. Each gesture's parameters are in the form `[delay, duration, coordinates]`, where:
- `delay` is how many milliseconds to wait before executing the gesture (optional, defaults to 0)
- `duration` is the execution time of the gesture
- Coordinates are the points the gesture passes through.

Example of a pinch gesture with two fingers:

```js
gestures([0, 500, [800, 300], [500, 1000]],
         [0, 500, [300, 1500], [500, 1000]]);
```

# RootAutomator

`RootAutomator` is an object that uses root privileges to simulate touches. It can perform single and multi-touch operations with no delay in execution.

It is recommended to have only one `RootAutomator` instance in a script and ensure it is properly exited when the script ends. You can register an exit listener to clean it up:

```js
var ra = new RootAutomator();
events.on('exit', function() {
  ra.exit();
});
// Perform some click operations
...
```

**Note: The following commands require root privileges.**

## RootAutomator.tap(x, y[, id])

* `x` {number} X coordinate
* `y` {number} Y coordinate
* `id` {number} Multi-touch ID (optional, default is 1). Can be specified via `setDefaultId`.

Taps at position (x, y). The `id` is an integer used to distinguish multi-touch points. Different IDs represent different "fingers". Example:

```js
var ra = new RootAutomator();
// Let "finger 1" tap at (100, 100)
ra.tap(100, 100, 1);
// Let "finger 2" tap at (200, 200)
ra.tap(200, 200, 2);
ra.exit();
```

If multi-touch is not needed, the `id` parameter can be omitted.

Multi-touch is commonly used for gestures or games, such as simulating pinch-to-zoom or two-finger swipes.

In some cases, `tap` may not register a response. You can use `RootAutomator.press()` as an alternative.

## RootAutomator.swipe(x1, y1, x2, y2[, duration, id])

* `x1` {number} X coordinate of swipe start
* `y1` {number} Y coordinate of swipe start
* `x2` {number} X coordinate of swipe end
* `y2` {number} Y coordinate of swipe end
* `duration` {number} Swipe duration in milliseconds (default: 300)
* `id` {number} Multi-touch ID (optional, default: 1)

Simulates a swipe from (x1, y1) to (x2, y2) over the specified duration.

## RootAutomator.press(x, y, duration[, id])

* `x` {number} X coordinate
* `y` {number} Y coordinate
* `duration` {number} Press duration in milliseconds
* `id` {number} Multi-touch ID (optional, default: 1)

Simulates pressing and holding at position (x, y) for the given duration.

## RootAutomator.longPress(x, y[, id])

* `x` {number} X coordinate
* `y` {number} Y coordinate
* `id` {number} Multi-touch ID (optional, default: 1)

Simulates a long press at position (x, y).

The functions above are for simple touch simulation. For more complex gestures, lower-level functions are needed.

## RootAutomator.touchDown(x, y[, id])

* `x` {number} X coordinate
* `y` {number} Y coordinate
* `id` {number} Multi-touch ID (optional, default: 1)

Simulates a finger press at position (x, y).

## RootAutomator.touchMove(x, y[, id])

* `x` {number} X coordinate
* `y` {number} Y coordinate
* `id` {number} Multi-touch ID (optional, default: 1)

Simulates moving a finger to position (x, y).

## RootAutomator.touchUp([id])

* `id` {number} Multi-touch ID (optional, default: 1)

Simulates lifting a finger.

# Simple Root-based Click and Swipe Commands

**Note:** The functions in this section may change in future versions. It is recommended to use `RootAutomator` instead of these functions.

All functions below require root privileges and allow clicking, swiping, etc. at arbitrary positions.

* These functions usually start with a capital letter to indicate their special privilege.
* None of these functions return any value.
* Their execution is asynchronous and non-blocking. Execution time varies across devices. The script does not wait for the action to complete. It is best to add an appropriate `sleep()` after each call.

Example:

```js
Tap(100, 100);
sleep(500);
```

**Important:** Actions may not be stoppable. For example:

```js
for (var i = 0; i < 100; i++) {
  Tap(100, 100);
}
```

After running this code, taps may continue even after stopping the script from the task manager.

Therefore, it is strongly recommended to add a delay after each action:

```js
for (var i = 0; i < 100; i++) {
  Tap(100, 100);
  sleep(500);
}
```

## Tap(x, y)

* `x`, `y` {number} Coordinates to click.

Clicks at position (x, y). You can enable "Pointer location" in Developer Options to determine the coordinates.

## Swipe(x1, y1, x2, y2, [duration])

* `x1`, `y1` {number} Starting coordinates of the swipe
* `x2`, `y2` {number} Ending coordinates of the swipe
* `duration` {number} Duration of the swipe action

Performs a swipe from (x1, y1) to (x2, y2).

# Widget-based Operations

Widget-based operations refer to selecting controls on the screen, retrieving their information, or performing actions on them. For most regular applications, widget-based operations offer good compatibility across different devices. However, for games — whose interfaces are usually not composed of standard widgets — the methods in this section cannot be used. For game scripting, please refer to the "Coordinate-based Operations" section.

Widget-based operations depend on the Accessibility service. It is recommended to call the `auto()` function at the beginning of your script to ensure the Accessibility service is enabled. If a statement requiring the service is reached while it is not active, an exception will be thrown and the user will be redirected to the Accessibility settings. This results in a poor user experience, as the script must be restarted. Future versions will include functions to wait for the Accessibility service to start and then resume the script.

You can also add `"auto";` at the very beginning of the script to indicate that it requires the Accessibility service. However, this approach is not recommended because the marker must appear at the absolute start of the file (no comments, statements, or whitespace allowed before it). We recommend using the `auto()` function instead.

## auto([mode])

* `mode` {string} Mode

Checks whether the Accessibility service is enabled. If not, throws an exception and redirects the user to the Accessibility settings screen. Also sets the Accessibility mode.

Available modes:

* `fast` — Fast mode. Enables widget caching so selectors can find screen controls more quickly. Useful for scripts that require fast widget operations. Not necessary for most general scripts.
* `normal` — Normal mode (default).

If no mode is specified, normal mode is used.

It is recommended to use `auto.waitFor()` and `auto.setMode()` instead of this function, because `auto()` will stop the script if the service is not enabled, while `auto.waitFor()` will continue running after the service starts.

Example:

```js
auto("fast");
```

Example 2:

```js
auto();
```

## auto.waitFor()

Checks whether the Accessibility service is enabled. If not, redirects the user to the Accessibility settings and waits for the service to start. Once the service is active, the script continues.

Because this function is blocking, it cannot be used in UI mode unless the script has coroutine support. In UI mode, it is recommended to use `auto()` instead.

## auto.setMode(mode)

* `mode` {string} Mode

Sets the Accessibility mode. Available values:

* `fast` — Fast mode (enables widget caching for faster selector queries).
* `normal` — Normal mode (default).

## auto.setFlags(flags)

**[Added in v4.1.0]**

* `flags` {string} | {Array} Flags to enable or disable certain features, including:
    * `findOnUiThread` — When enabled, selector searches are performed on the main thread. This was intended to solve secondary issues caused by thread safety problems (though it appears the original issues were not actually thread-safety related).
    * `useUsageStats` — Uses the "Usage Stats" service to detect the currently running app package name (requires "Usage access" permission). Useful if `currentPackage()` returns inaccurate results.
    * `useShell` — Uses shell commands to get the current app's package name and activity name (requires root).

Enables specific automator-related features. Example:

```js
auto.setFlags(["findOnUiThread", "useShell"]);
```

## auto.service

**[Added in v4.1.0]**

* [AccessibilityService](https://developer.android.com/reference/android/accessibilityservice/AccessibilityService/)

Returns the Accessibility service instance. Returns `null` if the service is not running.

See [AccessibilityService](https://developer.android.com/reference/android/accessibilityservice/AccessibilityService/).

## auto.windows

**[Added in v4.1.0]**

* {Array}

An array of all current windows ([AccessibilityWindowInfo](https://developer.android.com/reference/android/view/accessibility/AccessibilityWindowInfo/)). This may include the status bar, input method windows, the current app window, popups, floating windows, split-screen apps, etc. You can retrieve layout information for each window individually.

Requires Android 5.0 or higher.

## auto.root

**[Added in v4.1.0]**

* {UiObject}

The root layout element of the current window. Returns `null` if the Accessibility service is not running or if all WindowFilters return `false`.

If no `windowFilter` is set, this returns the active window (the window that has focus or is being touched). If a `windowFilter` is set, it returns the root of the first window that passes the filter.

On Android versions below 5.0, this always returns the root of the currently active window.

## auto.rootInActiveWindow

**[Added in v4.1.0]**

* {UiObject}

The root layout element of the currently active window (the window with focus or being touched). Returns `null` if the Accessibility service is not running.

## auto.setWindowFilter(filter)

**[Added in v4.1.0]**

* `filter` {Function} A function that receives a window ([AccessibilityWindowInfo](https://developer.android.com/reference/android/view/accessibility/AccessibilityWindowInfo/)) and returns a Boolean.

Sets a window filter. This filter determines which windows are considered target windows and affects selector searches.

For example, to make selectors search across **all** windows (including status bar, input method, etc.):

```js
auto.setWindowFilter(function(window) {
    // Return true for every window → search in all windows
    return true;
});
```

Another example — when using split-screen with Auto.js and QQ, and you only want the selector to search within the QQ interface:

```js
auto.setWindowFilter(function(window) {
    // For app windows, the title property is usually the app name
    return window.title == "QQ";
});
```

By default, selectors only search in the currently active window and ignore floating windows, the status bar, etc. Using a `WindowFilter` gives you control over which windows are searched.

**Note:** If the `WindowFilter` returns `false` for all windows, selector searches will return empty results.

This function also affects the result of `auto.windowRoots()`.

Requires Android 5.0 or higher.

## auto.windowRoots

**[Added in v4.1.0]**

* {Array}

Returns an array of root layout elements for all windows that pass the current `WindowFilter`.

On Android versions below 5.0, this always returns the array of root elements of currently active windows.

# SimpleActionAutomator

`SimpleActionAutomator` provides functions to simulate simple operations, such as clicking text, simulating key presses, etc. These functions can be used directly as global functions.

## click(text[, i])

* `text` {string} The text to click
* `i` {number} If the same text appears multiple times on screen, `i` indicates which occurrence to click (starting from 0)

Returns whether the click was successful. Returns `false` if the text does not exist on screen or if the area containing the text is not clickable. Otherwise returns `true`.

This function can click most buttons that contain text, for example the "Chats", "Contacts", "Discover", and "Me" buttons at the bottom of WeChat's main screen.

It is commonly used together with `while` to keep trying until a button is successfully clicked:

```js
while (!click("Scan"));
```

When the `i` parameter is not specified, it will attempt to click **all** occurrences of the text on screen and return whether all of them were clicked successfully.

`i` starts from 0. For example:
- `click("Hello", 0)` clicks the first "Hello" on screen
- `click("Hello", 1)` clicks the second "Hello" on screen

> The "area containing the text" refers to the clickable ancestor found by traversing upward from the text element.

## click(left, top, bottom, right)

* `left` {number} Distance from the left edge of the screen to the left side of the rectangular area (in pixels)
* `top` {number} Distance from the top edge of the screen to the top side of the rectangular area (in pixels)
* `bottom` {number} Distance from the top edge of the screen to the bottom side of the rectangular area (in pixels)
* `right` {number} Distance from the left edge of the screen to the right side of the rectangular area (in pixels)

**Note:** This function is mainly intended for use in recorded scripts. It is generally not recommended to use it directly in manually written code.

Clicks a control within the specified rectangular area. Returns `false` if no area on screen exactly matches the given rectangle or if the area is not clickable.

Some buttons or UI elements are icons rather than text (for example, the camera icon when posting to Moments, or the message/contact/status icons at the bottom of QQ). In such cases, you cannot use `click(text, i)`. Instead, you can click by describing the region where the icon is located using `left`, `top`, `right`, and `bottom`.

You can use the layout analysis tool in the floating window to inspect the `bounds` property of controls to determine the click area.

This statement is generated when recording scripts via the Accessibility service.

## longClick(text[, i])

* `text` {string} The text to long-press
* `i` {number} If the same text appears multiple times, `i` indicates which occurrence to long-press (starting from 0)

Returns whether the long press was successful.

When `i` is not specified, it attempts to long-press all occurrences of the text and returns whether all succeeded.

## scrollUp([i])

* `i` {number} Index of the scrollable control (0-based)

Finds the (i+1)th scrollable control and scrolls it **up or left**. Returns whether the operation succeeded. Returns `false` if no scrollable control exists on screen.

When called without the `i` parameter, `scrollUp()` finds the largest scrollable control on screen and scrolls it up or left (for example, the chat list in WeChat).

When `i` is provided, it scrolls the (i+1)th scrollable control. For example, `scrollUp(0)` scrolls the first scrollable control.

## scrollDown([i])

* `i` {number} Index of the scrollable control (0-based)

Finds the (i+1)th scrollable control and scrolls it **down or right**. Returns whether the operation succeeded.

When no parameter is given, it scrolls the largest scrollable control down or right.

## setText([i, ]text)

* `i` {number} The (i+1)th input box (optional)
* `text` {string} The text to set

Returns whether setting the text succeeded. Returns `false` if the corresponding input box could not be found.

When `i` is omitted, sets the text of **all** input boxes to the given value. For example: `setText("Test")`.

This function **replaces** the existing text in the input box (it does not append).

## input([i, ]text)

* `i` {number} The (i+1)th input box (optional)
* `text` {string} The text to input

Returns whether input succeeded. Returns `false` if the corresponding input box could not be found.

When `i` is omitted, appends the given text to **all** input boxes. For example: `input("Test")`.